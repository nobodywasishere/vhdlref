---
permalink: cases.html # url you want the page to be at
layout: page
title: "Case Statement"
description: "Case Statement."
chart-left: "Sequential Statement" # for the left side of the chart
chart-right: [Process, Function, Procedure] # for the right side of the chart
tags: [others, case, null]
---

{% include chart.html %}

<h3 class="text-hr"><span>Syntax</span></h3>

```vhdl
case expression is
    when choice =>
        sequential statements
    when choice =>
        sequential statements
end case;
```

See LRM section 8.7

<h3 class="text-hr"><span>Rules and Examples</span></h3>

All possible choices must be included, unless the __others__ clause is used as the last choice:
```vhdl
case SEL is
    when "01" =>   Z <=  A;
    when "10" =>   Z <=  B;
    when others => Z <= 'X';
end case;
```

A range or a selection may be specified as a choice:
```vhdl
case INT_A is
    when 0      =>  Z <=  A;
    when 1 to 3 =>  Z <=  B;
    when 4|6|8  =>  Z <=  C;
    when others =>  Z <= 'X';
end case;
```

Choices may not overlap:
```vhdl
case INT_A is
    when 0      =>  Z <=  A;
    when 1 to 3 =>  Z <=  B;
    when 2|6|8  =>  Z <=  C;   -- illegal
    when others =>  Z <= 'X';
end case;
```

A range may not be used with a vector type:
```vhdl
case VEC is
    when "000" to "010" =>  
        Z <= A;   -- illegal
    when "111"   =>  Z <= B;
    when others  =>  Z <= 'X';
end case;
```

See also the __null__ statement.

<h3 class="text-hr"><span>Synthesis Issues</span></h3>

The __case__ statement is generally synthesizable.

With repeated assignments to a target signal, it will synthesize to a large multiplexer with logic on the select inputs to evaluate the conditions for the different choices in the case statement branches. No "priority" will be inferred from the order of the branches

With multiple targets and embedded __if__ statements, the __case__ statement may be used to synthesize a general mapping function, e.g. next state and output generation for a finite state machine. For example:
```vhdl
case READ_CPU_STATE is
    when WAITING =>
        if CPU_DATA_VALID = '1' then
            CPU_DATA_READ  <= '1';
            READ_CPU_STATE <= DATA1;
        end if;
    when DATA1 =>
        -- etc.
end case;
```

<h3 class="text-hr"><span>New in VHDL-93</span></h3>

In VHDL-93, the __case__ statement may have an optional label:

```vhdl
label: case expression is
    -- etc.
end case label;
```
