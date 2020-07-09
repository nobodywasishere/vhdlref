---
permalink: aliasdec.html # url you want the page to be at
layout: page
title: "Alias Declaration"
description: "An alias is an alternative name for an existing object (signal, variable or constant). It does not define a new object."
chart-left: "Declaration" # for the left side of the chart
chart-right: [Entity,Package,Process,Architecture,Procedure,Function] # for the right side of the chart
tag: [alias]
---

{% include chart.html %}

<h3 class="text-hr"><span>Syntax</span></h3>

```vhdl
alias alias_name : alias_type is object_name;
```
See LRM section 4.3.4

<h3 class="text-hr"><span>Rules and Examples</span></h3>

An alias is an alternative name for an existing object (signal, variable or constant). It does not define a new object.
```vhdl
alias SIGN    : bit is DATA(31);
alias BYTE_ID : bit is NET_DATA_IN(7);
```

Aliases provide a useful "shorthand" for referencing complex slices etc.:
```vhdl
use work.BV_ARITH.all;

--

alias OPERAND : bit_vector(1 downto 0)
       is CPU_BUFFER(LOW) (4 downto 3);
alias A       : bit_vector(3 downto 0)
       is CPU_BUFFER(HIGH)(3 downto 0);
alias B       : bit_vector(2 downto 0)
       is CPU_BUFFER(LOW) (2 downto 0);

--

CPU_DATA_TMP := (B & A) + OPERAND;
```

An alias of an array object can be indexed in the opposite direction
```vhdl
signal BUS_A :
    std_ulogic_vector(7 downto 0);

alias BIT_REV_A :
    std_ulogic_vector(0 to 7) is BUS_A;
```

<h3 class="text-hr"><span>Synthesis Issues</span></h3>

Aliases are not supported by many logic synthesis tools.

A work-around is to declare new "alias" signals, variables or constants, and assign them with the slice expression. With signals and variables this increases simulation overhead, but preserves readability.

Such "alias" signals should be assigned concurrently, and "alias" variables should be reassigned each time their process is activated.

<h3 class="text-hr"><span>New in VHDL-93</span></h3>

Aliases may be applied much more extensively in VHDL-93.

All objects may be aliased, i.e. signals, files, variables and constants.

All "non-objects" can also be aliased, except labels, loop parameters and generate parameters. For instance:

```vhdl
-- an alias of a type
alias MY_LOGIC is ieee.std_logic_1164.std_logic;

-- an alias of a component
alias NAND2 is ASIC_LIB.ONE_MICRON.ND2;
```
