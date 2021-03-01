---
permalink: attrib.html
layout: refpage
title: "Attribute"
chart-left: "Attribute"
chart-right: [Entity,Architecture,Package,Package Body]
tags: [attributes, user defined attributes, group, "'high", "'low", "'left", "'right", "'range",
"'reverse_range", "'length", "'event", "'active", "'last_event", "'last_active", "'last_value", "'delayed(T)", "'stable(T)", "'quiet(T)", "'transaction", "'driving", "'driving_value", "'ascending", "'image(literal)", "'simple_name", "'instance_name", "'path_name"]
lrm:
    - 93: [14.1, 4.4, 5.1, 6.6]
---

<!-- tables generated using https://www.tablesgenerator.com/markdown_tables -->


## Syntax

```vhdl
object'attribute_name
```

## Rules and Examples

Attributes supply additional information about an item, e.g. a signal, variable, type or component. Certain attributes are predefined for types, array objects and signals.

These are some of the predefined attributes for scalar types, constrained array types and any objects declared to be of array types. They are the same type as the object (scalar), or the index (array):

|   Name  |        Definition        |
|:-------:|:------------------------:|
| X'high  | The upper bound of X     |
| X'low   | The lower bound of X     |
| X'left  | The leftmost bound of X  |
| X'right | The rightmost bound of X |

These are predefined only constrained array types and any objects declared to be of array types:

|       Name      |           Definition           |
|:---------------:|:------------------------------:|
| X'range         | The range of X                 |
| X'reverse_range | The range of X "back to front" |
| X'length        | X'high - X'low + 1 (integer)   |

These attributes are predefined for any signal X:

|      Name     |                 Definition                |
|:-------------:|:-----------------------------------------:|
| X'event       | True when signal X changes (boolean)      |
| X'active      | True when signal X assigned to (boolean)  |
| X'last_event  | When signal X last changed (time)         |
| X'last_active | When signal X was last assigned to (time) |
| X'last_value  | Previous value of X (same type as X)      |

These attributes create a new `signal`, based on signal X:

|      Name     |                  Definition                  |
|:-------------:|:--------------------------------------------:|
| X'ascending      | True if index range of X is ascending                                |
| X'delayed(T)  | Signal X delayed by T (same type as X)       |
| X'driving        | True if a process is driving signal X                                |
| X'driving_value  | Value a process is driving signal X with                             |
| X'image(literal) | String representation of enumeration literal                         |
| X'instance_name  | Path downto and including X, excluding entity and architecture names |
| X'path_name      | Path downto and including X, excluding entity and architecture names |
| X'simple_name    | String equivalent to the name of X                                   |
| X'stable(T)   | True if X unaltered for time T (boolean)     |
| X'quiet(T)    | True if X is unassigned for time T (boolean) |
| X'transaction | "Toggles" when X is assigned (bit)           |

A user defined `attribute` may be declared. These do not affect simulation, but may be used to supply information to other tools, e.g. for layout or synthesis:
```vhdl
type IC_PACKAGE is (DIL, PLCC, PGA);
attribute PTYPE: ICPACKAGE;
attribute PTYPE of U1 : component is PLCC;
attribute PTYPE of U2 : component is DIL;
```

The `group` construct allows collections of VHDL objects of different classes to be grouped together to allow common attributes to be set for the elements of these groups.

## Synthesis Issues

Logic synthesis tools usually support the predefined attributes `'high`, `'low`, `'left`, `'right`, `'range`, `'reverse_range`, `'length`, and `'event`. Some tools support `'last_value` and `'stable`.

Several synthesis vendors define a set of attributes to supply synthesis directives such as area or timing constraints, enumeration encoding, etc.
