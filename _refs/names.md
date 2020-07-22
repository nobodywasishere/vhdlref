---
permalink: names.html # url you want the page to be at
layout: refpage
title: "Name"
chart-left: "Identifier" # for the left side of the chart
chart-right: [Entity, Architecture, Package, Package Body, Configuration] # for the right side of the chart
---

<h3 class="text-hr"><span>Syntax</span></h3>

See LRM section 13.3

<h3 class="text-hr"><span>Rules and Examples</span></h3>



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

None of the VHDL keywords (i.e. __signal__, __bus__, __component__, __wait__, etc.) may be reused as a name.

<h3 class="text-hr"><span>Synthesis Issues</span></h3>

Legal __names__ (identifiers) are supported for synthesis, but long __names__ may be truncated in some tools, or when using certain output netlist formats.

<h3 class="text-hr"><span>New in VHDL-93</span></h3>

VHDL-93 supports extended identifiers. An extended identifier is delimited be backslashes(\), and may use any of the printing characters from the VHDL-93 extended character set.

This allows the use of names which would otherwise be illegal in VHDL (e.g.where compatibility with a preexisting design database is required). Examples:
```vhdl
\Buffer\ -- would otherwise be a keyword
\Buff\
\BUFF\   -- these are now two distinct identifiers
\BUS_$8\ -- contains otherwise illegal character
```

VHDL-93 has introduced the following new language keywords, which may not be reused as identifiers:  __group, impure, inertial, literal, postponed, pure, rol, ror, shared, sla, sll, sra, srl, unaffected, xnor__. These keywords should also be avoided in VHDL-87 models to ensure upward-compatibility.
