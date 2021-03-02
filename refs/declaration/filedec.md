---
permalink: filedec.html
layout: refpage
title: "File Declaration"
used-in: [Package Process Architecture Procedure Function]
tags: [file, mode, in, out, endfile, readline, read, std.textio, write, writeln, bit, bit_vector, boolean, character, integer, real, string, time, "'image", "'value"]
parent: Declarations
lrm:
    - 93: [3.4, 4.3.2, 14.3]
---



## Syntax

<!-- include the vhdl tag to highlight as vhdl -->
```vhdl
file logical_name : file_type is mode "file_name";
```

## Rules and Examples

Usually, files of type __text__ are used as they are portable between different VHDL simulators. The mode of the __file__ refers to the direction of data flow, and may be either __in__ (i.e. a read-only __file__) or __out__ (a write-only __file__):
```vhdl
use std.textio.all;

package REF_PACK is
    file INFILE  : text is  in "in.dat";
    file OUTFILE : text is out "out.dat";
end REF_PACK;
```

Text files may be read by using the __endfile__, __readline__ and __read__ subprograms defined in the package __std.textio__:
```vhdl
READ_FILE: process

    variable VEC_LINE : line;
    variable VEC_VAR : bit_vector(0 to 7);
    file VEC_FILE : text is in "stim.vec";

begin

    while not endfile(VEC_FILE) loop
        readline (VEC_FILE, VEC_LINE);
        read (VEC_LINE, VEC_VAR);
        A_BUS <= VEC_VAR;
        wait for 10 ns;
    end loop;
    wait;

end process READ_FILE;
```

The textio package must be made visible by the clause:
```vhdl
use std.textio.all;
```

Text files may be written by using the __write__ and __writeln__ subprograms, also defined in the textio package. Output data may be formatted using optional parameters for __write__.

Textio __read__ and __write__ procedures are defined for the types __bit__, __bit_vector__, __boolean__, __character__, __integer__, __real__, __string__ and __time__. They are not compatible with user-defined types or std_logic_1164 types (although some vendors supply routines for the std_logic_1164 types).

Text files may be written by using the __writeln__ and __write__ subprograms defined in the package __std.textio__:
```vhdl
WRITE_FILE: process (CLK)

    variable VEC_LINE : line;
    file VEC_FILE : text is out "results";

begin

    -- strobe OUT_DATA on falling edges
    -- of CLK and write value out to file

    if CLK='0' then
        write (VEC_LINE, OUT_DATA);
        writeline (VEC_FILE, VEC_LINE);
    end if;

end process WRITE_FILE;
```

A __file__ (read or write) is opened in VHDL when the structure in which it is declared is elaborated. This means that files declared in processes or architectures are opened only once at the beginning of a simulation. files declared in procedures are reopened at the beginning of the __file__ every time the procedure is elaborated (every time it is executed) and are closed every time the procedure finishes execution.

Files can be explicitly opened and closed during simulation.
```vhdl
file MYTEXT : text open read_mode is "enum.txt";
```

The attributes __'image__ and __'value__ can be used to make textio for enumerated types, see [__attributes__]({{ site.baseurl }}/"attrib.html").

## Synthesis Issues

__File__ declarations and operations are not supported by logic synthesis tools.
