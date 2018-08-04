---
layout: post
title: 'A digital chronometer design in VHDL'
categories: projects
author: marcel
published: true
date: 2018-05-20 16:01:10 -04:00
---

## Abstract
All along the semester, we have been working with Digital Systems subject as one of the main courses of the Electronics Engineering bachelor’s degree. Most part of the subject consist in practical cases where students, in groups of two or three, had to develop the projects based on hardware description languages (VHDL) and Field Programmable Gate Arrays (FPGA).
This is the report of one of the practices we worked on so we are able to get recognized the competence in a foreign language.

## Introduction
This is the fifth practice of the subject. It consists in the development of a digital chronometer. Given the instructions, we had to write and implement the hardware description of a chronometer that can count up to 1 hour with a resolution of 10^-2 seconds. The source of the clock is the internal reference of the Basys 3 (100MHz). The actual value of counting had to be shown on the four 7-segment displays embedded in the board. Due to the lack of displays, we should be able to see the counting in two different modes (MM : SS and SS : CS) moving one of the switches of the board. One of the buttons is for the reset, another is to indicate START/STOP, another one is to store to a record memory the value of the counter at the moment we require it, and the other button is to show the recorded value while we push it down.

## Contents
```
| Ch.   | Title                                  |  p |
|-------|----------------------------------------|---:|
| 1     | Introduction                           |  1 |
| 1.1   | Objectives                             |  1 |
| 1.2   | Abstract                               |  1 |
| 2     | Development of the digital chronometer |  2 |
| 2.1   | Top level                              |  2 |
| 2.2   | Components                             |  8 |
| 2.2.1 | Clock divider                          |  8 |
| 2.2.2 | Units division                         |  9 |
| 2.2.3 | Edge detection                         |  9 |
| 2.2.4 | Toggle                                 |  9 |
| 3     | Results and conclusion                 | 11 |
```

###### Marcel Cases

