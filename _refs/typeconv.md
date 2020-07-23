---
permalink: typeconv.html # url you want the page to be at
layout: refpage
title: "Type Conversion"
chart-left: "Expression" # for the left side of the chart
chart-right: [Package, Entity, Architecture, Process, Procedure, Function] # for the right side of the chart
tags: [] # list of tags
---

<h3 class="text-hr"><span>Syntax</span></h3>

<!-- include the vhdl tag to highlight as vhdl -->
```vhdl
target_type (closely_related_expression)
```

```vhdl
conversion_function (expression)
```

See LRM section 7.3.5

<h3 class="text-hr"><span>Rules and Examples</span></h3>

Objects of user-defined types cannot directly be assigned to or from objects of even a closely related type. A type conversion allows the assignment to be made:
```vhdl
type BUS_VAL is range 0 to 255;

variable X_INT : integer := 22;
variable X_BUS : BUS_VAL;

--

X_BUS := X_INT; --illegal
X_BUS := BUS_VAL(X_INT);
```

Closely related types are:
- integer types and real types
- array types whose lengths, index types and element types match.

For instance:
```vhdl
type T_BYTE is array (7 downto 0) of std_ulogic;
signal TYPE_BUS : T_BYTE;
signal VEC_BUS : std_ulogic_vector(7 downto 0);

--

TYPE_BUS <= VEC_BUS; --illegal
TYPE_BUS <= T_BYTE(VEC_BUS);
```

If conversion is required between types which are not closely related, a user defined function must be used:
```vhdl
signal X_BOOL: boolean;
signal X_STD:  std_ulogic;

function BOOL_TO_SL(
    X : boolean
) return std_ulogic is
begin
    if X then
        return ('1');
    else
        return ('0');
    end if;
end BOOL_TO_SL;

--

X_STD <= X_BOOL; --illegal
X_STD <= BOOL_TO_SL(X_BOOL);
```

A type conversion function may be called in a port map to match port type to signal type.

<h3 class="text-hr"><span>Synthesis Issues</span></h3>

Most logic synthesis tools support type conversion for appropriate array and integer types.

Most also accept the type conversion functions in the std_logic_1164 package.

Some synthesis vendors supply a VHDL package containing conversion functions which the synthesizer will support.

<h3 class="text-hr"><span>New in VHDL-93</span></h3>

Type Conversions have not changed in VHDL-93. 
