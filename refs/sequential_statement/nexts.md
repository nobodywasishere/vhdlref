---
permalink: nexts.html
layout: refpage
title: "Next Statement"
used-in: [Loop, For Loop, While Loop]
parent: Sequential Statements
lrm:
    - 93: [8.9]
---

## Syntax

<!-- include the vhdl tag to highlight as vhdl -->
```vhdl
next;
```

```vhdl
next loop_label;
```

```vhdl
next loop_label when condition;
```

## Rules and Examples

The __next__ statement is used to prematurely terminate the current iteration of a __while__, __for__ or infinite __loop__:
```vhdl
for I in 0 to 7 loop
    if SKIP = '1' then
        next;
    else
        N_BUS <= TABLE(I);
        wait for 5 ns;
    end if;
end loop;
```

The next statement may test a boolean condition directly using the __when__ keyword:
```vhdl
process (A)
begin
    Z <= "0000";
    for I in 0 to 3 loop
        next when A /= I;
        Z(I) <= '1';
    end loop;
end process;
```

For a next statement within a set of nested loops, the optional loop label may be used to indicate which level of loop is to be iterated. The default (no label) is the innermost loop. If an outer loop is specified, loops inside are effectively exited:
```vhdl
READ_BUS: process
begin
    RESETLOOP: loop

        VALID_CHECK: while
            (CPU_DATA_VALID /= '1') loop
            wait until rising_edge(CLK) or RESET = '1';
            next RESETLOOP when RESET='1';
        end loop VALID_CHECK;

        CPU_DATA_READ <= '1';
        wait until rising_edge(CLK);
        LOCAL_BUFFER <= DATA_BUS;
        wait until rising_edge(CLK);
        CPU_DATA_READ <= '0';

    end loop RESETLOOP;
end process READ_BUS;
```

The next statement may have an optional label:
```vhdl
label next loop_label;
```
## Synthesis Issues

The next statement is supported by some logic synthesis tools, with certain restrictions.
