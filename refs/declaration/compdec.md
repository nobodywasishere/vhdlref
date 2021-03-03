---
permalink: compdec.html
layout: refpage
title: "Component"
used-in: [Architecture, Package]
tags: [configuration, begin, component, declaration, component instantiation]
parent: Declarations
lrm:
    - 93: [4.5, 1.1.1.1, 1.1.1.2]
---


## Syntax

```vhdl
component component_name is
    generic (
        generic_list
    );
    port (
        port_list
    );
end component [component_name];
```

## Rules and Examples

The port list must define the name, the mode (i.e.direction) and the type of each port on the component.
```vhdl
component HALFADD is
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

    component ORGATE is
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
component PARITY is
    generic (
        N : integer
    );
    port (
        A : in  std_ulogic_vector(N-1 downto 0);
        ODD : out std_ulogic
    );
end component;
```

An entity-architecture pair can be instantiated directly. In this case a component declaration is not required. This is more compact, but does not allow the flexibility of configuration. See [__Component Instantiation__]({{ site.baseurl }}/'compinst.html').

## Synthesis Issues

__Component__ declarations are supported for synthesis, providing the port types are acceptable to the logic synthesis tool. Usually, only generics of type integer are supported. Whether a synthesis tool will "flatten through" a component, treat is as a "black box", or recognize it as a primitive is usually under the user's control.
