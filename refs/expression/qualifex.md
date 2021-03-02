---
permalink: qualifex.html
layout: refpage
title: "Qualified Expression"
chart-left: "Expression"
chart-right: [Entity, Architecture, Package, Package Body]
tags: []
parent: Expressions
lrm:
    - 93: [7.3.4]
---

## Syntax

<!-- include the vhdl tag to highlight as vhdl -->
```vhdl
type'(expression)
```

## Rules and Examples

A qualified expression is an expression with its type explicitly stated. This is necessary where it might otherwise be ambiguous:
```vhdl
string'("0010");
bit_vector'("0010");
std_logic_vector'("0010");
```

Qualified expressions may be required when calling overloaded functions or procedures. The qualification makes it clear which version is being called:
```vhdl
architecture OVER of A is

    signal P_STD : std_logic;
    signal P_BIT : bit;

    function PARITY (
        X : bit_vector
    ) return bit is
    begin
      -- function code
    end PARITY;

    function PARITY (
        X : std_logic_vector
    ) return std_logic is
    begin
      -- function code
    end PARITY;

begin
    P_BIT <= PARITY(bit_vector'("00100"));
    P_STD <= PARITY(std_logic_vector'("10101"));
end OVER;
```

Qualification may be necessary for certain aggregate and array expressions:
```vhdl
entity CONCAT is
    port(
        A, B : in  std_ulogic;
        VALUE: out integer range 0 to 9
    );
end CONCAT;

architecture BEHAVIOURAL of CONCAT is
    subtype T_2 is std_ulogic_vector(1 downto 0);
begin
    process(A, B)
    begin
        case T_2'(A & B) is
            when "00"   => VALUE <= 0;
            when "01"   => VALUE <= 1;
            when "10"   => VALUE <= 2;
            when "11"   => VALUE <= 3;
            when others => VALUE <= 9;
        end case;
    end process;
end BEHAVIOURAL;
```

## Synthesis Issues

Qualified expressions are usually supported by logic synthesis tools, providing the expression is of a synthesizable type.
