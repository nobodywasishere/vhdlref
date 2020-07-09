---
permalink: blocks.html # url you want the page to be at
layout: page
title: "Block Statement"
description: "Template Page."
chart-left: "Concurrent Statement" # for the left side of the chart
chart-right: [Architecture] # for the right side of the chart
tags: [guard condition, guarded block, guarded signal assignments, guarded signals, bus, register, unguarded block, block]
---

{% include chart.html %}

<h3 class="text-hr"><span>Syntax</span></h3>

```vhdl
label: block (optional_guard_condition)
    declarations
begin
    concurrent statements
end block label;
```

See LRM section 9.1

<h3 class="text-hr"><span>Rules and Examples</span></h3>

A label is compulsory:
```vhdl
CONTROL_LOGIC: block
begin
    U1: CONTROLLER_A
        port map (CLK, X, Y, Z);
    U2: CONTROLLER_A
        port map (CLK, A, B, C);
end block CONTROL_LOGIC;

DATA_PATH: block
begin
    U3: DATAPATH_A port map
        (BUS_A, BUS_B, BUS_C, Z);
    U4: DATAPATH_B port map
        (BUS_A, BUS_C, BUS_D, C);
end block DATA_PATH;
```

Without a guard condition, a block is a group of concurrent statements within an architecture. It may have local signals, constants, etc. declared.

Blocks may contain further blocks, implying a form of hierarchy within a single architecture.

A Block may contain any of the declarations possible for an architecture. Items declared within a block are only visible inside it.

IF an optional guard condition is included, the block becomes a __guarded block__. The __guard condition__ must return a boolean value, and controls __guarded signal assignments__ within the block. If the guard condition evaluates to false, the drive to any __guarded signals__ from the block is "switched off". Such signals must be declared to be guarded signals of a resolved type. Guarded signals can be declared by adding the words __bus__ or __register__ after the name of the type of the signal. The difference between bus and register signals is that if all drivers to a bus signal are "switched off", it requires a resolution function to provide a value for the signal but a register signal retains its last driven value after all drivers to it have been switched off.
```vhdl
architecture BLKS of TRISTATE is
    signal INT: std_logic bus;
begin

    DRIVER_1: block (EN = '1')
    begin
        INT <= guarded DATA_1;
    end block DRIVER_1;

end BLKS;
```
<h3 class="text-hr"><span>Synthesis Issues</span></h3>

Unguarded __block__ statements are usually ignored by logic synthesis tools (i.e. all blocks within an architecture are "flattened").
__Guarded block__ statements are __not__ usually supported for synthesis.

Sequential (i.e. flip-flop and register) behavior can be modeled using guarded blocks, but again for synthesis and readability it is better described using "clocked" processes.

<h3 class="text-hr"><span>New in VHDL-93</span></h3>

In VHDL-93 the keyword __block__ (or the guard condition, if there is one), may be followed by the keyword __is__, for consistancy.:
```vhdl
label: block (optional guard_condition) is
    -- etc
```
