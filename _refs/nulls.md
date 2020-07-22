---
permalink: nulls.html # url you want the page to be at
layout: refpage
title: "Null Statement"
chart-left: "Sequential Statement" # for the left side of the chart
chart-right: [Process, Function, Procedure] # for the right side of the chart
---



<h3 class="text-hr"><span>Syntax</span></h3>

<!-- include the vhdl tag to highlight as vhdl -->
```vhdl
null;
```

See LRM section 8.12

<h3 class="text-hr"><span>Rules and Examples</span></h3>

The null statement performs no action. It is usually used with the case statement to indicate that under certain conditions, no action is required.
```vhdl
case ENCRYPTION is
    when "00" =>
        CPU_DATA_TMP := (B & A) - OPERAND;
    when "01" =>
        CPU_DATA_TMP := (B & A) + OPERAND;
    when "10" =>
        CPU_DATA_TMP := (A & B) - OPERAND;
    when "11" =>
        CPU_DATA_TMP := (A & B) + OPERAND;
    when others =>
        null;
end case;
```

<h3 class="text-hr"><span>Synthesis Issues</span></h3>

The __null__ statement is supported by synthesis tools.

Note: using a __null__ statement in a "combinational process" can result in latches being inferred, unless all signals driven by the process are given unconditional default assignments.

<h3 class="text-hr"><span>New in VHDL-93</span></h3>

In VHDL-93, the __null__ may have an optional label:
```vhdl
label null;
```
