---
title: "Infrastructure TSSR — Active Directory, GLPI et VLAN"
description: "Épreuve pratique du Titre Professionnel TSSR : un domaine Windows, le DHCP, un serveur GLPI authentifié sur l'AD, la segmentation en VLAN, la sauvegarde des configurations et une GPO, montés de zéro."
date: 2026-01-14
draft: false
weight: 5
summary: "L'épreuve pratique de mon titre systèmes et réseaux : un domaine Windows, GLPI authentifié sur Active Directory, du routage inter-VLAN et une GPO de démarrage."
categories: ["Systèmes et réseaux"]
tags: ["TSSR", "Active Directory", "GLPI", "Cisco", "GPO"]
showTaxonomies: true
showTableOfContents: true
---

*Épreuve pratique (ECF) du Titre Professionnel Technicien Supérieur Systèmes et Réseaux (TSSR, RNCP niveau 5), janvier 2026.*

{{< lead >}}
Une entreprise fictive, sept missions, et une preuve horodatée pour chaque étape.
{{< /lead >}}

## Le sujet

L'épreuve met en scène un studio de design fictif, *CreativeFusion Studios*. Ses problèmes sont très courants : un mot de passe par application, des demandes de support perdues entre mails et appels, et tous les services sur un même réseau à plat. Ma mission était d'y remédier, puis de prouver chaque étape par des captures horodatées.

La copie d'examen n'est pas publiée. Toutes les captures de cette page en sont issues, et chaque commande ou fichier de configuration est retranscrit depuis ces captures, sans rien ajouter. Quand j'ai corrigé quelque chose après coup, je le signale.

