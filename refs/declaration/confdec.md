---
permalink: cofdec.html
layout: refpage
title: "Configuration"
title-short: "Config."
used-in:
tags: [configuration, declaration, default binding, last analyzed, all, others, specification, declaration, end]
parent: Declarations
lrm:
    - 93: [1.3]
---

Add information about what a configuration is and what it's used for
{: .todo }

## Syntax

```vhdl
configuration config_name of entity_name is
    for architecture_name
        for instance_label: component_name
            use entity library_name.entity_name(arch_name);
            for arch_name

                --

                lower-level configuration
                specifications

                --

            end for;
        end for;
    end for;
end [configuration] config_name;
```

```vhdl
configuration config_name of entity_name is
    for architecture_name
        for instance_label: component_name
            use configuration library_name.cfg_name;
        end for;
    end for;
end config_name;

## Rules and Examples

With first form of component configuration above, a whole hierarchy may be configured from a single declaration.

The second form above is used with a tree of configuration declarations, each one corresponding to a point in the hierarchy.

In the absence of an explicit configuration for any part of a model, __default binding__ will occur. For each unbound instance of every component, an entity will be selected whose name, port names and port types etc. match those in the corresponding component declaration. Where an entity has more than one architecture, the __last analyzed__ architecture will be used.

The keyword __all__ may be used to refer to all instances of a component:
```vhdl
configuration CFG_FULLADD of FULLADD is
    for STRUCTURAL
        for all : HALFADD use entity
            work.HALFADD(BEHAVE);
        end for;
    end for;
end CFG_FULLADD;
```

The keyword __others__ may also be used to refer to all instances not explicitly mentioned.

If the port names on an entity do not match those on the component declaration, a port map may be included in the configuration:
```vhdl
configuration CFG_FULLADD_DELAY of FULLADD is
    for STRUCTURAL
        for all : HALFADD
            use entity work.HA(B)
            port map(
                X => A,
                Y => B,
                S => SUM,
                C => CARRY
            );
        end for;
    end for;
end CFG_FULLADD_DELAY;
```

A configuration __specification__ for a component (or instance) may legally be overridden by a configuration __declaration__ for the same item.

## Synthesis Issues

Configuration is not usually supported by synthesis tools. The user usually has to ensure that component and entity names and ports match, and that only one architecture per entity is analyzed.
