---
permalink: ifs.html
layout: refpage
title: "If Statement"
used-in: [Process, Function, Procedure]
tags: [if, elif, else]
parent: Sequential Statements
lrm:
    - 93: [8.6]
---



## Syntax

<!-- include the vhdl tag to highlight as vhdl -->
```vhdl
if condition1 then

    -- sequential statements

elsif condition2 then

    -- sequential statements

else

    -- sequential statements

end if;
```

## Rules and Examples

Conditions may overlap - only the statements after the first "true" condition are executed.
```vhdl
if (X = 5) and (Y = 9) then
    Z <= A;
elsif (X >= 5) then
    Z <= B;
else
    Z < C;
end if;
```

The __elsif__ and __else__ clauses are optional. This process models a transparent latch:
```vhdl
process (EN, D)
begin

    if (EN = '1') then
        Q <= D;
    end if;

end process;
```

A condition can be any boolean expression:
```vhdl
process (ALARM_TIME, CURRENT_TIME)

    variable AL_EQ_CUR: boolean;

begin

    AL_EQ_CUR := (ALARM_TIME = CURRENT_TIME);

    if AL_EQ_CUR then
        SOUND_ALARM <= '1';
    else
        SOUND_ALARM <= '0';
    end if;

end process;
```

An if statement may be used to infer edge-triggered registers in a process sensitive to a clock signal. Asynchronous reset may also be modeled:
```vhdl
process(CLK, RESET)
begin

    if RESET = '1' then

        COUNT <= 0;

    elseif CLK'event and CLK='1' then

        if (COUNT >= 9) then
            COUNT <= 0;
        else
            COUNT <= COUNT + 1;
        end if;

    end if

end process;
```

If statements may be used to specify conditional assignments or state transitions in a finite state machine:
```vhdl
case READ_CPU_STATE is

    when WAITING =>
        if CPU_DATA_VALID = '1' then
            CPU_DATA_READ <= '1';
            READ_CPU_STATE <= DATA1;
        end if;

    when DATA1 =>

    -- other branches of the case statement

end case;
```

The `if` may have an optional label:
```vhdl
label: if condition then

    -- etc

end if label
```

## Synthesis Issues

The if statement is generally synthesizable. Where an if statement is used to detect the clock edge in a "clocked process", certain conventions must be obeyed. Using an if statement without an else clause in a "combinational process" can result in latches being inferred, unless all signals driven by the process are given unconditional default assignments. For more details see [Process]({{ site.baseurl }}/process.html).
