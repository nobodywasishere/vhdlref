---
permalink: generics.html
layout: refpage
title: "Generic"
chart-left: "Declaration"
chart-right: [Entity, Component]
tags: [generics, map - generic]
parent: Declarations
lrm:
    - 93: [1.1.1.1, 5.2.1.2, 9.6]
---

## Syntax

<!-- include the vhdl tag to highlight as vhdl -->
```vhdl
entity entity_name is
    generic (
        -- generic list
    );
    port (
        -- port list
    );
end entity_name;
```

```vhdl
entity component_name is
    generic (
        -- generic list
    );
    port (
        -- port list
    );
end component_name;
```

```vhdl
instance_label: component_name
    generic map (
        -- generic_association_list
    )
    port map (
        -- port_association_list
    );
```

## Rules and Examples

__Generics__ are a means of passing specific information into an entity. They do not have a mode as they can only go into an entity or component:
```vhdl
entity PARITY is
    generic (
        N : integer
    );
    port (
        A : in std_ulogic_vector(N-1 downto 0),
        ODD : out std_ulogic
    );
end PARITY;
```

In the corresponding component declaration, the generics are also declared before the ports:
```vhdl
component PARITY is
    generic (
        N : integer
    );
    port (
        A : in std_ulogic_vector(N-1 downto 0),
        ODD : out std_ulogic
    );
end component;
```

An instance of a component with __generics__, has a __generic map__ declared before the port map (note: there is no semicolon between them!). This allows a value to be set for the generic:
```vhdl
U1: PARITY
    generic map (
        N => 8
    )
    port map (
        A => DATA_BYTE,
        ODD => PARITY_BYTE
    );
```

By declaring __generics__ of type __time__, delays may be programmed on an instance-by-instance basis. __Generics__ may be given a default value, in case a value is not supplied for all instances:
```vhdl
entity AN2_GENERIC is
    generic (
        DELAY : time := 1.0 ns
    );
    port (
        A, B : in std_ulogic;
        Z : out std_ulogic
    );
end AN2_GENERIC;

architecture BEH of AN2_GENERIC is

begin

    Z <= A and B after DELAY;

end A;
```

The value of a generic may be read in either the entity or any of its architectures. It may even be passed into lower-level components.

Default values for generics may be given in an entity declaration or in a component declaration. generics may be set (via a generic map) in an instantiation, or a configuration. The rules regarding different combinations of these are complex: see _VHDL_ by Douglas Perry, page 218.

## Synthesis Issues

Usually, only __generics__ of type integer are supported. Values for __generics__ in an entity declaration have to be supplied by the user to allow elaboration at the time of synthesis. __Generic map__ is usually ignored.
