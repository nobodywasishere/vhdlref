---
permalink: waits.html
layout: refpage
title: "Wait Statement"
used-in: [Process, Procedure]
tags: [statement - wait, wait, wait for, wait on, wait until, until, time, "'event", process - clocked, process - combinational]
parent: Sequential Statements
lrm:
    - 93: [8.1]
---

## Syntax

<!-- include the vhdl tag to highlight as vhdl -->
```vhdl
wait until condition;

wait on signal_list;

wait for time;

wait;
```

## Rules and Examples

The __wait until__ statement suspends a process until a change occurs on one or more of the signals in the statement and the condition is evaluated to be true. A rising edge on NET_DATA_VALID and three rising edges on CLK must occur for this process to cycle:
```vhdl
READ_NET: process
begin
    wait until NET_DATA_VALID = '1';
    NET_DATA_READ <= '1';
    wait until CLK='1';
    wait until CLK='1';
    NET_BUFFER <= NET_DATA_IN;
    wait until CLK='1';
    NET_DATA_READ <= '0';
end process READ_NET;
```

The __'event__ attribute in the following form of wait statement is in fact redundant, but is required by many synthesis tools:
```vhdl
WAIT_PROC: process
begin
    wait until CLK'event and CLK='1';
    Q1 <= D1;
end process;
```

The __wait on__ statement is equivalent to a sensitivity list. These processes will behave identically:
```vhdl
process (A, B)
begin
    -- sequential statements
end process;

process
begin
    -- identical sequential statements
    wait on A, B;
end process;
```

Wait for and wait are useful in behavioral models and test benches. Wait on it's own suspends a process indefinitely:
```vhdl
STIMULUS: process
begin
    EN_1   <= '0';
    EN_2   <= '1';
    wait for 10 ns;
    EN_1   <= '1';
    EN_2   <= '0';
    wait for 10 ns;
    EN_1 <= '0';
    wait for 10 ns;
    wait; -- end of test
end process STIMULUS;
```

The wait statement cannot be used:
- In a process with a sensitivity list
- In a procedure called from a process with a sensitivity list
- In a function
- In a procedure called from a function

A wait statement may have a label.

## Synthesis Issues

Most logic synthesis tools only support a single wait until (clock edge expression) statement in a __clocked process__.

Some tools support a single __wait on__ statement as an alternative to a sensitive list in a __combinational process__.

__Wait for__, unconditional wait, and wait statements in procedures are not supported.
