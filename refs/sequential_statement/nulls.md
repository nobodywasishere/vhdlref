---
permalink: nulls.html
layout: refpage
title: "Null Statement"
chart-left: "Sequential Statement"
chart-right: [Process, Function, Procedure]
parent: Sequential Statements
lrm:
    - 93: [8.12]
---



## Syntax

<!-- include the vhdl tag to highlight as vhdl -->
```vhdl
null;
```

## Rules and Examples

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

The __null__ may have an optional label:
```vhdl
label null;
```

## Synthesis Issues

The __null__ statement is supported by synthesis tools.

Note: using a __null__ statement in a "combinational process" can result in latches being inferred, unless all signals driven by the process are given unconditional default assignments.
