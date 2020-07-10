---
permalink: attrib.html # url you want the page to be at
layout: refpage
title: "Attributes"
chart-left: "Attribute" # for the left side of the chart
chart-right: [Entity,Architecture,Package,Package Body] # for the right side of the chart
tags: [attributes, user defined attributes, group, "'high", "'low", "'left", "'right", "'range",
"'reverse_range", "'length", "'event", "'active", "'last_event", "'last_active", "'last_value", "'delayed(T)", "'stable(T)", "'quiet(T)", "'transaction", "'driving", "'driving_value", "'ascending", "'image(literal)", "'simple_name", "'instance_name", "'path_name"]
---

<!-- tables generated using https://www.tablesgenerator.com/markdown_tables -->


<h3 class="text-hr"><span>Syntax</span></h3>

```vhdl
object'attribute_name
```

See LRM sections 14.1, 4.4, 5.1 and 6.6


<h3 class="text-hr"><span>Rules and Examples</span></h3>

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

These attributes create a __new signal__, based on signal X:

|      Name     |                  Definition                  |
|:-------------:|:--------------------------------------------:|
| X'delayed(T)  | Signal X delayed by T (same type as X)       |
| X'stable(T)   | True if X unaltered for time T (boolean)     |
| X'quiet(T)    | True if X is unassigned for time T (boolean) |
| X'transaction | "Toggles" when X is assigned (bit)           |

__User defined attributes__ may be declared. These do not affect simulation, but may be used to supply information to other tools, e.g. for layout or synthesis:
```vhdl
type IC_PACKAGE is (DIL, PLCC, PGA);
attribute PTYPE: ICPACKAGE;
attribute PTYPE of U1 : component is PLCC;
attribute PTYPE of U2 : component is DIL;
```

<h3 class="text-hr"><span>Synthesis Issues</span></h3>

Logic synthesis tools usually support the predefined attributes __'high__, __'low__, __'left__, __'right__, __'range__, __reverse_range__, __'length__, and __'event__. Some tools support __'last_value__ and __'stable__

Several synthesis vendors define a set of attributes to supply synthesis directives such as area or timing constraints, enumeration encoding, etc.

<h3 class="text-hr"><span>New in VHDL-93</span></h3>

VHDL-93 has several new predefined attributes:

|       Name       |                              Definition                              |
|:----------------:|:--------------------------------------------------------------------:|
| X'driving        | True if a process is driving signal X                                |
| X'driving_value  | Value a process is driving signal X with                             |
| X'ascending      | True if index range of X is ascending                                |
| X'image(literal) | String representation of enumeration literal                         |
| X'simple_name    | String equivalent to the name of X                                   |
| X'instance_name  | Path downto and including X, excluding entity and architecture names |
| X'path_name      | Path downto and including X, excluding entity and architecture names |

The __group__ construct allows collections of VHDL objects of different classes to be grouped together to allow common attributes to be set for the elements of these groups.
