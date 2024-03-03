---
title: Pwnable &#124; FTZ HackerSchool - Level4. Backdoor
date: 2022-01-31 00:00:00 +0900
categories: [Software, Security]
tags: [writeups, problem_solving]
author: soom1017
---

## Intro
The hint file says, someone has plant a backdoor in `/etc/xinetd.d`{: .filepath}.

![problem_description](/assets/img/pwnable/backdoor.png)
_"backdoor": What hackers leave for later, after gaining root privileges_

### Background Knowledge
"xinetd" (Extended Internet Service Daemon) listens to network requests, and executes right service for the request. 

So, the `/etc/xinetd.d`{: .filepath} directory has settings for individual services, and items not set here follow the global setting of `/etc/xinetd.conf`{: .filepath}.

## Exploit
I took a closer look at the directory. And there was the literal "backdoor" file :)

![exploit](/assets/img/pwnable/etc_xinetd.png)

Printing the content of backdoor, it says when `finger`{: .filepath} service is requested on TCP, it executes /home/level4/tmp/backdoor file with level5's privilege.

![exploit](/assets/img/pwnable/etc_xinetd2.png)

There was nothing in `tmp/`{: .filepath} directory, so I made one (`backdoor`{: .filepath} file).
```bash
#!/bin/bash

my-pass
```

I executed finger service based on finger man page, then the flag has come.

![exploit](/assets/img/pwnable/etc_xinetd3.png)