---
permalink: procedur.html
layout: refpage
title: "Procedure"
used-in: [Package, Entity, Architecture, Process, Procedure, Function]
tags: [unconstrained, package body, statement - wait, process, function, package, process - postponed]
parent: Declarations
lrm:
    - 93: [2.1, 2.2, 8.5, 9.3]
---

## Syntax

<!-- include the vhdl tag to highlight as vhdl -->
```vhdl
procedure procedure_name (parameter_list) is
    declarations
begin
    sequential statements
end procedure_name;
```

## Rules and Examples

Procedures may have in, out or inout parameters. These may be signal, variable or constant. the default for in parameters is constant. For out and inout it is variable. In fact, a constant in parameter can be associated with a signal, variable constant or expression when the procedure is called:
```vhdl
procedure DISPLAY_MUX (
    ALARM_TIME, CURRENT_TIME : in digit;
    SHOW_A : in std_ulogic;
    signal DISPLAY_TIME : out digit
) is
begin
    if (SHOW_A = '1') then
        DISPLAY_TIME <= ALARM_TIME;
    else
        DISPLAY_TIME <= CURRENT_TIME;
    end if;
end DISPLAY_MUX;
```

Procedures may be called concurrently or sequentially. A concurrent procedure call executes whenever any of its in or inout parameters change:
```vhdl
architecture SUBPROG of DISP_MUX is
--
begin
    DISPLAY_MUX (ALARM_TIME, CURRENT_TIME, SHOW_A, DISPLAY_TIME);
end SUBPROG;
```

A procedure may declare local variables. These do not retain their values between successive calls, but are re-initialized each time. Array-type parameters may be unconstrained
```vhdl
procedure PARITY (
    signal X : in std_ulogic_vector;
    signal Y : out std_ulogic
) is
    variable TMP : std_ulogic := '0';
begin
    for J in X'range loop
        TMP := TMP xor X(J);
    end loop; -- works for any size X
    Y <= TMP;
end PARITY;
```

A procedure can contain wait statements, unless it is called from a process with a sensitivity list, or from within a function.

If a procedure is defined in a package, its body (the algorithm part) must be placed in the package body.  
```vhdl
package REF_PACK is
    procedure PARITY (
        signal X : in std_logic_vector;
        signal Y : out std_logic
    );
end REF_PACK;

package body REF_PACK is
    procedure PARITY (
        signal X : in std_logic_vector;
        signal Y : out std_logic
    ) is  
    begin
        -- procedure code
    end PARITY;
end REF_PACK;
```

The keyword __end__ may be followed by the keyword __procedure__ for clarity and consistency.

Procedures may be given an optional label.

A concurrent procedure call can be specified to run as a postponed process.

## Synthesis Issues

Procedures are usually supported for synthesis, providing they do not contain any wait statements.
