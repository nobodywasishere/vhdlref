---
permalink: var_ass.html
layout: refpage
title: "Variable Assignment"
chart-left: "Sequential Statement"
chart-right: [Process, Procedure, Function]
tags: []
parent: Sequential Statements
lrm:
    - 93: [8.4]
---

## Syntax

<!-- include the vhdl tag to highlight as vhdl -->
```vhdl
variable_name := expression;
```

## Rules and Examples

Assignments may be made from signals to variables and vice-versa, providing the types match:
```vhdl
process (A, B, C, SEL)
    variable X : integer range 0 to 7;
begin
    if SEL = '1' then
        X := B;
    else
        X := C;
    end if;

    Z <= A + X;
end process;
```

A variable assignment takes effect immediately:
```vhdl
architecture EX1 of V is
    signal A, B, Y, Z : integer;
begin
    process (A, B)
        variable M, N : integer;
    begin
        M := A;
        N := B;
        Z <= M + N;
        M := 2 * A;
        Y <= M + N;
    end process;
end EX1;
```

An equivalent architecture with concurrent signal assignments:
```vhdl
architecture EX2 of V is
    signal A, B, Y, Z : integer;
begin
     Z <= A + B;
     Y <= 2*A + B;
end EX2;
```

A variable assignment may not be given a __delay__.

A variable in a process can act as a register if it is read before it has been written to, since it retains its value between successive process activations.
```vhdl
process (CLK)
    variable Q : std_ulogic;
begin
    if CLK'event and CLK='1' then
        PULSE <= D and not(Q);
        Q := D;
        -- PULSE and Q act as registers
    end if;
end process;
```

A variable assignment may have a label:
```vhdl
label: variable_name := expression;
```

<!-- VHDL supports __shared variables__ which may be accessed by more than one process. However, the language does not define what happens if two or more processes make conflicting accesses to a shared variable at the same time. -->

## Synthesis Issues

Variable assignments are generally synthesizable, providing they use types and operators acceptable to the synthesis tool.

In a "clocked process", each variable which has its value read before it has had an assignment to it will be synthesized as the output of a register.

In a "combinational process", reading a variable before it has had an assignment may cause a latch to be synthesized.

Variables declared in a subprogram are synthesized as combinational logic.
