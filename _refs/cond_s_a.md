---
permalink: cond_s_a.html # url you want the page to be at
layout: refpage
title: "Conditional Signal Assignment"
title-short: "Cond. Signal Assign."
chart-left: "Concurrent Statement" # for the left side of the chart
chart-right: [Architecture] # for the right side of the chart
tags: [] # list of tags
---

<h3 class="text-hr"><span>Syntax</span></h3>

<!-- include the vhdl tag to highlight as vhdl -->
```vhdl
signal_name <= expression_1 when condition_1 else
               expression_2 when condition_2 else expression_3;
```

See LRM section 9.5.1

<h3 class="text-hr"><span>Rules and Examples</span></h3>

Each condition is a boolean expression:
```vhdl
architecture COND of BRANCH is
begin
    Z <= A when X > 5 else
         B when X < 5 else C;
end COND;
```

Conditions may overlap. The expression corresponding to the first "true" condition is assigned.
```vhdl
architecture COND of BRANCH is
begin
   Z <= A when X =  5 else
        B when X < 10 else C;
end COND;
```

There must be a final unconditional __else__ expression:
```vhdl
architecture COND of WRONG is
begin
    Z <= A when X > 5;  --illegal
end COND;
```

The expressions assigned may be delayed. Transport delay mode may also be specified.

Conditional signal assignments may be used to define __tri-state buffers__, using the __std_logic__ and __std_logic_vector__ type. Note the use of the aggregate form for a vector bus.
```vhdl
architecture COND of TRI_STATE is
    signal TRI_BIT: std_logic;
    signal TRI_BUS: std_logic_vector(0 to 7);
begin
    TRI_BIT <= BIT_1 when EN_1 = '1' else 'Z';
    TRI_BUS <= BUS_1 when EN_2 = '1' else (others => 'Z');
end COND;
```

<h3 class="text-hr"><span>Synthesis Issues</span></h3>

Conditional signal assignments are generally synthesizable.

A conditional signal assignment will usually result in combinational logic being generated. Assignment to 'Z' will normally generate tri-state drivers. Assignment to 'X' may not be supported.

If a signal is conditionally assigned to itself, latches may be inferred.

<h3 class="text-hr"><span>New in VHDL-93</span></h3>

In VHDL-93, any signal assigment statement may have an optinal label.

VHDL-93 defines an __unaffected__ keyword, which indicates a condition when a signal is not given a new assignment:
```vhdl
label: signal <= expression_1 when condition_1 else
                 expression_2 when condition_2 else unaffected;
```

The keywords __inertial__ and __reject__ may also be used in a conditional signal assignment.

A conditional signal assignment can be specified to run as a __postponed process__.
