---
permalink: sig_dec.html
layout: refpage
title: "Signal Declaration"
chart-left: "Declaration"
chart-right: [Architecture]
tags: ["'left"]
parent: Declarations
lrm:
    - 93: [4.3.1.2]
---

## Syntax

<!-- include the vhdl tag to highlight as vhdl -->
```vhdl
signal signal_name : type;
```

```vhdl
signal signal_name : type := initial_value;
```

## Rules and Examples

```vhdl
signal SUM, CARRY1, CARRY2 : bit;
signal COUNT : integer range 0 to 15;
signal CLK, RESET : std_ulogic := '0';
signal ALARM_TIME : T_CLOCK_TIME := (1, 2, 0, 0);
signal CONDITION : boolean := false;
```

During elaboration, each signal is set to an initial value. If a signal is not given an explicit initial value, it will default to the leftmost value ('left) of its declared type:
```vhdl
signal I : integer range 0 to 3; -- I will initialise to 0
signal X : std_logic; -- X will initialise to 'U'
```

A signal which is driven by more than one process, concurrent statement, or component instance must be declared with a resolved type, i.e. std_logic or std_logic_vector:
```vhdl
architecture COND of TRI_STATE is
    signal TRI_BIT: std_logic;
begin
    TRI_BIT <= BIT_1 when EN_1 = '1' else 'Z';
    TRI_BIT <= BIT_2 when EN_2 = '1' else 'Z';
end COND;
```

Signals may not be declared in a processor subprogram (except as formal parameters).

Ports declared in an entity are accessible as signals within the associated architecture(s) and do not need to be redeclared.

A signal of a __resolved type__ may be declared as a __guarded resolved__ signal. This is required if all drivers to a signal may be turned off, through guarded assignments.

signal signal_name : resolved_type signal_kind;

The "signal kind" keyword may be __register__ or __bus__. Guarded resolved signals of kind __register__ retain their current value when drive is turned off, where signals of kind __bus__ rely on the resolution function to provide a "no-drive" value.

## Synthesis Issues

Signals are supported for synthesis, providing they are of a type acceptable to the logic synthesis tool.

The signal kinds __register__ and __bus__ are usually ignored.

Only certain resolved signal types are supported. Most tools recognize the __std_logic_1164__ types.
