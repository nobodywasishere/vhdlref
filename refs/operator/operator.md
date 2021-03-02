---
permalink: operator.html
layout: refpage
title: "Logical Operations"
chart-left: "Operator"
chart-right: [Expression]
lrm:
    - 93: [7.2]
---



## Syntax

See reference manual.

## Rules and Examples

The __logical operators__ are predefined for __bit__, __boolean__, __bit_vector__, linear arrays of __boolean__, __std_logic__ and __std_logic_vector__ types. They return a value of the same type:
```vhdl
C <= A and B;
C <= A or B;
C <= A nand B;
C <= A nor B;
C <= A xor B;
C <= A xnor B;
C <= not B;
```

| A | B | and | or | nand | nor | xor | xnor | not |
|---|---|-----|----|------|-----|-----|------|-----|
| 0 | 0 | 0   | 0  | 1    | 1   | 0   | 1    | 1   |
| 0 | 1 | 0   | 1  | 1    | 0   | 1   | 0    | 0   |
| 1 | 0 | 0   | 1  | 1    | 0   | 1   | 0    | 1   |
| 1 | 1 | 1   | 1  | 1    | 0   | 0   | 1    | 0   |

The equality and inequality operators are predefined for all types, and they return a boolean value:
```vhdl
if (A = B) then -- equal to
    -- other code here
end if;

if (A /= B) then -- not equal to
    -- other code here
end if;
```

The other relational operators are predefined for all scalar types, and all one-dimensional array types. They also return a boolean value:
```vhdl
<   -- less than
>   -- greater than
<=  -- less than or equal to
>=  -- greater than or equal to
```

For arrays of different lengths, the predefined relational operators align the left-hand elements and compare corresponding positions. This can lead to unexpected results:
```vhdl
constant ARR1 : bit_vector := "0011";
constant ARR2 : bit_vector := "01";
-- (ARR1 < ARR2) will return true
```

The __&__ operator is used to concatenate (join) arrays, or join new elements to an array:
```vhdl
Z_BUS(1 downto 0) <= '0' & B_BIT;
BYTE <= A_BUS & B_BUS;
```

For physical types (i.e. time), assignments must be dimensionally consistent:
```vhdl
variable TIME1,TIME2: time;

...

TIME1 := TIME2 * 2.5;
TIME1 := TIME2 / 4;
TIME1 := 3.6 ns + TIME2;
TIME1 := TIME2 * 6.67 ns;   --illegal
```

Other numeric operators are exponentiation (__\**__), absolute value (__abs__), modulus (__mod__), and remainder (__rem__).

Shift and rotate operators are defined for one-dimensional arrays of bit or boolean:
```vhdl
sll -- shift left logical
srl -- shift right logical
sla -- shift left arithmetic
sra -- shift right arithmetic
rol -- rotate left
ror -- rotate right
```

## Synthesis Issues

Most predefined operators are synthesizable, providing they are used with types accepted by the synthesis tool. See also [type declarations]({{ site.baseurl }}/type_dec.html) and [overloading]({{ site.baseurl }}/qualifex.html).

The following are not usually synthesizable, except as part of a constant expression: exponentiation (\**), division by other than 2, mod, rem.
