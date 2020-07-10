---
permalink: template.html # url you want the page to be at
layout: refpage
title: "Template Page"
chart-left: "What it does" # for the left side of the chart
chart-right: [Where, It, Wants, To, Go] # for the right side of the chart
---



<h3 class="text-hr"><span>Syntax</span></h3>

<!-- include the vhdl tag to highlight as vhdl -->
```vhdl
(value_1, value_2, ...)
```

<h3 class="text-hr"><span>Rules and Examples</span></h3>

Aggregates are a grouping of values to form an array or record expression. The first form is called __positional association__, where the values are associated with elements from left to right:
```vhdl
signal Z_BUS : bit_vector (3 downto 0);
signal A_BIT, B_BIT, C_BIT, D_BIT : bit;

--

Z_BUS <= (A_BIT, B_BIT, C_BIT, D_BIT);
```

<h3 class="text-hr"><span>Synthesis Issues</span></h3>

Logic synthesis tools may not support named association fully. Also, record assignments using aggregates may not be supported.

<h3 class="text-hr"><span>New in VHDL-93</span></h3>

Aggregates have not changed in VHDL-93.
