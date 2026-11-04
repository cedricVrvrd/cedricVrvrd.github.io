# Heading North

Personal website of **Cédric Vervoord** — a DevOps homelab journey, built in public.
Site personnel de **Cédric Vervoord** — un parcours DevOps et un homelab, construits en public.

🌐 **https://cedricvrvrd.github.io/** (EN by default · FR under `/fr/`)

[English](#english) · [Français](#français)

---

## English

### What's on the site

| Section | Folder | Content |
|---|---|---|
| Heading North Lab | `content/heading-north-lab/` | A step-by-step homelab project following the story of a **fictional** company, Norrøn Voyages |
| Projects | `content/projects/` | Web development, systems and networks, and DevOps projects, with demos and code links |
| Tech Watch | `content/tech-watch/` | A verified, sourced news item each week (cybersecurity, DevOps, networking) |
| Friday Fun Facts | `content/fun-facts/` | True, sourced anecdotes from IT and security history |
| CTF Write-ups | `content/ctf-writeups/` | CTF challenges I solve: the approach and what I take from it |
| CV · Contact | `content/cv/`, `content/contact/` | Résumé and contact details |

### Stack

- [Hugo](https://gohugo.io/) **extended** (version pinned in the workflow: `HUGO_VERSION` in `.github/workflows/hugo.yaml`)
- [Blowfish](https://blowfish.page/) theme, as a Git submodule in `themes/blowfish`
- Hosting on **GitHub Pages**, deployed by **GitHub Actions** on every push to `main`
- Two languages: English (default) and French

### Repository layout

```
archetypes/   content templates
assets/       custom CSS (assets/css/custom.css), images
config/       Hugo configuration (hugo.toml, languages, menus, params)
content/      all pages, one folder per section
static/       favicons and static files
themes/       Blowfish (submodule)
```

### Run it locally

```bash
git clone --recurse-submodules git@github.com:cedricVrvrd/cedricVrvrd.github.io.git
cd cedricVrvrd.github.io
hugo server -D -F --disableFastRender
```

If the theme folder is empty after cloning: `git submodule update --init --recursive`.
`-D` shows drafts and `-F` shows future-dated pages; the production build uses neither.

### Writing content

- Each page is a **bundle**: a folder with `index.en.md`, `index.fr.md` and a `featured.png` thumbnail (1200 × 630).
- Front matter: `title`, `description`, `date`, `draft`, `summary`, `tags`.
- **A page is published when `draft: false` and its `date` is not in the future** (`buildDrafts` and `buildFuture` are off).
- Tech Watch and Fun Facts are always sourced; CTF write-ups never show flags or answers of active rooms.
- No public IPs, internal domain names, keys, tokens or sensitive hostnames in any page or screenshot.

### Deployment

A push to `main` triggers the **Build and deploy** workflow. In the repository settings, Pages must use **Source: GitHub Actions**. To check that everything is pushed: `git log --oneline origin/main..main` should be empty.

### Credits

Theme: [Blowfish](https://github.com/nunocoracao/blowfish) by Nuno Coração — see the theme repository for its license.

---

## Français

### Ce que contient le site

| Rubrique | Dossier | Contenu |
|---|---|---|
| Heading North Lab | `content/heading-north-lab/` | Un projet de homelab pas à pas, qui suit le scénario d'une entreprise **fictive**, Norrøn Voyages |
| Projets | `content/projects/` | Projets de développement web, systèmes et réseaux, et DevOps, avec démos et liens vers le code |
| Veille | `content/tech-watch/` | Chaque semaine, une actualité vérifiée et sourcée (cybersécurité, DevOps, réseau) |
| Friday Fun Facts | `content/fun-facts/` | Des anecdotes vraies et sourcées sur l'histoire de l'informatique et de la sécurité |
| Write-ups CTF | `content/ctf-writeups/` | Les épreuves CTF que je résous : la démarche et ce que j'en retiens |
| CV · Contact | `content/cv/`, `content/contact/` | CV et coordonnées |

### Technologies

- [Hugo](https://gohugo.io/) version **extended** (version fixée dans le workflow : `HUGO_VERSION` dans `.github/workflows/hugo.yaml`)
- Thème [Blowfish](https://blowfish.page/), en sous-module Git dans `themes/blowfish`
- Hébergement sur **GitHub Pages**, déploiement par **GitHub Actions** à chaque push sur `main`
- Deux langues : anglais (par défaut) et français

### Organisation du dépôt

```
archetypes/   modèles de contenu
assets/       CSS personnalisé (assets/css/custom.css), images
config/       configuration Hugo (hugo.toml, langues, menus, paramètres)
content/      toutes les pages, un dossier par rubrique
static/       favicons et fichiers statiques
themes/       Blowfish (sous-module)
```

### Lancer le site en local

```bash
git clone --recurse-submodules git@github.com:cedricVrvrd/cedricVrvrd.github.io.git
cd cedricVrvrd.github.io
hugo server -D -F --disableFastRender
```

Si le dossier du thème est vide après le clonage : `git submodule update --init --recursive`.
`-D` affiche les brouillons et `-F` les pages à date future ; le build de production n'utilise ni l'un ni l'autre.

### Écrire du contenu

- Chaque page est un **bundle** : un dossier avec `index.en.md`, `index.fr.md` et une vignette `featured.png` (1200 × 630).
- Front matter : `title`, `description`, `date`, `draft`, `summary`, `tags`.
- **Une page est publiée si `draft: false` et si sa `date` n'est pas dans le futur** (`buildDrafts` et `buildFuture` sont désactivés).
- La veille et les Fun Facts sont toujours sourcés ; les write-ups CTF n'affichent jamais les flags ni les réponses des rooms actives.
- Aucune IP publique, nom de domaine interne, clé, jeton ou nom d'hôte sensible dans une page ou une capture.

### Déploiement

Un push sur `main` lance le workflow **Build and deploy**. Dans les paramètres du dépôt, Pages doit utiliser **Source : GitHub Actions**. Pour vérifier que tout est poussé : `git log --oneline origin/main..main` doit être vide.

### Crédits

Thème : [Blowfish](https://github.com/nunocoracao/blowfish) de Nuno Coração — voir le dépôt du thème pour sa licence.
