---
permalink: var_dec.html # url you want the page to be at
layout: refpage
title: "Variable Declaration"
chart-left: "Declaration" # for the left side of the chart
chart-right: [Process, Procedure, Function] # for the right side of the chart
tags: [] # list of tags
---

<h3 class="text-hr"><span>Syntax</span></h3>

<!-- include the vhdl tag to highlight as vhdl -->
```vhdl
variable variable_name : type;
```

```vhdl
variable variable_name : type := initial_value;
```

See LRM section 4.3.1.3

<h3 class="text-hr"><span>Rules and Examples</span></h3>

```vhdl
variable HEIGHT : integer := 8;
variable COND : boolean := true;
variable IN_STRING : string(1 to 80);
variable M,N : bit := '1';
variable I : integer range 0 to 3;
variable MAKE_FRAME_STATE : T_MAKE_FRAME_STATE := RCV_HIGH;
```

A Variable may be given an explicit initial value when it is declared. If a variable is not given an explicit value, it's default value will be the leftmost value (__'left__) of its declared type.
```vhdl
variable I : integer range 0 to 3; -- initial value of I is 0
variable X : std_ulogic; -- initial value of X is 'U'
```

Variables within subprograms (functions and procedures) are initialized each time the subprogram is called:
```vhdl
function PARITY (
    X : std_ulogic_vector
) return std_ulogic is
    variable TMP : std_ulogic := '0';
begin
    for J in X'range loop
        TMP := TMP xor X(J);
    end loop; -- no need to initialise TMP
    return TMP;
end PARITY;
```

Variables in processes except for __for loop__ variables receive their initial values at the start of the simulation time (time = 0 ns). In this example we need to reset TMP to '0' each time the process is activated:
```vhdl
process (A)
    variable TMP : std_ulogic := '0';
begin
    TMP := '0';

    for I in A'low to A'high loop
        TMP := TMP xor A(I);
    end loop;

    ODD <= TMP;
end process;
```

<h3 class="text-hr"><span>Synthesis Issues</span></h3>

Variables are supported for synthesis, providing they are of a type acceptable to the logic synthesis tool.

In a __clocked process__, each variable which has its value read before it has had an assignment to it will be synthesized as the output of a register.

In a __combinational process__, reading a variable before it has had an assignment may cause a latch to be synthesized.

Variables declared in a subprogram are synthesized as combinational logic.

<h3 class="text-hr"><span>New in VHDL-93</span></h3>

In VHDL-93, __shared variables__ may be declared within an architecture, block, generate statement, or package:
```vhdl
shared variable variable_name : type;
```

Shared variables may be accessed by more than one process. However, the language does not define what happens if two or more processes make conflicting accesses to a shared variable at the same time. 
