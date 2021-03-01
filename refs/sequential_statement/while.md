---
permalink: while.html
layout: refpage
title: "While and Infinite Loop"
chart-left: "Sequential Statement"
chart-right: [Process, Function, Procedure]
tags: [loop, loop - while, loop - infinite, wait, exit]
parent: Sequential Statements
lrm:
    - 93: [8.8]
---

## Syntax

<!-- include the vhdl tag to highlight as vhdl -->
```vhdl
while condition loop
   -- sequential statements
end loop;
```

```vhdl
loop
    -- sequential statements
end loop;
```

## Rules and Examples

The __while__ loop repeats the enclosed sequence of statements while the condition is true. The condition is tested before each iteration:
```vhdl
process (A)
    variable I : integer range 0 to 4;
begin
    Z <= "0000";
    I := 0;
    while (I <= 3) loop
        if (A = I) then
            Z(I) <= '1';
        end if;
        I := I + 1;
    end loop;
end process;
```

While loops may be useful in test benches:
```vhdl
process
begin
    while NOW < MAX_SIM_TIME loop
        CLK <= not CLK ;
        wait for PERIOD/2;
    end loop;
    wait;
end process;
```

To prevent simulation hang-up, an infinite loop should usually contain at least one __wait__ or __exit__ statement:
```vhdl
process (A)
    variable I : integer range 0 to 4;
begin
    Z <= "0000";
    I := 0;    
    L1: loop
        exit L1 when I = 4;
        if (A = I) then
            Z(I) <= '1';
        end if;
        I := I + 1;
    end loop;    
end process;
```

## Synthesis Issues

While and infinite loops are supported by some logic synthesis tools, with certain restrictions.
