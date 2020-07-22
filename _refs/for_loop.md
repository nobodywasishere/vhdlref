---
permalink: for_loop.html # url you want the page to be at
layout: refpage
title: "For Loop"
chart-left: "Sequential Statement" # for the left side of the chart
chart-right: [Process, Function, Procedure] # for the right side of the chart
tags: [loop - for, range, "'high", "'low", "'range", wait]
---



<h3 class="text-hr"><span>Syntax</span></h3>

<!-- include the vhdl tag to highlight as vhdl -->
```vhdl
optional_label: for parameter in range loop

    -- sequential statements

end loop label;
```
See LRM section 8.8

<h3 class="text-hr"><span>Rules and Examples</span></h3>

The __for__ loop defines a loop parameter which takes on the type of the range specified. For example, the range __0 to 3__ implies an integer:
```vhdl
process (A)
begin

    Z <= "0000";

    for I in o to 3 loop
        if (A = I) then
            Z(I) <= '1';
        end if;
    end loop;

end process;
```

Attributes such as __'high__, __'low__ and __'range__ may also be used to define the iterations of a __for__ loop:
```vhdl
process (A)#

    variable TMP : std_ulogic;

begin

    TMP := '0';

    for I in A'low to A'high loop
        TMP := TMP xor A(I);
        end loop;
    ODD <= TMP;

end process;

```

The range may be any discrete range, e.g. an enumerated type:
```vhdl
type PRIMARY is (RED, GREEN, BLUE);
type COLOUR is ARRAY (PRIMARY) of integer range 0 to 255;

-- other statements

MUX: process
begin

    for SEL in PRIMARY loop
        V_BUS <= VIDEO(SEL);
        wait for 10 ns;
    end loop;

end process MUX;
```

The loop parameter does not need to be declared: it is implicitly declared within the loop. It may not be modified within the loop:
```vhdl
for I in 1 to 10 loop
    if (REPEAT = '1') then
        I := I-1;    -- Illegal
    end if;
end loop;
```

<h3 class="text-hr"><span>Synthesis Issues</span></h3>

The for loop is supported for synthesis, providing:
* the loop range is static (i.e. implies a definite number of iterations), and
* the loop contains no __wait__ statements.

<h3 class="text-hr"><span>New in VHDL-93</span></h3>

The for loop statement has not changed in VHDL-93.
