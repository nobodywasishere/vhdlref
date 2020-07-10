---
permalink: filedec.html # url you want the page to be at
layout: refpage
title: "File Declaration"
chart-left: "Declaration" # for the left side of the chart
chart-right: [Package Process Architecture Procedure Function] # for the right side of the chart
tags: [file, mode, in, out, endfile, readline, read, std.textio, write, writeln, bit, bit_vector, boolean, character, integer, real, string, time, "'image", "'value"]
---



<h3 class="text-hr"><span>Syntax</span></h3>

<!-- include the vhdl tag to highlight as vhdl -->
```vhdl
file logical_name : file_type is mode "file_name";
```
See LRM sections 3.4, 4.3.2 and 14.3

<h3 class="text-hr"><span>Rules and Examples</span></h3>

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

Text files may be written by using the __write__ and __writeln__ subprograms, also defined in the textio package. Output data may be formatted using optional parameters for __write__ - see the LRM section 14.3.

Textio __read__ and __write__ procedures are defined for the types __bit__, __bit_vector__, __boolean__, __character__, __integer__, __real__, __string__ and __time__. They are not compatible with user-defined types or std_logic_1164 types (although some vendors supply routines for the std_logic_1164_types).

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

<h3 class="text-hr"><span>Synthesis Issues</span></h3>

__File__ declarations and operations are not supported by logic synthesis tools.

<h3 class="text-hr"><span>New in VHDL-93</span></h3>

VHDL-93 allows files to be explicitly opened and closed during simulation - this was not directly supported in VHDL-87. Consequently, __file declarations are not upwards-compatible between VHDL-87 and VHDL-93__. For instance, in VHDL-93 the equivalent declaration to the example above would be:
```vhdl
file MYTEXT : text open read_mode is "enum.txt";
```


The new attributes __'image__ and __'value__ make textio for enumerated types much easier - see
[__attributes__]({{ "attrib.html" | baseurl }}).
