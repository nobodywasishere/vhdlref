---
permalink: generate.html
layout: refpage
title: "Generate Statement"
chart-left: "Concurrent Statement"
chart-right: [Architecture]
tags: [generate, generics, generate - for, generate - if]
parent: Concurrent Statements
lrm:
    - 93: [9.7]
---



## Syntax

<!-- include the vhdl tag to highlight as vhdl -->
```vhdl
label: for parameter in range generate

    -- concurrent statements

end generate label;
```

## Rules and Examples

The __for generate__ statement is usually used to instantiate "arrays" of components. The generate parameter may be used to index array-type signals associated with component ports:
```vhdl
architecture GEN of REG_BANK is

    component REG
        port(
            D, CLK, RESET : in std_ulogic;
            Q : out std_ulogic
        );
    end component;

begin

    GEN_REG:
    for I in 0 to 3 generate
        REGX : REG port map ( DIN(I), CLK, RESET, DOUT(I));
    end generate GEN_REG;

end GEN;
```

A label is compulsory with a __generate__ statement.

The __for generate__ statement is particularly powerful when used with integer __generics__.

Instance labels inside a __generate__ statement do not need to have an index:
```vhdl
REGX(I): -- Illegal
```

__For generate__ statements may be nested to create two-dimensional instance "arrays".

Another form of __generate__ is the __if generate__ statement. This is usually used within a __for generate__ statement, to account for irregularity. For instance, a ripple-carry adder with no carry-in:
```vhdl
architecture GEN of RIPPLE is

    component FULLADD
        port (
            A, B, CIN : in bit;
            SUM, CARRY : out bit
        );
    end component;

    component HALFADD
        port(
            A, B : in bit;
            SUM, CARRY : out bit
        );
    end component;

    signal C : bit_vector(0 to 7);

begin

    GEN_ADD: for I in 0 to 7 generate

        LOWER_BIT: if I=0 generate
            U0: HALFADD port map ( A(I), B(I), S(I), C(I));
        end generate LOWER_BIT;

        UPPER_BITS: if I>0 generate
            UX: FULLADD port map ( A(I), B(I), C(I-1), S(I), C(I));
        end generate UPPER_BITS;

    end generate GEN_ADD;

    COUT <= C(7);

end GEN;
```

A __generate__ statement may contain local declarations, followed by the keyword begin.

## Synthesis Issues

__Generate__ statements are usually supported for synthesis.
