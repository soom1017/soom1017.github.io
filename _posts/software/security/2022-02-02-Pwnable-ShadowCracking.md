---
title: Pwnable &#124; FTZ HackerSchool - Level8. Shadow Cracking
date: 2022-02-02 00:00:00 +0900
categories: [Software, Security]
tags: [writeups, problem_solving]
author: soom1017
---

## Intro
Here's hint file. I have to find a shadow file, of which size is 2700.

![problem_description](/assets/img/pwnable/shadowcracking.png)
_"shadow file": Usually has password informations_

I got to find the shadow file, of course it's not `/etc/shadow`{: .filepath}.

![problem_description](/assets/img/pwnable/found_txt.png)

It seems `found.txt`{: .filepath} is shadow file, and it really does have read access in level8 group.

![problem_description](/assets/img/pwnable/found_txt2.png)

## Exploit
Structure of the shadow file is,
```bash
username:pw($id$salt$hashed):last-password-changed:min-required:max-required:warn:inactive:expire
# min/max-required: min/max days the password is valid.
```

`id` in pw means an applied hash algorithm like below. So in this case, it's encrpyted by MD5.

![exploit](/assets/img/pwnable/shadowid.png)

I couldn't just decrypt with MD5 decrypters in Google, so I searched for Unix's password cracker. There was a cracking tool named "John the ripper", and I finally got the flag.

![exploit](/assets/img/pwnable/found_txt3.png)