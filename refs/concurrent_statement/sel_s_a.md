---
permalink: sel_s_a.html
layout: refpage
title: "Selected Signal Assignment"
used-in: [Architecture]
tags: []
parent: Concurrent Statements
lrm:
    - 93: [9.5.2]
---

## Syntax

<!-- include the vhdl tag to highlight as vhdl -->
```vhdl
with expression select
    signal_name <= expression_1 when choice_1,
                   expression_2 when choice_2;
```

## Rules and Examples

The rules are the same as for the __case statement__, i.e. all possible choices must be included unless the __others__ clause is used as the last choice:
```vhdl
architecture SEL of BRANCH is
begin
    with CMD select
        Z <= B when "00",
             C when "01",
             A when others;
end SEL;
```

A range or a selection may be specified as a choice:
```vhdl
with INT_A select
    Z <= A when 0,
         B when 1 to 3,
         C when 4|6|8,
         D when others;
```

As with the case statement, choices may not overlap:
```vhdl
with INT_A select
    Z <= A  when 0,
         B  when 1 to 3,
         C  when 2|6|8,   --illegal
        'X' when others;
```

As with the case statement, there is no implied priority to the choices:
```vhdl
architecture COND of BYTE is
    type BYTE_POS is (LOWER, UPPER);
    signal SEL: BYTE_POS;
begin
    with SEL select
        OBUS <= REG(0 to 7)  when LOWER,
                REG(8 to 15) when UPPER;
end COND;
```

The expressions assigned may be delayed. Transport delay mode may also be specified.

Any signal assignment may have an optional label.

The __unaffected__ keyword indicates a choice where the signal is not given a new assignment. This is roughly equivalent to the use of the null statement within case:
```vhdl
label: with expression select
    signal <= expression_1 when choice_1 ,
              expression_2 when choice_2 ,
                unaffected when others;
```

The keywords __inertial__ and __reject__ may also be used in a selected signal assignment.

A selected signal assignment can be specified to run as a __postponed process__.

## Synthesis Issues

Selected signal assignments are generally synthesizable.

A selected signal assignment will usually result in combinational logic being generated. Assignments to 'Z' will normally generate tri-state drivers. Assignment to 'X' may not be supported.

If a signal is conditionally assigned to itself, latches may be inferred.
