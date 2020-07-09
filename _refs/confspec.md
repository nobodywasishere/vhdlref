---
permalink: confspec.html # url you want the page to be at
layout: page
title: "Configuration Specification"
description: "Configuration Specification."
chart-left: "Specification" # for the left side of the chart
chart-right: [Architecture] # for the right side of the chart
tags: [specification, all, others, default binding, last analyzed, declaration]
---

{% include chart.html %}

<h3 class="text-hr"><span>Syntax</span></h3>

```vhdl
for instance_label: component_name
    use entity
        library_name.entity_name(architecture_name);
```

```vhdl
for instance_label: component_name
    use configuration library_name.config_name;
```
See LRM section 5.2

<h3 class="text-hr"><span>Rules and Examples</span></h3>

Using a configuration __specification__, components may be configured within an architecture which instances them, rather than using a separate configuration declaration design unit. This is less flexible, as the architecture has to be re-analyzed to change the configuration.

Component instances may be individually configured:
```vhdl
architecture STR of XA is

    component HALFADD
        port(
            A,B : in bit;
            SUM, CARRY : out bit
        );
    end component;

    component ORGATE
        port(
            A,B : in bit;
            Z : out bit
        );
    end component;

    for U1 : HALFADD use entity work.HA(BEHAVE);
    for U2 : ORGATE use entity work.OG(BEHAVE);

begin

    U1: HALFADD port map ( A, B, S, C);
    U2: ORGATE port map ( A, B, Y);

end STR;
```

The keyword __all__ may be used to refer to all instances of a component:
```vhdl
for all: FULLADDER use entity
    work.FULLADD(STRUCTURAL);
```

The keyword __others__ may also be used to refer to all instances not explicitly mentioned.

If the port names on an entity do not match those on the component declaration, a port map may be included in the configuration:
```vhdl
for all:HALFADD use entity
    work.HALFADD(BEHAVE)
    port map (
        X => A,
        Y => B,
        S => SUM,
        C => CARRY
    );
```

In the absence of an explicit configuration for any part of a model, __default binding__ will occur. For each unbound instance of every component, an entity will be selected whose name, port names and port types etc. match those in the corresponding component declaration. Where an entity has more than one architecture, the __last analyzed__ architecture will be used.

<h3 class="text-hr"><span>Synthesis Issues</span></h3>

Configuration is not usually supported by synthesis tools. The user usually has to ensure that component and entity names and ports match, and that only one architecture per entity is analyzed.

<h3 class="text-hr"><span>New in VHDL-93</span></h3>

In VHDL-93, an entity-architecture pair may be directly instantiated, i.e. a component need not be declared. This is more compact, but does not allow the flexibility of configuration.
```vhdl
DIRECT: entity HA_ENTITY(HA_ARCH) port map( A, B, S, C);
```

In VHDL-93, a configuration __specification__ for a component (or instance) may legally be overridden by a configuration __declaration__ for the same item. This was not allowed in VHDL-87.
