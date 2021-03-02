---
permalink: literals.html
layout: refpage
title: "Literals"
used-in: [Expression]
parent: Expressions
lrm:
    - 93: [7.3.1, 13.4, 3.1.1, 3.1.3]
---

## Syntax

See reference manual.

## Rules and Examples

Numeric literals with a decimal point are real, those without are integer:
```vhdl
constant FREEZE : integer := 32;
constant TEMP : real := 32.0;
```

Numeric literals may be expressed in any base from 2 to 16. They may also be broken up using underscore, for clarity.
```vhdl
A_INT <= 16#FF#;
B_INT <= 2#1010_1010#;
MONEY := 1_000_000.0;
```

Real numbers may be expressed in exponential form:
```vhdl
FACTOR := 2.2E-6;
```

Literals of type time (and other physical types) must have units. The units should be preceded by a space, although some tools may not require this:
```vhdl
constant DEL1 : time := 10 ns;
constant DEL2 : time := 2.27 us;
```

Literals of enumerated types may either be characters (as for bit and std_logic), or identifiers:
```vhdl
type MY_LOGIC is ('X','0','1','Z');
type T_STATE is (IDLE, READ, END_CYC);
signal CLK : MY_LOGIC := '0';
signal STATE : T_STATE := IDLE;
```

## Synthesis Issues

Logic synthesis tools may not support named association fully. Also, record assignments using aggregates may not be supported.
