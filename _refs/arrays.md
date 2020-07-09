---
permalink: /arrays.html # url you want the page to be at
layout: page
title: "Arrays"
description: "An arraycontains multiple elements of the same type."
chart-left: "Declaration" # for the left side of the chart
chart-right: [package, entity, architecture, process, procedure, function] # for the right side of the chart
---

{% include chart.html %}

<h3 class="text-hr"><span>Syntax</span></h3>

```vhdl
type type_name is array (range) of element_type;
```
See LRM section 3.2.1

<h3 class="text-hr"><span>Rules and Examples</span></h3>

An __array__ contains multiple elements of the same type. When an array object is declared, an existing array type must be used.
```vhdl
type NIBBLE is array (3 downto 0) of std_ulogic;
type RAM is array (0 to 31) of integer range 0 to 255;
signal A_BUS : NIBBLE;
signal RAM_0 : RAM;
```

An array type definition can be __unconstrained__, i.e. of undefined length. __String__, __bit_vector__, and __std_logic_vector__ are defined in this way. An object (signal, variable or constant) of an unconstrained array type must have it's index type range defined when it is declared.
```vhdl
type INT_ARRAY is array (integer range <>) of integer;
variable INT_TABLE: INT_ARRAY(0 to 9);
variable LOC_BUS : std_ulogic_vector(7 downto 0);
```

Arrays with character elements such as __string__, __bit_vector__, and __std_logic_vector__ may be assigned a literal value using double quotes (see __literals__):
```vhdl
CONSTANT MSG_o: string := "Test 1 Completed";

A_BUS <= "0000";
LOC_BUS <= "10101010";
```

Arrays may also be assigned using __concatenation__ (&), [__aggregates__]({{ 'aggregat.html' | absolute_url }}), __slices__, or a mixture. By default, assignment is made by __position__.
```vhdl
A_BUS <= (A_BIT, B_BIT, C_BIT, D_BIT);

-- an equivalent assignment:
A_BUS <= (A_BIT & B_BIT & C_BIT & D_BIT);

-- rotate A_BUS to the left:
A_BUS <= A_BUS(2 downto 0) & A_BUS(3);
```

Arrays of arrays may be declared. These are useful for memories, vector tables, etc.:
```vhdl
type MEM is array (0 to 7) of NIBBLE;
-- an array "array of array" type
variable MEM8X4 : MEM;

--

-- accessing the whole array:
MEM8X4 := ("0000", "0001", "0010", "0011", "0100", "0101", "0110", "0111");
-- accessing a "word"
MEM8X4(5) := "0110";
-- accessing a single bit
MEM8X4(6) (0) := '0';
```

True two (or more) dimensional arrays may also be declared:
```vhdl
type T_2D is array (3 downto 0, 1 downto 0) of integer;
signal X_2D : T_2D;

--

X_2D <= ((0,0), (1,1), (2,2), (3,3));
X_2D(3,1) <= 4;
```

<h3 class="text-hr"><span>Synthesis Issues</span></h3>

Most logic synthesis tools accept one-dimensional arrays of other supported types. 1-D arrays of 1-D arrays are often supported. Some tols also allow true 2-D arrays, but not more dimensions.

Note that arrays are usually implemented using gates and flip-flops, not ROM's and RAM's.

<h3 class="text-hr"><span>New in VHDL-93</span></h3>

Array types have not changed in VHDL-93.
