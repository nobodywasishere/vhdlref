---
permalink: exist.html # url you want the page to be at
layout: refpage
title: "Exit Statement"
chart-left: "Sequential Statement" # for the left side of the chart
chart-right: [loop, loop - for, loop - while, when, exit] # for the right side of the chart
---



<h3 class="text-hr"><span>Syntax</span></h3>

<!-- include the vhdl tag to highlight as vhdl -->
```vhdl
exit;
```
```vhdl
exit loop_label;
```
```vhdl
exit loop_label when condition;
```
See LRM section 8.10

<h3 class="text-hr"><span>Rules and Examples</span></h3>

The exit statement is used to terminate a __while__, __for__ or infinite __loop__:
```vhdl
for I in 0 to 7 loop
    if FINISH_LOOP_EARLY = '1' then
        exit;
    else
        A_BUS <= TABLE(I);
        wait for 5 ns;
    end if;
end loop;
```

The exit statement may test a boolean condition directly using the __when__ keyword:
```vhdl
process (A)
    variable I : integer range 0 to 4;
begin
    Z <= "0000";
    I := 0;    
    loop
        exit when I = 4;
        if (A = I) then
            Z(I) <= '1';
        end if;
            I := I + 1;
    end loop;
end process;
```

For an exit statement within a set of nested loops, the optional loop label may be used to indicate which level of loop is to be exited. The default (no label) is the innermost loop:
```vhdl
L1: for I in 0 to 7 loop

    L2: for J in 0 to 7 loop

        exit L1 when QUIT_BOTH_LOOPS = '1';
        exit when QUIT_INNER_LOOP = '1';

        -- other statements

    end loop L2;

end loop L1;
```

<h3 class="text-hr"><span>Synthesis Issues</span></h3>

The exit statement is supported by some logic synthesis tools, barring certain restrictions.

<h3 class="text-hr"><span>New in VHDL-93</span></h3>

In VHDL-93, the __exit__ statement may have an optional label
```vhdl
label: exit loop_label;
```
