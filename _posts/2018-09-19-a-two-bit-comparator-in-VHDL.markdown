---
layout: post
title: 'A two bit comparator in VHDL'
author: marcel
category: projects
published: true
date: 2018-09-19 11:00:30 +03:00
---

## Introduction
This is a VHDL design of a digital **two-bit comparator**. An output is shown depending on whether the comparation is greater, equal or less than the other.

## Workflow
Three different methods to compare two bits have been implemented: its boolean equations, VHDL's "when .. else" statement and VHDL's "with .. select" statement. The **simulation**, the **RTL analysis** and the **synthesis scheme** are shown as well.

## Contents
```
1 Introduction . . . . . . . . . . . . . . . . . 1
1.1 Aim  . . . . . . . . . . . . . . . . . . . . 1
1.2 Background . . . . . . . . . . . . . . . . . 1
2 Workflow . . . . . . . . . . . . . . . . . . . 3
2.1 Top level. . . . . . . . . . . . . . . . . . 3
2.1.1 Libraries. . . . . . . . . . . . . . . . . 3
2.1.2 Entity . . . . . . . . . . . . . . . . . . 3
2.1.3 Architecture . . . . . . . . . . . . . . . 4
2.1.3.1 Method 1: boolean equations  . . . . . . 4
2.1.3.2 Method 2: "when .. else" statement . . . 4
2.1.3.3 Method 3: "with .. select" statement . . 5
2.2 Testbench  . . . . . . . . . . . . . . . . . 5
3 Results and conclusion . . . . . . . . . . . . 7
3.1 Simulation . . . . . . . . . . . . . . . . . 7
3.2 RTL analysis . . . . . . . . . . . . . . . . 7
3.3 Synthesis analysis . . . . . . . . . . . . . 8
4 Conclusion . . . . . . . . . . . . . . . . . .10
References . . . . . . . . . . . . . . . . . . .11
```

## Check out the document
[Open PDF](https://1drv.ms/b/s!AtguJR4tix_G42S3zPHYfIO35fwR){: .btn}
