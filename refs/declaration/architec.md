---
permalink: architec.html
layout: refpage
title: "Architecture"
used-in:
tags: [architecture, configuration, end, variable - shared, bound]
parent: Declarations
---


## Syntax


```vhdl
architecture architecture_name of entity_name is

    -- declarations

begin

    -- concurrent statements

end [architecture] architecture_name;
```

## Rules and Examples

Declarations may typically be any of the following: type, subtype, signal, constant, file, alias, component, attribute, function, procedure, configuration specification.
```vhdl
architecture TB of TB_CPU is

    component CPU_IF
        port (
            --port list
        );
    end component;

    signal CPU_DATA_VALID: std_ulogic;
    signal CLK, RESET: std_ulogic := '0';
    constant PERIOD : time := 10 ns;
    constant MAX_SIM: time := 50 * PERIOD;

begin

    -- concurrent statements

end TB;
```

Items declared in an architecture are visible in any process or block within it.

The order of concurrent statements is not important - behavior is defined by data dependencies only:
```vhdl
architecture EX1 of CONC is

    signal Z, A, B, C, D : integer;

begin

    D <= A + B;
    Z <= C + D;

end EX1;
```

An equivalent architecture:
```vhdl
architecture EX2 of CONC is

    signal Z, A, B, C, D : integer;

begin

    Z <= C + D;
    D <= A + B;

end EX2;
```

An architecture can contain any mix of component instances, processes or other concurrent statements:
```vhdl
architecture TEST of TB_DFF is

    component DFF is
        port (
            CLK, D:  in std_ulogic;
            Q     : out std_ulogic
        );
    end component;

    signal CLK, D, Q : std_ulogic := '0';

begin

    UUT: DFF port map (CLK, D, Q);

    CLK <= not (CLK) after 25 ns;

    STIMULUS: process
    begin
        wait for 50 ns;
        D <= '1';
        wait for 100 ns;
        D <= '0';
        wait for 50 ns;
    end process STIMULUS;

end TEST;
```

An entity can have one or more architectures. which one is used (or "bound") depends on the __configuration__.

An architecture cannot be analyzed unless the entity it refers to exists in the same design library.

__Shared variables__ may be declared within an architecture. Shared variables may be accessed by more than one process. However, the language does not define what happens if two or more processes make conflicting accesses to a shared variable at the same time.

## Synthesis Issues

Architectures are fully supported by synthesis tools, provided the declarations and statements they contain are compatible with synthesis.

Configuration is not usually supported by synthesis tools, so only one architecture per entity may be analyzed. With some tools, this architecture must be in the same design file as the entity.
