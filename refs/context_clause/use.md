---
permalink: use.html
layout: refpage
title: "Use Clause"
used-in: [Entity, Architecture, Package, Configuration]
tags: []
parent: Context Clause
lrm:
    - 93: [10.4]
---

## Syntax

<!-- include the vhdl tag to highlight as vhdl -->
```vhdl
use library_name.primary_unit_name;
```

```vhdl
use library_name.primary_unit_name.item;
```

## Rules and Examples

The use clause must appear before the start of the design unit itself. If the unit to be used is not in the library __work__, it must be preceded by a library clause:
```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.all;

entity WIDGET is

-- etc.

end WIDGET;
```

The use clause is valid only for the design unit immediately following it in the design file. However it also automatically applies to any secondary units associated with primary units for which it is valid.

Where multiple primary design units in the same design file need to use the same items, the use clause(s) must be repeated before each unit.

The last field in a use clause may be replaced by __all__ to access all items in a design unit, or all design units in a library:
```vhdl
library MY_LIB;
use MY_LIB.MY_PACK.all;
```

The shorter form of the use clause may appear in a configuration, to select which library entities are selected from:
```vhdl
library ASIC_LIB;
configuration ASIC_TECH of ENT is
    for GATE_ARCH
        use ASIC_LIB.all;
    end for;
end ASIC_TECH;
```

The shorter form of the use clause may also appear in the declarative part of an entity, architecture or block.

## Synthesis Issues

The use clause is usually supported by synthesis tools, but design libraries are often not.

Design files corresponding to any design units referenced by a use clause must be analyzed before the design units referencing them can be synthesized.
