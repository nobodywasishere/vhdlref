---
permalink: assert.html # url you want the page to be at
layout: page
title: "Assert"
description: "The assert statement tests a boolean condition. If this returns false, it outputs a message containing the report string to the simulator screen."
chart-left: "Concurrent Statement" # for the left side of the chart
chart-right: [Entity,Architecture] # for the right side of the chart
chart2-left: "Sequential Statement" # for the left side of the chart
chart2-right: [Process,Function,Procedure] # for the right side of the chart
tags: [assert, note, warning, error, concurrent, unconditional, false, report]
---

{% include chart.html %}

<h3 class="text-hr"><span>Syntax</span></h3>

```vhdl
assert condition report string severity severity_level;
```

See LRM sections 8.2 and 9.4

<h3 class="text-hr"><span>Rules and Examples</span></h3>

The assert statement tests a boolean condition. If this returns false, it outputs a message containing the report string to the simulator screen:
```vhdl
assert (J /= C) report "J = C" severity note;
```

The severity level may be defined as __note__, __warning__, __error__, or __failure__. Failure normally aborts the simulation.
```vhdl
assert (not OVERFLOW) report "Accumulator overflowed" severity failure;
```

If the message clause is ommited, a default message is output. The severity level and the name of the design unit containing the relevant assert statement may also be output.

If the severity clause is ommited, the default level is __error__.

A __concurrent__ statement monitors the boolean condition continuously.

An __unconditional__ message can be output by using the literal __false__:
```vhdl
procedure PUT
    (signal STACK  : inout T_STACK;
    signal POINTER : inout T_POINT;
    signal ITEM    : in    T_DATA) is
begin
    if (POINTER < 5) then
        STACK(POINTER) <= ITEM;
        POINTER <= POINTER + 1;
    else
        assert false report "Stack overflow" severity error;
    end if;
end PUT;
```

As well as functional errors, timing errors can be reported via __assert__:
```vhdl
CHECK_SETUP: process (CLK, D)
begin
    if (CLK'event and CLK = '1') then
        assert D'stable(SETUP_TIME) report "Setup Violation..." severity warning;
    end if;
end process CHECK_SETUP;
```

<h3 class="text-hr"><span>Synthesis Issues</span></h3>

Assert statements are ignored by logic synthesis tools.

<h3 class="text-hr"><span>New in VHDL-93</span></h3>

In VHDL-93, the __assert__ statement may have an option label.

A concurrent __assert__ statement may be run as a postponed [__process__]({{'process.html' | baseurl }}).

VHDL-93 allows __report__ to be used on it's own as a sequential statement, giving the same functionality as __assert false__, except that the default severity is __note__.

```vhdl
MSG1: report "Starting test sequence" severity note;
```
