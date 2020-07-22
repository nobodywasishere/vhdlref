---
permalink: process.html # url you want the page to be at
layout: refpage
title: "Process"
chart-left: "Concurrent Statement" # for the left side of the chart
chart-right: [Architecture] # for the right side of the chart
tags: [] # list of tags
---

<h3 class="text-hr"><span>Syntax</span></h3>

<!-- include the vhdl tag to highlight as vhdl -->
```vhdl
optional_label: process (
    -- optional sensitivity list
)
	-- declarations
begin
	-- sequential statements
end process optional_label;
```

See LRM section 9.2

<h3 class="text-hr"><span>Rules and Examples</span></h3>

The sensitivity list is a list of signals. A change in value on one or more of these signals, causes the process to be activated:
```vhdl
process (ALARM_TIME, CURRENT_TIME)
begin
    if (ALARM_TIME = CURRENT_TIME) then
        SOUND_ALARM <= '1';
    else
        SOUND_ALARM <= '0';
    end if;
end process;
```

Alternatively, process activation and suspension may be controlled via the wait statement:
```vhdl
process
begin
    if (ALARM_TIME = CURRENT_TIME) then
        SOUND_ALARM <= '1';
    else
        SOUND_ALARM <= '0';
    end if;
    wait on ALARM_TIME, CURRENT_TIME;
end process;
```

A process cannot have both a sensitivity list and wait statements. A process may contain any sequential statement.

<h3 class="text-hr"><span>Synthesis Issues</span></h3>

Processes are synthesizable, provided they match certain typical forms, some of which are shown below.

A "clocked process" with either a wait statement or sensitivity list. For such a process, registers are inferred on all signals which have assignments to them:
```vhdl
WAIT_PROC: process
begin
    wait until CLK'event and CLK='1';
    Q1 <= D1;
end process;

SENSE_PROC: process (CLK)
begin
    if CLK'event and CLK='1' then
        Q2 <= D2;
    end if;
end process;
```

A "combinational process" must have a sensitivity list containing all the signals which it reads (inputs), and must always update the signals which it assigns (outputs):
```vhdl
process (A, B, SEL)
begin
    Z <= B;
    if (SEL = '1') then
        Z <= A;
    end if;
end process;
```

<h3 class="text-hr"><span>New in VHDL-93</span></h3>

In VHDL-93, the keyword __process__ (or the sensitivity list, if there is one) may be followed by the keyword __is__ for clarity and consistency.

In VHDL-93, a postponed process may be defined. Such a process runs when all normal processes have completed at a particular point in simulated time. Postponed processes cannot schedule any further zero-delay events. Their main use is to perform timing or functional checks, based on the "steady-state" values of signals.
