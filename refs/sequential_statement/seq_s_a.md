---
permalink: seq_s_a.html
layout: refpage
title: "Sequential Signal Assignment"
chart-left: "Sequential Statement"
chart-right: [Process, Procedure]
tags: []
parent: Sequential Statements
lrm:
    - 93: [8.3]
---

## Syntax

<!-- include the vhdl tag to highlight as vhdl -->
```vhdl
signal_name <= expression;
```

```vhdl
signal_name <= expression after delay;
```

## Rules and Examples

A sequential signal assignment takes effect only when the process suspends. If there is more than one assignment to the same signal before suspension, the last one executed takes effect:
```vhdl
process (A, B, SEL)
begin
    Z <= B;
    if SEL='1' then
        Z <= A;
    end if;
end process;
```

An equivalent process:
```vhdl
process (A, B, SEL)
begin
    if SEL='1' then
        Z <= A;
    else
        Z <= B;
    end if;
end process;
```

In this architecture, the signals Y and Z will both get the same value (2*A + B) because even though two assignments to the signal M are executed, the first will always be superseded by the second
```vhdl
architecture EX1 of V is
    signal A, B, M, N, Y, Z : integer;
begin
    process (A, B, M, N)
    begin
        M <= A;
        N <= B;
        Z <= M + N;
        M <= 2 * A;
        Y <= M + N;
    end process;
end EX1;
```

If a signal which has assignments to it within a process is also in the sensitivity list, it may cause the process to be reactivated.

A sequential signal assignment may have a delay:
```vhdl
process (A, B)
begin
    SUM   <= A xor B after 1.7 ns;
    CARRY <= A and B after 1.2 ns;
end process;
```

The rules about what happens when a delayed signal assignment is subsequently overridden are complex: see the reference manual.
 <!-- section 8.3.1 or "A VHDL Primer" by Jayaram Bhasker, section 4.14. -->

A delayed sequential signal assignment does not suspend the process or procedure for the time specified. The assignment is scheduled to occur after the specified time, and any further sequential statements are executed immediately.

Any signal assignment statement may have an optional label:
```vhdl
label: signal_name <= expression;
```

A delayed signal assignment with inertial delay may be explicitly preceded by the keyword __inertial__. It may also have a reject time specified. This is the minimum "pulse width" to be propagated, if different from the inertial delay:
```vhdl
output <= reject 2 ns inertial input after 10 ns;
```

## Synthesis Issues

Sequential signal assignments are generally synthesizable, providing they use types and operators acceptable to the synthesis tool. Delays are usually ignored.

All signals with assignments to them within a "clocked process" will become the outputs of registers in the synthesized design.

Signals driven by a "combinational process" will be inferred as the outputs of combinational logic but a signal which is assigned only under certain conditions may infer a latch. Assignment to 'Z' will normally generate tri-state drivers. assignment to 'X' may not be supported.
