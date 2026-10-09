---
title: "The 75-cent hacker"
description: "How a tiny accounting error led an astronomer to a KGB-backed spy ring."
date: 2026-10-09
draft: false
summary: "In 1986, a 75-cent gap in a lab's billing led an astronomer turned sysadmin to a hacker selling secrets to the KGB."
tags: ["Friday Fun Fact", "Blue Team", "History", "Honeypot"]
---

**75 cents. That's all that was missing from a computer bill — and it brought down a spy ring.**

## A rounding error that wasn't

In 1986, Cliff Stoll was an astronomer who had become a system administrator at Lawrence Berkeley Laboratory, in California. Scientists paid for the computer time they used, and his supervisor asked him to explain a 75-cent gap in the accounting.

Most people would have written it off as a rounding error. Stoll dug in. He traced the gap to an unknown user who had used nine seconds of computing time without paying. Worse, the intruder had gained root access to the system.

## Ten months on the trail

Instead of simply locking the intruder out, Stoll and his colleagues chose to watch him. For about ten months, Stoll followed his every session, kept detailed notes in a logbook, and discovered that the lab was only a stepping stone: the intruder was using it to reach US military systems.

## The trap

Stoll noticed that the intruder was interested in the "Star Wars" missile defense program (SDI). So he created a fake "SDInet" account full of impressive-sounding but meaningless documents. The bait worked: the intruder stayed connected long enough for the connection to be traced across international networks. It is often described as one of the earliest documented uses of a **honeypot**.

The trail led to West Germany and to Markus Hess, who had been selling the results of his intrusions to the KGB. He was convicted of espionage in 1990.

## The Blue Team lesson

Attacks rarely hide in big, obvious alerts. They hide in small anomalies that nobody takes the time to explain. Stoll's investigation also shows the value of two habits every defender needs today:

- **Keep and read your logs.** Without the accounting records, there would have been no gap to notice.
- **Document everything.** Stoll's logbook made it possible to understand the attacker's methods and, later, to prove what happened.

## Sources

- Clifford Stoll, *The Cuckoo's Egg* (1989)
- Clifford Stoll, "Stalking the Wily Hacker", *Communications of the ACM* (1988)
- [Markus Hess — Wikipedia](https://en.wikipedia.org/wiki/Markus_Hess)
- [The Cuckoo's Egg — Wikipedia](https://en.wikipedia.org/wiki/The_Cuckoo%27s_Egg_(book))
- [How a Berkeley eccentric beat the Russians — California Magazine](https://alumni.berkeley.edu/california-magazine/spring-2016-war-stories/how-berkeley-eccentric-beat-russians-and-then-made/)

*Illustration: fictional reconstruction of an accounting report, not an original 1986 document.*
