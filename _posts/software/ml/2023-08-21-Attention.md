---
title: Attention, Is Explanation? or Not?
date: 2023-08-21 00:00:00 +0900
categories: [Software, Machine Learning]
tags: [project, paper_review]
author: soom1017
---

I'm currently implementing conversation system with NLP. Since it is kind of task-oriented dialogue sytem, I tried Dialogue State Tracking (DST) model, but the learning did not work well due to data quantity - almost one-shot learning. As an alternative, I thought reversing "attention" (used by LLM) would represent the important phrases in a conversation. Could it be possible to use the attention as explanation?

## Attention is not Explanation
Authors in the paper ["Attention is not Explanation"](https://arxiv.org/abs/1902.10186) say it's not possible.

## Attention as Explanation