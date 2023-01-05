---
title: "String Formatting"
date: 2023-01-04T22:47:44-05:00
draft: false
tags: ["go"]
---

Go offers several printing **verbs** designed to format general Go values.

| Verb | Usage | Example |
|----|----|----|
| %v | struct | {1 2} |
| %+v | include struct name | {x:1 y:2} |
| %#v | prints like it would appear in the source code | main.point{x:1, y:2} |
| %T | print type of a value | main.point |
| %t | boolean | true |
| %d | integer | 123 |
| %6d | specify the width of the number |       12 |
| %b | binary representation | 1110 |
| %c | print character corresponding to integer | ! |
| %x | provides hex encoding | 1c8 |
| %f | floats | 78.9000 |
| %-6.2f | specify the width of the number and decimal precision, left justify with - flag | 1.20      |
| %e | float scientific notation | 1.234000e+08 |
| %E | float scientific notation | 1.234000E+08 |
| %s | string | a string buh |
| %q | double quote string | "\"string\"" |
| %p | pointer | 0xc0000ba000 |