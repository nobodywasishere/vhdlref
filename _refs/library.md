---
permalink: library.html # url you want the page to be at
layout: refpage
title: "Library Clause"
chart-left: "Context Clause" # for the left side of the chart
chart-right: [Entity, Package, Configuration] # for the right side of the chart
tags: [] # list of tags
---

<h3 class="text-hr"><span>Syntax</span></h3>

<!-- include the vhdl tag to highlight as vhdl -->
```vhdl
library library_name, another_library_name;
```

See LRM section 11.2

<h3 class="text-hr"><span>Rules and Examples</span></h3>

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


<h3 class="text-hr"><span>Synthesis Issues</span></h3>

The library clause is usually ignored by synthesis tools.

<h3 class="text-hr"><span>New in VHDL-93</span></h3>

The library clause has not changed in VHDL-93.
