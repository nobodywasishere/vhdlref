---
permalink: names.html
layout: refpage
title: "Names"
chart-left: "Identifier"
chart-right: [Entity, Architecture, Package, Package Body, Configuration]
parent: Expressions
lrm:
    - 93: [13.3]
---

## Syntax

See reference manual.

## Rules and Examples



__Names__ (or identifiers) may consist of letters, numbers and underscore:
```vhdl
architecture RTL of UNIT_34 is
signal SOUND_ALARM : std_ulogic;
```

Case is not sensitive, so the following are all equivalent:
```vhdl
An_Example_Name
AN_EXAMPLE_NAME
an_example_name
```

Names must start with a letter:
```vhdl
signal 16_BIT_BUS : integer;   -- illegal
signal _BUS_16_BIT_ : integer; -- illegal
signal BUS_16_BIT : integer;   -- OK
```

__Names__ may be of arbitrary length.

None of the following VHDL keywords may be reused as a name:
- signal
- bus
- component
- wait
- group
- impure
- inertial
- literal
- postponed
- pure
- rol
- ror
- shared
- sla
- sll
- sra
- srl
- unaffected
- xnor

VHDL supports extended identifiers. An extended identifier is delimited by backslashes (`\\`), and may use any of the printing characters from the VHDL extended character set.

This allows the use of names which would otherwise be illegal in VHDL (e.g.where compatibility with a preexisting design database is required). Examples:
```vhdl
\Buffer\ -- would otherwise be a keyword
\Buff\
\BUFF\   -- these are now two distinct identifiers
\BUS_$8\ -- contains otherwise illegal character
```

## Synthesis Issues

Legal __names__ (identifiers) are supported for synthesis, but long __names__ may be truncated in some tools, or when using certain output netlist formats.
