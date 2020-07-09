---
permalink: /compdec.html # url you want the page to be at
layout: page
title: "Component Declaration"
description: "Component Declaration."
chart-left: "Declaration" # for the left side of the chart
chart-right: [Architecture, Package] # for the right side of the chart
tags: [configuration, begin, component, declaration]
---

{% include chart.html %}

<h3 class="text-hr"><span>Syntax</span></h3>

```vhdl
component component_name
    generic (
        generic_list
    );
    port (
        port_list
    );
end component;
```

See LRM sections 4.5, 1.1.1.1 and 1.1.1.2

<h3 class="text-hr"><span>Rules and Examples</span></h3>

The port list must define the name, the mode (i.e.direction) and the type of each port on the component.
```vhdl
component HALFADD
    port (
        A,B : in bit;
        SUM, CARRY : out bit
    );
end component;
```

A component declaration does not define the entity-architecture pair to be bound to each instance, or even the ports on the entity. These are defined by the __configuration__.

In an architecture, components must be declared before the __begin__ statement:
```vhdl
architecture STRUCTURAL of FULLADD is

    -- (local signal declarations here)

    component ORGATE
        port (
            A, B : in bit;
            Z : out bit
        );
    end component;

    -- (other component declarations)

begin

    -- the architecture contents

end STRUCTURAL;
```

A component declared in a package is visible in any architecture which uses the package, and need not be declared again.

For a component with generics, these must be declared before the ports. They do not have a mode, as by definition they can only pass information into the entity:
```vhdl
component PARITY
    generic (
        N : integer
    );
    port (
        A : in  std_ulogic_vector(N-1 downto 0);
        ODD : out std_ulogic
    );
end component;
```

<h3 class="text-hr"><span>Synthesis Issues</span></h3>

__Component__ declarations are supported for synthesis, providing the port types are acceptable to the logic synthesis tool. Usually, only generics of type integer are supported. Whether a synthesis tool will "flatten through" a component, treat is as a "black box", or recognize it as a primitive is usually under the user's control.

<h3 class="text-hr"><span>New in VHDL-93</span></h3>

In VHDL-93, an entity-architecture pair can be instantiated directly. In this case a component declaration is not required. This is more compact, but does not allow the flexibility of configuration.

In VHDL-93, the component name may be followed by the keyword __is__, for clarity and consistency. Also the keywords __end__ and __component__ may be followed by a repetition of the component name:
```vhdl
component component_name is
    port (port list);
end component component_name;
```