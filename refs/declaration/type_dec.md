---
permalink: type_dec.html
layout: refpage
title: "Type Declaration"
used-in: [Package, Entity, Architecture, Process, Procedure, Function]
tags: []
parent: Declarations
lrm:
    - 93: [4.1, 3.0]
---

## Syntax

<!-- include the vhdl tag to highlight as vhdl -->
```vhdl
type type_name is type_definition;
```

## Rules and Examples

__Scalar__ types hold only one value. Predefined scalar types include __integer__, __real__, __bit__, __boolean__ and __character__.

User defined numeric types may be declared:
```vhdl
type T_INT is range 0 to 9;
type T_REAL is range -9.9 to 9.9;
type BUS_VAL is range 0 to 255;
```

User defined enumerated types may be defined with either characters or identifiers as literals:
```vhdl
type MY_STATE is (RESET,IDLE,ACKA);
type MY_LOGIC is ('X','0','1','Z');
```

Objects of a user-defined type cannot directly be assigned to or from objects of a different type. For more details see Subtypes and type conversions.

__Composite__ types (arrays and records) hold more than one value. __Array__ types have multiple elements of the same type. __Record__ types have named fields of differing types:
```vhdl
type T_PACKET is record
    BYTE_ID: std_ulogic;
    PARITY : std_ulogic;
    ADDRESS: integer range 0 to 3;
    DATA   : std_ulogic_vector(3 downto 0);
end record;
```

Record type objects are assigned using aggregates. Individual fields are assigned using a __selected name__:
```vhdl
signal TX_DATA : T_PACKET;

--

TX_DATA.ADDRESS <= 3;
```

Other types which may be declared are __file__ types, __access__ types and __physical__ types.

__Physical__ types are for describing physical quantities with units, i.e. voltage, temperature, area, etc. The predefined type __time__ is a physical type which can be expressed in the following units:

| Type | Units       |
|------|-------------|
| fs   | femtosecond |
| ps   | picosecond  |
| ns   | nanosecond  |
| us   | microsecond |
| ms   | millisecond |
| sec  | second      |
| min  | minute      |
| hr   | hour        |

Access types are dynamic pointer addressed types, useful for modeling potentially large structures, i.e. memory, FIFO queues, etc. For more details see the reference manual.

## Synthesis Issues

Most logic synthesis tools accept the following types:  __integer__, __boolean__, __bit__, user-defined __enumerated types__, __bit_vector__, linear __arrays__ and __records__ of other supported types, plus the __std_logic_1164__ types.

Synthesis tools will infer an appropriate number of bits for enumerated and integer types. It may be possible to specify the encoding to be used in each case.

Access, file, and physical types are unsupported.

The keywords __end record__ may be followed by the type name for clarity and consistency.

The predefined types __character__ and __string__ support an extended character set, including those used in most European languages.
