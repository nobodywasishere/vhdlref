---
permalink: while.html # url you want the page to be at
layout: refpage
title: "While and Infinite Loop"
chart-left: "Sequential Statement" # for the left side of the chart
chart-right: [Process, Function, Procedure] # for the right side of the chart
tags: [loop, loop - while, loop - infinite, wait, exit] # list of tags
---

<h3 class="text-hr"><span>Syntax</span></h3>

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

See LRM section 8.8

<h3 class="text-hr"><span>Rules and Examples</span></h3>

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

<h3 class="text-hr"><span>Synthesis Issues</span></h3>

While and infinite loops are supported by some logic synthesis tools, with certain restrictions.

<h3 class="text-hr"><span>New in VHDL-93</span></h3>

The while and infinite loop statements have not changed in VHDL-93.
