---
permalink: conc_s_a.html # url you want the page to be at
layout: refpage
title: "Concurrent Signal Assignment"
chart-left: "Concurrent Statement" # for the left side of the chart
chart-right: [Architecture] # for the right side of the chart
tags: [] # list of tags
---

<h3 class="text-hr"><span>Syntax</span></h3>

<!-- include the vhdl tag to highlight as vhdl -->
```vhdl
signal_name <= expression;
```

```vhdl
signal_name <= expression after delay;
```

See LRM section 9.5

<h3 class="text-hr"><span>Rules and Examples</span></h3>

A concurrent signal assignment assigns a new value to the target signal whenever any of the signals on the right hand side change:
```vhdl
architecture CONC of HA is
begin
    SUM   <= A xor B;
    CARRY <= A and B;
end CONC;
```

Concurrent assignments have an "equivalent process". This is the equivalent process for the concurrent statements above.
```vhdl
architecture SEQ of HA is
begin
    process (A, B)
    begin
        SUM   <= A xor B;
        CARRY <= A and B;
    end process;
end SEQ;
```

A signal assignment may have a delay specified:
```vhdl
architecture DELAYS of X is
    constant PERIOD : time := 10 ns;
begin
    SUM   <= A xor B after 5 ns;
    CARRY <= A and B after 3 ns;
    CLK   <= not CLK after PERIOD/2;
end DELAYS;
```

The default delay model is __inertial__. This means that "pulses" shorter than the delay time are not propagated. The alternative is __transport__ delay, which propagates all transitions:
```vhdl
architecture TRANS of BUFF is
    constant DELAY : time := 10 ns;
begin
    O_PIN <= transport I_PIN after DELAY;
end TRANS;
```

Multiple concurrent assignments to the same signal imply multiple drivers. A signal which is the target of multiple concurrent signal assignments must be of a resolved type, e.g. std_logic, std_logic_vector.

For __guarded assignments__, see __blocks__.

<h3 class="text-hr"><span>Synthesis Issues</span></h3>

Concurrent signal assignments are generally synthesizable, providing they use types and operators acceptable to the synthesis tool.

A signal assigned with a concurrent statement will be inferred as combinational logic.

Guarded assignments are not usually supported, and delays are ignored.

<h3 class="text-hr"><span>New in VHDL-93</span></h3>

In VHDL-93, any signal assignment statement may have an optional label:
```vhdl
label: signal_name <= expression;
```

A delayed signal assignment with inertial delay may be explicitly preceded by the keyword __inertial__. It may also have a __reject time__ specified. This is the minimum "pulse width" to be propagated, if different from the inertial delay:
```vhdl
OUTPUT <= reject 2 ns inertial not (INPUT) after 10 ns;
```

A concurrent signal assignment can be specified to run as a postponed process (see __process__).
