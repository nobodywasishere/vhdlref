---
permalink: constdec.html
layout: refpage
title: "Constant"
used-in: [Entity, Package, Process, Architecture, Procedure, Function]
parent: Declarations
lrm:
    - 93: [4.3.1.1]
---

## Syntax

```vhdl
constant constant_name : type := value;
```

## Rules and Examples

```vhdl
constant BUS_WIDTH : integer := 8;
constant FOUR_ONES :
    std_logic_vector(3 downto 0):= "1111";

constant PERIOD : time := 10 ns;
constant MAX_SIM_TIME : time:= 50 * PERIOD;
```

The values of array constants other than string, bit_vector, and std_logic_vector must be set using aggregates.
```vhdl
type T_CLOCK_TIME is ARRAY(3 downto 0) of
    integer range 0 to 9;
constant TWELVE_O_CLOCK :
    T_CLOCK_TIME := ( 1, 2, 0, 0);
```

In a package, a constant may be __deferred__. This means its value is defined in the package body, and the value may be changed only by re-analyzing the package body.
```vhdl
package P is
    constant C : integer;
end P;

package body P is
    constant C : integer := 200;
end P;
```

Provided they are of the correct type, constants may be used in any expression. They may be associated with generics of component instances and passed into procedures.
```vhdl
process
    type T_DATA is array (0 to 3) of
        bit_vector(7 downto 0);
    constant DATA : T_DATA :=
        ("00001000",
         "00010001",
         "00100010",
         "01000011");

begin
    for I in DATA'range loop
        serialize_byte( DATA(I), DOUT);
    end loop;
end process;
```

Constants and constant expressions may also be associated with input ports of component instances.

## Synthesis Issues

Constants are supported for synthesis, providing they are of a type acceptable to the logic synthesis tool. They are either synthesized as connections to logic '1' or '0', or are used to help minimize the number of gates required. Deferred constants may not be supported.
