---
title: Reversing &#124; Dreamhack - Patch
date: 2022-02-10 00:00:00 +0900
categories: [Software, Security]
tags: [writeups, problem_solving]
author: soom1017
image:
    path: /assets/img/reversing/patch-exec.png
---

## Intro
As the name of the problem suggests, I have to patch a program to remove the line-drawing code, so that flag is not obscured. Since it's a GUI program made with WinAPI, first find WinMain and decompile it, as follows.

![reversing_capture](/assets/img/reversing/patch.png){: .normal }

Before creating window with "CreateWindowExW", it registers drawing information with the function "RegisterClassExW". 

Therefore, I would look at `v11`, which is argument of `RegisterClassExW`, and especially `sub_1400032F0` logic that is assigned to `v11.lpfWndProc`.

> lpfnWndProc: Defines most of window's behavior

## Exploit

![reversing_capture](/assets/img/reversing/patch2.png){: .normal }

It seems the block from `BeginPaint` to `EndPaint` (in case 0xFu) is what I want. In the function `sub_140002C40`, `sub_140002B80` is repeatedly called with different parameter values, to draw line-by-line. 

So I debugged with breakpoint at `sub_140002B80`, and observed lines in the window.

I found the painting function with the shortcut `g`, clicked on Edit > Patch Program > Assemble, changed the function's first instruction to `ret`, and got the flag.

![solved](/assets/img/reversing/patch3.png){: .normal }