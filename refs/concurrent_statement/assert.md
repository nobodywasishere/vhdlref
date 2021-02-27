---
permalink: assert.html
layout: refpage
title: "Assert"
description: "The assert statement tests a boolean condition. If this returns false, it outputs a message containing the report string to the simulator screen."
chart-left: "Concurrent Statement"
chart-right: [Entity,Architecture,Process,Function,Procedure]
tags: [assert, severity level, concurrent, unconditional, report, statement - concurrent, message - unconditional, process, process - postponed]
parent: Concurrent Statements
parent: Sequential Statements
lrm:
    - 93: [8.2, 9.4]
---


## Syntax

```vhdl
assert condition report string severity severity_level;
```

```vhdl
label: assert condition report string severity severity_level;
```

## Rules and Examples

The assert statement tests a boolean condition. If this returns false, it outputs a message containing the report string to the simulator screen:
```vhdl
assert (J /= C) report "J = C" severity note;
```

The severity level may be defined as `note`, `warning`, `error`, or `failure`. Failure normally aborts the simulation.
```vhdl
assert (not OVERFLOW) report "Accumulator overflowed" severity failure;
```

If the message clause is ommited, a default message is output. The severity level and the name of the design unit containing the relevant assert statement may also be output.

If the severity clause is ommited, the default level is `error`.

A __concurrent__ statement monitors the boolean condition continuously.

An __unconditional__ message can be output by using the literal `false`:
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

`Report` can be used on it's own as a sequential statement, giving the same functionality as `assert false`, except that the default severity is `note`.

```vhdl
MSG1: report "Starting test sequence" severity note;
```

A concurrent `assert` statement may be run as a postponed [__process__]({{ site.baseurl}}/'process.html').

## Synthesis Issues

Assert statements are ignored by logic synthesis tools.
