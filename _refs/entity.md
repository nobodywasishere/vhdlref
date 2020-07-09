---
permalink: /entity.html # url you want the page to be at
layout: page
title: "Entity"
description: "Entity."
chart-left: "Primary Library Unit" # for the left side of the chart
chart-right: # for the right side of the chart
---

{% include chart.html %}

<h3 class="text-hr"><span>Syntax</span></h3>

```vhdl
entity entity_name is
    generic (generic_list);
    port (port_list);
end entity_name;
```

See LRM section 1.1

<h3 class="text-hr"><span>Rules and Examples</span></h3>

The port list must define the name, the mode (i.e. direction) and the type of each port on the __entity__:
```vhdl
entity HALFADD is
    port(
        A,B : in bit;
        SUM, CARRY : out bit
    );
end HALFADD;

entity COUNTER is
    port (
        CLK  : in std_ulogic;
        RESET: in std_ulogic;
        Q    : out integer range 0 to 15
    );
end COUNTER;
```

The top-level __entity__ in a simulatable VHDL model is usually "empty", i.e. has no ports. Its architecture is usually the "test bench":
```vhdl
entity TB_DISPLAY is
end TB_DISPLAY;

architecture TEST of TB_DISPLAY is

    -- component declaration(s)
    -- signal declarations

begin

    -- component instance(s)
    -- test processes

end TEST;
```

Each entity port acts like a signal which is visible in the architecture(s) of the entity. The mode (direction) of each port determines whether it may be read from or written to in the architecture:

|  Mode  | Read in Arch | Write in Arch |
|:------:|:------------:|:-------------:|
| in     | Yes          | No            |
| out    | No           | Yes           |
| inout  | Yes          | Yes           |
| buffer | Yes          | Yes           |

If an __entity__ has generics, these must be declared before the ports. They do not have a mode, as by definition they can only pass information into the __entity__:
```vhdl
entity AN2_GENERIC is
    generic (
        DELAY: time := 1.0 ns
    );
    port (
        A,B : in std_ulogic;
        Z : out std_ulogic
    );
end AN2_GENERIC;
```

An entity may also contain declarations. Items declared are visible within the architecture(s) of the entity.

<h3 class="text-hr"><span>Synthesis Issues</span></h3>

Entity declarations are supported for synthesis, providing the port types are acceptable to the logic synthesis tool. Usually, only generics of type integer are supported. Values for generics have to be supplied by the user at the time of synthesis.

<h3 class="text-hr"><span>New in VHDL-93</span></h3>

In VHDL-93, the keyword __end__ may be followed by the keyword __entity__ for clarity and consistency.
