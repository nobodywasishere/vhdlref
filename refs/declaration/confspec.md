---
permalink: confspec.html
layout: refpage
title: "Configuration Specification"
title-short: "Config. Specification"
used-in: [Architecture]
tags: [specification, all, others, default binding, last analyzed, declaration]
parent: Declarations
lrm:
    - 93: [5.2]
---

Add information about what a configuration is and what it's used for
{: .todo }

## Syntax

```vhdl
for instance_label: component_name
    use entity
        library_name.entity_name(architecture_name);
```

```vhdl
for instance_label: component_name
    use configuration library_name.config_name;
```

## Rules and Examples

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

An entity-architecture pair may be directly instantiated, i.e. a component need not be declared. This is more compact, but does not allow the flexibility of configuration.
```vhdl
DIRECT: entity HA_ENTITY(HA_ARCH) port map( A, B, S, C);
```

A configuration __specification__ for a component (or instance) may legally be overridden by a configuration __declaration__ for the same item.

## Synthesis Issues

Configuration is not usually supported by synthesis tools. The user usually has to ensure that component and entity names and ports match, and that only one architecture per entity is analyzed.
