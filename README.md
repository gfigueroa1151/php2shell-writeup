# php2shell-writeup
My lab writeup of the php2shell exploit

PHP2Shell Lab Writeup

A blue team walkthrough of PHP2Shell, the pair of critical PHP vulnerabilities (CVE-2026-109618 and CVE-2026-109619) that got emergency patches on October 21, 2026. I worked through the TryHackMe room against a vulnerable PHP server and wrote up what the attack does and, more importantly for where I am headed, how a defender would catch it.

The full writeup, with the room diagrams and screenshots from my own run, is in the Word document in this repo.

What this covers
The short version: why this one matters. The flaw is in the PHP runtime itself, not in any application, so an unauthenticated attacker can run code before the website's own code even starts. A clean, well built site gets no protection from it.

How the attack works: the chain in plain terms, from the upload progress foothold, to the memory bailout that leaves a dangling pointer, to the cookie header memory leak that defeats ASLR, to the forged destructor that lands code execution as www-data.

The defender's view: why you cannot fix this at the application layer, the interim measures that buy time before patching, the one defense that does not help (a module based WAF), what to detect, and the post exploitation activity to watch for.
Key takeaway

Patch the PHP runtime (8.5.12, 8.4.27, 8.3.36, or 8.2.35) and restart every worker. Updating WordPress, Drupal, or Laravel does nothing, because the broken code sits underneath all of them. The lesson I took from this is to treat the runtime as part of the attack surface and patch it with the same urgency as the application.

Why I built this

I am an IT Support Specialist at the Washington State Department of Health transitioning into blue team work, targeting SOC and incident response roles. This is part of a series of hands-on labs and writeups I use to build and document detection and response skills.

Lab completed on TryHackMe, October 2026. The exploit explanation is kept at the concept level.