| # | Mission | Outils |
|---|---------|--------|
| 1 | [Créer le domaine de l'entreprise](#1--domaine-active-directory) | Windows Server 2022, AD DS, DNS |
| 2 | [Une étendue DHCP par service](#2--étendues-dhcp) | DHCP Windows |
| 3 | [Un serveur de ticketing pour le support](#3--serveur-de-ticketing-glpi) | Debian 13, Apache, PHP-FPM 8.4, MariaDB, GLPI 11 |
| 4 | [Se connecter à GLPI avec son compte de domaine](#4--authentification-glpi-sur-lactive-directory) | LDAP, compte de service AD |
| 5 | [Segmenter le réseau, router entre VLAN](#5--segmentation-en-vlan-et-routage-inter-vlan) | Cisco Packet Tracer, 2960 + 2901 |
| 6 | [Sauvegarder les configs du switch et du routeur](#6--sauvegarde-des-configurations-sur-ftp) | IOS `copy running-config ftp:` |
| 7 | [Empêcher les IP fixes saisies par les utilisateurs](#7--gpo-qui-force-le-dhcp-au-démarrage) | GPO, script PowerShell au démarrage |

## Les machines et le réseau

La [RFC 1178](https://www.rfc-editor.org/rfc/rfc1178) recommande de nommer les machines d'après un thème plutôt que leur rôle. J'ai choisi la mythologie nordique : pour quelqu'un qui met le cap au nord, ça s'imposait.

| Hôte | Rôle | OS | IP |
|------|------|----|----|
| **MIDGARD** | Contrôleur de domaine, DNS, DHCP | Windows Server 2022 | 10.0.60.1 (fixe) |
| **YGGDRASIL** | Serveur GLPI (sans interface graphique) | Debian 13 | 10.0.60.2 (fixe) |
| **THOR** | Poste de test joint au domaine | Windows 10 | DHCP |

Missions 1 à 4 et 7 sur machines virtuelles VMware, missions 5 et 6 dans Cisco Packet Tracer.

Six services, un VLAN et un /24 chacun. La passerelle est toujours la dernière adresse utilisable (`.254`), et chaque étendue distribue MIDGARD comme serveur DNS.

| VLAN | Service | Réseau | Passerelle |
|------|---------|--------|------------|
| 10 | RH | 10.0.10.0/24 | 10.0.10.254 |
| 20 | Comptabilité | 10.0.20.0/24 | 10.0.20.254 |
| 30 | Informatique | 10.0.30.0/24 | 10.0.30.254 |
| 40 | Direction | 10.0.40.0/24 | 10.0.40.254 |
| 50 | Design | 10.0.50.0/24 | 10.0.50.254 |
| 60 | Serveurs | 10.0.60.0/24 | 10.0.60.254 |

{{< mermaid >}}
flowchart LR
    R["Router0 · Cisco 2901<br/>Gi0/0.10 … Gi0/0.60<br/>passerelles .254 + ip helper"]
    S["Switch0 · Cisco 2960"]
    R ---|"trunk 802.1Q<br/>Gi0/0 ↔ Fa0/1"| S
    S ---|"Fa0/2 · VLAN 50"| D["PC0 · Design"]
    S ---|"Fa0/3 · VLAN 40"| DG["PC1 · Direction"]
    S ---|"Fa0/4 · VLAN 30"| I["PC2 · Informatique"]
    S ---|"Fa0/5 · VLAN 20"| C["PC3 · Comptabilité"]
    S ---|"Fa0/6 · VLAN 10"| H["PC4 · RH"]
    S ---|"Fa0/7 · VLAN 60"| M["MIDGARD · 10.0.60.1<br/>DHCP + FTP"]
{{< /mermaid >}}

---

## 1 · Domaine Active Directory

**Le besoin.** Un point unique pour gérer comptes et accès : un nouveau domaine, `CreativeFusion-Studios.eu`, sur Windows Server 2022, avec un nom de serveur conforme à la RFC 1178.

**Ce que j'ai fait**

1. Installé Windows Server 2022 et renommé le serveur **MIDGARD**.
2. Configuré une adresse fixe : `10.0.60.1/24`, passerelle `10.0.60.254`.
3. Ajouté le rôle **AD DS**, puis promu le serveur contrôleur de domaine d'une **nouvelle forêt**, `CreativeFusion-Studios.eu`, avec le DNS intégré.
4. Organisé l'annuaire avant de créer quoi que ce soit, en suivant l'organigramme :

```text
CreativeFusion-Studios.eu
├── 00_GROUPES
├── 01_ADMIN
│   └── Comptes_techniques      ← Sync_GLPI, compte de service de GLPI (mission 4)
├── 02_COMPTABILITE
├── 03_DESIGN_ANIMATION
│   ├── PERSONNEL
│   └── POSTES                  ← THOR est ici, cible de la GPO (mission 7)
├── 04_DIRECTION
│   ├── PERSONNEL
│   └── POSTES
├── 05_INFORMATIQUE
│   ├── PERSONNEL
│   └── POSTES
├── 06_RH
│   ├── PERSONNEL
│   └── POSTES
└── 07_SERVEURS
```

Séparer les *personnes* (`PERSONNEL`) et les *ordinateurs* (`POSTES`) dans chaque service sert plus tard : une GPO destinée aux ordinateurs se lie à une OU `POSTES` sans toucher aux comptes utilisateurs.

**La vérification.** `nslookup midgard` résout `midgard.CreativeFusion-Studios.eu` en `10.0.60.1`. Le client Windows 10 **THOR** a rejoint le domaine, et le compte administrateur du domaine y ouvre une session.

![Ouverture de session sur le domaine depuis THOR](01-domain-logon.png)

## 2 · Étendues DHCP

**Le besoin.** Chaque service a son réseau et son étendue DHCP. La passerelle est la dernière adresse utilisable de chaque réseau, le serveur AD garde une adresse fixe, et chaque étendue distribue le serveur AD/DNS comme DNS.

**Ce que j'ai fait.** Ajouté le rôle DHCP sur MIDGARD, terminé sa configuration post-installation, puis créé six étendues :

| Étendue | Réseau | Routeur (option 003) | DNS (option 006) |
|---------|--------|----------------------|------------------|
| Etendue_RH | 10.0.10.0/24 | 10.0.10.254 | 10.0.60.1 |
| Etendue_Comptabilité | 10.0.20.0/24 | 10.0.20.254 | 10.0.60.1 |
| Etendue_Informatique | 10.0.30.0/24 | 10.0.30.254 | 10.0.60.1 |
| Etendue_Direction_Générale | 10.0.40.0/24 | 10.0.40.254 | 10.0.60.1 |
| Etendue_Design_Animation | 10.0.50.0/24 | 10.0.50.254 | 10.0.60.1 |
| Etendue_Serveurs | 10.0.60.0/24 | 10.0.60.254 | 10.0.60.1 |

Exemple de plage, pour la comptabilité : `10.0.20.1` → `10.0.20.253`. Le `.254` reste hors plage puisqu'il appartient à la passerelle.

![Les six étendues sur MIDGARD](02-dhcp-scopes.png)

**La vérification.** Sur THOR, `ipconfig /all` montre un bail obtenu auprès de MIDGARD, avec la bonne passerelle et le bon DNS. THOR est dans le réseau serveurs, son bail vient donc de `Etendue_Serveurs`. Les postes des autres services n'atteignent le serveur que via un relais DHCP entre VLAN : c'est l'objet de la [mission 5](#5--segmentation-en-vlan-et-routage-inter-vlan).

![THOR reçoit son adresse de MIDGARD (adresses MAC floutées)](02-thor-dhcp-lease.png)

## 3 · Serveur de ticketing GLPI

**Le besoin.** Les demandes de support arrivent par mail et par téléphone : rien n'est suivi, et aucune métrique sur les temps de résolution. L'entreprise a choisi GLPI, sur un serveur Debian **sans interface graphique**, dans le réseau serveurs.

**Le serveur.** Debian 13 « trixie » (le sujet demandait Debian 12, mais la 13 était la version stable du moment), nom d'hôte **YGGDRASIL**, adresse fixe `10.0.60.2/24`.

**La pile web** — commandes telles que tapées, dans l'ordre :

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install apache2 -y
sudo apt install php -y
sudo apt-get install php-fpm mariadb-server
sudo apt-get install php-{curl,gd,intl,mysql,zip,bcmath,mbstring,xml,bz2}
sudo apt install php-ldap                 # nécessaire ensuite pour l'authentification AD
```

**La base de données.** Un compte dédié, limité à la base GLPI, plutôt que root :

```bash
sudo mariadb-secure-installation          # root passé en authentification unix_socket
sudo mysql -u root -p
```
```sql
CREATE DATABASE db1_glpi;
GRANT ALL PRIVILEGES ON db1_glpi.* TO glpi_adm@localhost IDENTIFIED BY '********';
FLUSH PRIVILEGES;
```

**GLPI 11.0.4.** Le sujet demandait la 10.0.10 *minimum*. J'ai pris la version courante, compatible avec le PHP 8.4 fourni par Debian 13.

```bash
cd /tmp
wget https://github.com/glpi-project/glpi/releases/download/11.0.4/glpi-11.0.4.tgz
sudo tar -xzvf glpi-11.0.4.tgz -C /var/www/
```

**Configuration, données et journaux hors de la racine web.** Par défaut, ils sont sous `/var/www/glpi`. Les déplacer garantit qu'une erreur de configuration ne pourra jamais les exposer en HTTP.

```bash
sudo chown www-data /var/www/glpi/ -R
sudo mkdir /etc/glpi
sudo chown www-data /etc/glpi/
sudo mv /var/www/glpi/config /etc/glpi
sudo mkdir /var/lib/glpi
sudo chown www-data /var/lib/glpi/
sudo mv /var/www/glpi/files/ /var/lib/glpi
sudo mkdir /var/log/glpi
sudo chown www-data /var/log/glpi
```

Puis on indique à GLPI où chercher :

```php
<?php
// /var/www/glpi/inc/downstream.php
define('GLPI_CONFIG_DIR', '/etc/glpi/');
if (file_exists(GLPI_CONFIG_DIR . '/local_define.php')) {
        require_once GLPI_CONFIG_DIR . '/local_define.php';
}
```
```php
<?php
// /etc/glpi/local_define.php
define('GLPI_VAR_DIR', '/var/lib/glpi/files');
define('GLPI_LOG_DIR', '/var/log/glpi');
```

**Apache + PHP-FPM.** Un hôte virtuel dédié, dont la racine est uniquement `/var/www/glpi/public` :

{{< accordion >}}
{{< accordionItem title="/etc/apache2/sites-available/support-creative-fusion-studios.eu.conf" >}}
```apache
<VirtualHost *:80>
        ServerName support-creative-fusion-studios.eu
        DocumentRoot /var/www/glpi/public

        <Directory /var/www/glpi/public>
                Require all granted

                RewriteEngine On

                #ensure authorization headers are passed to PHP.
                #Some apache configurations may filter them and break usage of API, CalDAV...

                RewriteCond %{HTTP:Authorization} ^(.+)$
                RewriteRule .* - [E=HTTP_AUTHORIZATION:%{HTTP:Authorization}]

                #redirect all request to GLPI router, unless file exists.

                RewriteCond %{REQUEST_FILENAME} !-f
                RewriteRule ^(.*)$ index.php [QSA,L]

        </Directory>

        <FilesMatch \.php$>
                SetHandler "proxy:unix:/run/php/php8.4-fpm.sock|fcgi://localhost/"
        </FilesMatch>
</VirtualHost>
```
{{< /accordionItem >}}
{{< /accordion >}}

```bash
sudo a2ensite support-creative-fusion-studios.eu.conf
sudo a2dissite 000-default.conf
sudo a2enmod proxy_fcgi setenvif
sudo a2enconf php8.4-fpm
sudo systemctl restart apache2
```

**Durcissement des sessions PHP**, dans `/etc/php/8.4/fpm/php.ini` :

```ini
session.cookie_httponly = on      ; cookie illisible par JavaScript (limite le vol de session par XSS)
session.cookie_samesite = Lax     ; cookie non envoyé sur les requêtes intersites (protection CSRF)
```

**L'installeur web**, lancé depuis un navigateur du réseau (`http://10.0.60.2`), puis :

```bash
sudo rm /var/www/glpi/install/install.php
```

Dernière étape : changement du mot de passe du compte super-admin par défaut `glpi`.

**La vérification.** `systemctl status apache2` → `active (running)` après chaque modification, `ip a` → `10.0.60.2/24`, et le tableau de bord GLPI accessible depuis le réseau.

![Tableau de bord GLPI](03-glpi-dashboard.png)

{{< alert icon="circle-info" >}}
Le bandeau orange, c'est GLPI qui signale que les autres comptes par défaut (`post-only`, `tech`, `normal`) avaient encore leur mot de passe d'origine. Voir [ce que je durcirais](#avec-le-recul).
{{< /alert >}}

## 4 · Authentification GLPI sur l'Active Directory

**Le besoin.** Les utilisateurs se connectent à GLPI avec leur compte de domaine, et non avec un mot de passe GLPI à part.

**Ce que j'ai fait.** Un compte de service dans l'AD, `Sync_GLPI`, dans `01_ADMIN/Comptes_techniques`. GLPI s'en sert uniquement pour lire l'annuaire : aucun identifiant administrateur n'est stocké sur le serveur GLPI. Puis un nouvel annuaire LDAP dans GLPI (*Configuration → Authentification → Annuaire LDAP*) :

| Champ | Valeur |
|-------|--------|
| Serveur / port | `10.0.60.1` / `389` |
| Filtre de connexion | `(&(objectCategory=person)(objectClass=user))` |
| BaseDN | `DC=creativefusion-studios,DC=eu` |
| Compte de bind | `CN=Sync_GLPI,OU=Comptes_techniques,OU=01_ADMIN,DC=creativefusion-studios,DC=eu` |
| Champ de l'identifiant | `samaccountname` |
| Champ de synchronisation | `objectguid` |

`objectguid` plutôt que l'identifiant : si un utilisateur est renommé dans l'AD, GLPI reconnaît toujours la même personne.

**La vérification.** Le test intégré à GLPI : connexion TCP, BaseDN, bind et recherche réussis (8 entrées trouvées).

![Test LDAP dans GLPI](04-glpi-ldap-test.png)

J'ai ensuite créé des utilisateurs de test dans l'AD, ouvert une session sur THOR pour définir leur mot de passe, puis je me suis connecté à GLPI avec la source **Active Directory**. Les utilisateurs AD apparaissent alors dans la liste des utilisateurs GLPI.

![Connexion avec un compte AD](04-glpi-ad-logon.png)

![Les utilisateurs AD dans GLPI](04-glpi-ad-users.png)

## 5 · Segmentation en VLAN et routage inter-VLAN

**Le besoin.** Segmenter le réseau par service, tout en permettant à chaque poste d'obtenir son adresse du serveur DHCP et de pinguer toutes les autres machines. Il faut donc router entre les VLAN.

Réalisé dans **Cisco Packet Tracer**, à partir de la topologie fournie par le sujet : un switch 2960, un routeur 2901, un PC par service et le serveur.

![Topologie finale dans Packet Tracer](05-packet-tracer-topology.png)

**Le switch.** Les VLAN 10 à 60, nommés d'après les services, un port d'accès par VLAN (Fa0/2 → Fa0/7), et Fa0/1 en **trunk 802.1Q** vers le routeur, limité aux VLAN 10 à 60.

**Le routeur.** Un « router-on-a-stick » : un seul lien physique, une sous-interface par VLAN, chacune étant la passerelle (`.254`) de son réseau.

```text
interface gigabitEthernet 0/0.10
 encapsulation dot1Q 10
 ip address 10.0.10.254 255.255.255.0
```

**Le DHCP entre VLAN.** Une requête DHCP est un broadcast, et un broadcast ne traverse pas un routeur. Sur chaque sous-interface cliente, `ip helper-address 10.0.60.1` transforme le broadcast en unicast vers le serveur. Le VLAN 60 n'en a pas besoin : le serveur y est déjà.

**Le serveur (MIDGARD dans Packet Tracer).** Adresse fixe `10.0.60.1`, passerelle `10.0.60.254`, un pool DHCP par VLAN client (début `.1`, passerelle `.254`, DNS `10.0.60.1`). Tous les PC en DHCP.

{{< accordion >}}
{{< accordionItem title="Switch0 — liste complète des commandes" >}}
```text
enable
configure terminal
vlan 10
 name RH
 exit
vlan 20
 name COMPTABILITE
 exit
vlan 30
 name INFORMATIQUE
 exit
vlan 40
 name DIRECTION
 exit
vlan 50
 name DESIGN
 exit
vlan 60
 name SERVEURS
 exit
interface fa0/2
 switchport mode access
 switchport access vlan 50
 exit
interface fa0/3
 switchport mode access
 switchport access vlan 40
 exit
interface fa0/4
 switchport mode access
 switchport access vlan 30
 exit
interface fa0/5
 switchport mode access
 switchport access vlan 20
 exit
interface fa0/6
 switchport mode access
 switchport access vlan 10
interface fa0/7
 switchport mode access
 switchport access vlan 60
 exit
interface fa0/1
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50,60
 no shutdown
 exit
```
{{< /accordionItem >}}
{{< accordionItem title="Router0 — liste complète des commandes" >}}
```text
enable
configure terminal
interface gigabitEthernet 0/0
 no shutdown
 exit
interface gigabitEthernet 0/0.10
 encapsulation dot1Q 10
 ip address 10.0.10.254 255.255.255.0
 ip helper-address 10.0.60.1
 exit
interface gigabitEthernet 0/0.20
 encapsulation dot1Q 20
 ip address 10.0.20.254 255.255.255.0
 ip helper-address 10.0.60.1
 exit
interface gigabitEthernet 0/0.30
 encapsulation dot1Q 30
 ip address 10.0.30.254 255.255.255.0
 ip helper-address 10.0.60.1
 exit
interface gigabitEthernet 0/0.40
 encapsulation dot1Q 40
 ip address 10.0.40.254 255.255.255.0
 ip helper-address 10.0.60.1
 exit
interface gigabitEthernet 0/0.50
 encapsulation dot1Q 50
 ip address 10.0.50.254 255.255.255.0
 ip helper-address 10.0.60.1
 exit
interface gigabitEthernet 0/0.60
 encapsulation dot1Q 60
 ip address 10.0.60.254 255.255.255.0
 exit
```
*Regroupé par sous-interface pour la lisibilité : pendant l'examen, les helper-address ont été ajoutées dans un second temps.*
{{< /accordionItem >}}
{{< accordionItem title="Vérification — show vlan brief / show ip interface brief" >}}
```text
Switch#show vlan brief
VLAN Name                             Status    Ports
---- -------------------------------- --------- ------------------------------
1    default                          active    Fa0/1, Fa0/8, Fa0/9, Fa0/10 …
10   RH                               active    Fa0/6
20   COMPTABILITE                     active    Fa0/5
30   INFORMATIQUE                     active    Fa0/4
40   DIRECTION                        active    Fa0/3
50   DESIGN                           active    Fa0/2
60   SERVEURS                         active    Fa0/7

Router#show ip interface brief
Interface              IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0     unassigned      YES unset  up                    up
GigabitEthernet0/0.10  10.0.10.254     YES manual up                    up
GigabitEthernet0/0.20  10.0.20.254     YES manual up                    up
GigabitEthernet0/0.30  10.0.30.254     YES manual up                    up
GigabitEthernet0/0.40  10.0.40.254     YES manual up                    up
GigabitEthernet0/0.50  10.0.50.254     YES manual up                    up
GigabitEthernet0/0.60  10.0.60.254     YES manual up                    up
```
{{< /accordionItem >}}
{{< /accordion >}}

**La vérification.** Depuis chaque PC, un ping vers chaque réseau (`ping -n 1`, pour tout faire tenir sur une capture). Depuis PC4 (RH), le TTL raconte l'histoire : **128** pour l'adresse de son propre VLAN, **127** partout ailleurs, soit un saut par le routeur.

![Ping inter-VLAN depuis PC4](05-inter-vlan-ping.png)

## 6 · Sauvegarde des configurations sur FTP

**Le besoin.** Tester la sauvegarde des configurations du switch et du routeur sur le serveur FTP, avec le compte `admin` / `Cisco` fourni par le sujet.

**Le routeur.** Ma première tentative passait les identifiants dans l'URL :

```text
Router#copy running-config ftp://admin:Cisco@10.0.60.1/router_backup.cfg
% Invalid input detected at '^' marker.
```

L'IOS de Packet Tracer n'accepte pas cette syntaxe : il faut d'abord déclarer les identifiants dans la configuration.

```text
Router(config)#ip ftp username admin
Router(config)#ip ftp password Cisco
Router#copy running-config ftp:
Address or name of remote host []? 10.0.60.1
Destination filename [Router-confg]? router_backup.cfg
[OK - 1367 bytes]
```

**Le switch.** Mêmes commandes, mais la première copie a échoué :

```text
%Error opening ftp://.../switch_backup.cfg (Timed out)
```

Un switch de niveau 2 n'a pas d'adresse IP par défaut : il ne pouvait tout simplement pas joindre le serveur FTP. La solution : une interface de management dans le VLAN serveurs et une passerelle par défaut.

```text
interface vlan 60
 ip address 10.0.60.2 255.255.255.0
 no shutdown
ip default-gateway 10.0.60.254
```

Ensuite : `[OK - 1592 bytes]`.

**La vérification.** Les deux fichiers sont présents sur le serveur FTP.

![router_backup.cfg et switch_backup.cfg sur le serveur FTP](06-ftp-backups.png)

## 7 · GPO qui force le DHCP au démarrage

**Le besoin.** Un ticket récurrent : des utilisateurs ne peuvent pas se connecter avec leur compte de domaine, parce que certains ont saisi une IP fixe. Le sujet demande une GPO qui exécute un script PowerShell au **démarrage de l'ordinateur** pour remettre la carte réseau en DHCP.

**Ce que j'ai fait**

1. Un groupe de sécurité, `G_DHCP_POSTES`, avec THOR comme membre.
2. Le script, stocké dans SYSVOL pour que tous les ordinateurs du domaine puissent le lire (`\\CreativeFusion-Studios.eu\SYSVOL\CreativeFusion-Studios.eu\scripts\`) :

```powershell
# force_dhcp.ps1 — pour chaque carte active : DHCP activé, DNS manuels supprimés
Get-NetAdapter | Where-Object {$_.Status -eq "Up"} | ForEach-Object {
        Set-NetIPInterface -InterfaceIndex $_.InterfaceIndex -Dhcp Enabled
        Set-DnsClientServerAddress -InterfaceIndex $_.InterfaceIndex -ResetServerAddresses
}
```
```bat
:: force_dhcp.bat — lanceur
@echo off
powershell.exe -NoProfile -ExecutionPolicy Bypass -File "\\CreativeFusion-Studios.eu\SYSVOL\CreativeFusion-Studios.eu\scripts\force_dhcp.ps1"
exit /b 0
```

3. La GPO `GPO_FORCE_DHCP_STARTUP`, liée à `03_DESIGN_ANIMATION/POSTES`, où se trouve THOR :
   - *Configuration ordinateur → Stratégies → Paramètres Windows → Scripts → Démarrage* → le lanceur `.bat` ;
   - filtrage de sécurité sur `G_DHCP_POSTES` au lieu de *Utilisateurs authentifiés* ;
   - *Toujours attendre le réseau lors du démarrage de l'ordinateur et de l'ouverture de session* → **Activé**, pour que le script ne s'exécute pas avant que le réseau soit prêt.

**La vérification.** Sur THOR, `gpupdate /force`, puis `gpresult /r /scope computer` en administrateur : `GPO_FORCE_DHCP_STARTUP` figure parmi les stratégies appliquées, et THOR est bien membre de `G_DHCP_POSTES`.

![gpresult sur THOR](07-gpresult.png)

{{< alert icon="triangle-exclamation" >}}
**Corrigé après coup.** En relisant mes captures pour cette page, j'ai trouvé deux fautes de frappe dans la ligne DNS du script écrit pendant l'examen : `- InterfaceIndex` (avec une espace) et `-ResetServerAdresses`. Le script ci-dessus est la version corrigée. `gpresult` prouve que la GPO a été *appliquée*, pas que chaque ligne a *réussi* : la ligne DHCP était correcte, la ligne DNS aurait échoué.
{{< /alert >}}

---

## Avec le recul

L'examen demandait que ça fonctionne. Avec un regard sécurité, voici ce que je ferais autrement.

**Mes erreurs, gardées volontairement**

- **Une faute de frappe dans le script de la GPO :** la GPO s'appliquait, mais une ligne aurait échoué. Leçon retenue : un script se teste à la main sur un poste avant qu'une GPO ne le pousse sur tous les autres.
- **Un mauvais masque** sur une sous-interface du routeur (`255.255.255.255`), refusé par l'IOS : `Bad mask /32 for address 10.0.40.254`. Un rappel : lire la sortie de la console plutôt qu'enchaîner les commandes à l'aveugle.
- **Une sauvegarde du switch en échec**, faute d'IP de management. Évident une fois compris : un équipement de niveau 2 a besoin d'une adresse pour parler à qui que ce soit.

**Ce que je durcirais sur un réseau de production**

| Point | À l'examen | En production |
|-------|------------|---------------|
| LDAP entre GLPI et l'AD | port 389, non chiffré | LDAPS (636) ou StartTLS, pour que le mot de passe du compte de service ne circule jamais en clair |
| Comptes GLPI par défaut | `post-only`, `tech`, `normal` encore avec leur mot de passe d'origine | les modifier ou les désactiver dès l'installation |
| GLPI en HTTP | `http://10.0.60.2` | HTTPS avec un certificat d'une AC interne |
| Sauvegardes de configuration | FTP avec identifiants en clair, imposé par le sujet | SCP/SFTP, un compte dédié, des sauvegardes versionnées |
| Lanceur du script | `-ExecutionPolicy Bypass` | un script signé et une stratégie `AllSigned` |
| Nom du domaine AD | `CreativeFusion-Studios.eu`, un TLD public, imposé par le sujet | un sous-domaine que l'entreprise possède réellement (ex. `ad.example.com`), pour éviter les conflits DNS avec Internet |
| Traiter le symptôme | une GPO remet le DHCP à chaque démarrage | retirer aussi aux utilisateurs standard le droit de modifier les paramètres réseau |

## Technologies

Windows Server 2022 · Active Directory · DNS · DHCP · GPO · PowerShell · Debian 13 · Apache · PHP-FPM · MariaDB · GLPI 11 · LDAP · Cisco IOS · Packet Tracer

<div style="display:flex;flex-wrap:wrap;gap:0.75rem;margin-top:1.5rem">
{{< button href="https://github.com/cedricVrvrd/tssr-infra-ad-glpi-vlan" target="_blank" rel="noopener" >}}
Fichiers de configuration sur GitHub
{{< /button >}}
</div>
