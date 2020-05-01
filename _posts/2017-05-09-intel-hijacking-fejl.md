---
layout: post
title: Intel Hijacking fejl
link: https://www.grahamcluley.com/intel-patches-remote-hijack-bug-hid-chips-seven-years/
---

![Chip]({{ site.url }}/public/assets/20170509_chip.jpg)

Udemærket intro til det store gabende hul i Intels professionelle chips af David Bisson:

> [...] by exploiting this vulnerability, an unauthenticated network attacker could gain system privileges to the AMT or ISM technology. From there, they could abuse their privileges to reboot the system and examine drive contents.

> That's not even the worst part. Linux kernel expert Matthew Garrett elaborates:

>> "AMT supports providing an ISO remotely. In older versions of AMT (before 11.0) this was in the form of an emulated IDE controller. In 11.0 and later, this takes the form of an emulated USB device. The nice thing about the latter is that any image provided that way will probably be automounted if there's a logged in user, which probably means it's possible to use a malformed filesystem to get arbitrary code execution in the kernel. Fun!"

Min arbejdsmaskine _havde_ AMT slået til. Måske jeg lige skal tjekke en kollegas. Remote...
