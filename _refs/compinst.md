---
permalink: /compinst.html # url you want the page to be at
layout: page
title: "Component Instantiation"
description: "Template Page."
chart-left: "Concurrent Statement" # for the left side of the chart
chart-right: [Architecture] # for the right side of the chart
tags: [list, positional, named, association, open, generic map]
---

{% include chart.html %}

<h3 class="text-hr"><span>Syntax</span></h3>

```vhdl
instance_label: component_name
    generic map (generic_association_list)
    port map (port_association_list);
```

See LRM section 9.6

<h3 class="text-hr"><span>Rules and Examples</span></h3>

The instance label is compulsory. The component name must match the relevant component declaration.
```vhdl
architecture STRUCT of INC is

    signal X,Y,S,C : bit;

    component HALFADD
        port (
            A,B : in bit;
            SUM, CARRY : out bit
        );
    end component;

begin

    U1: HALFADD port map (X, Y, S, C);

    -- other statements

end STRUCT;
```

The association <mark>list</mark> defines which local signals connect to which component ports. The association <mark>list</mark> above is __positional__, i.e. the signals are connected up in the order in which the ports were declared.

The alternative is __named association__, where ports are explicitly referenced and order is not important:
```vhdl
ADDER1: HALFADD
    port map (  
        B => Y,     
        A => X,
        SUM => S,
        CARRY => C
    );
```

Ports may be left unconnected using the keyword __open__:
```vhdl
ADDER1: HALFADD
    port map (  
        B => Y,     
        A => X,
        SUM => S,
        CARRY => open
    );
```

An instance of a component with generics, has a __generic map__ declared before the port map:
```vhdl
U1 : PARITY
    generic map (
        N => 8
    )
    port map (
        A => DATA_BYTE,
        ODD => PARITY_BYTE
    );
```

<h3 class="text-hr"><span>Synthesis Issues</span></h3>

Component instantiation is supported for synthesis, although __generic map__ is usually ignored. Whether a logic synthesis tool will "flatten through" a component, treat it as a "black box", or recognize it as a primitive is usually under the user's control.

<h3 class="text-hr"><span>New in VHDL-93</span></h3>

In VHDL-93, an entity-architecture pair may be directly instantiated (a component doesn't need to be declared). This is more compact, but does not allow the flexibility of configuration:
```vhdl
DIRECT: entity HA_ENTITY(HA_ARCH)
    port map ( A, B, S, C);
```
