---
permalink: library.html
layout: refpage
title: "Library Clause"
chart-left: "Context Clause"
chart-right: [Entity, Package, Configuration]
tags: []
parent: Context Clause
lrm:
    - 93: [11.2]
---

## Syntax

<!-- include the vhdl tag to highlight as vhdl -->
```vhdl
library library_name, another_library_name;
```

## Rules and Examples

A library clause must appear before the start of a design unit:
```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.all;
entity WIDGET is

-- etc.

end WIDGET;
```

The library clause is valid only for the design unit immediately following, and any of its secondary units.

Each simulator provides a way to map the library logical name to the library's physical position in the host environment. This is typical done through shell variables, or file system links.

The libraries work and std do not have to be declared. Each design unit is implicitly preceded by the following:
```vhdl
library WORK;
library STD;
use STD.STANDARD.all;
```


## Synthesis Issues

The library clause is usually ignored by synthesis tools.
