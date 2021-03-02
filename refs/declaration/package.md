---
permalink: package.html
layout: refpage
title: "Package"
chart-left: "Primary Library Unit"
chart-right:
tags: [type, subtype, constant, file, alias, component, attribute, function, procedure, package, use clause, package body, deferred, shared variables, groups]
parent: Declarations
lrm:
    - 93: [2.5]
---



## Syntax

<!-- include the vhdl tag to highlight as vhdl -->
```vhdl
package package_name is
    -- declarations
end package_name;
```

## Rules and Examples

Declarations may typically be any of the following: type, subtype, constant, file, alias, component, attribute, function, procedure
```vhdl
package DEMO_PACK is

    constant SOME_FLAG : bit_vector := "11111111";

    type STATE is (RESET, IDLE, ACKA);

    component HALFADD
        port(
            A, B : in bit;
            SUM, CARRY : out bit
        );
    end component;

end DEMO_PACK;
```

Items declared in a package are visible wherever selected via a use clause. For instance, assume DEMO_PACK is analyzed into library work:
```vhdl
use work.DEMO_PACK.all;

entity DEMO is
    port (
        Z: out bit_vector(7 downto 0)
    );
end DEMO;

architecture BEHAVE of DEMO is
begin
    Z <= SOME_FLAG;
end BEHAVE;
```

When a procedure or function is declared in a package, its body (the algorithm part) must be placed in the package body.

A constant declared in a package may be deferred. This means that its value may be changed by re-analyzing only the package body:
```vhdl
package P is
    constant C : integer;
end P;

package body P is
    constant C : integer := 200;
end P;
```

Packages are usually supported by synthesis tools, provided all the items they declare are compatible with synthesis

Synthesizable declarations and non-synthesizable declarations (e.g.for a test bench) should therefore be placed in separated packages.

Design Libraries are often not supported, so design files containing packages must either by analyzed first for synthesis, or be present in the local directory.

If a package has a body, it must usually be in the same design file as the package itself.

The keyword __end__ may be followed by the keyword __package__, for clarity and consistency.

Shared variables and groups may also be declared in a package.

## Synthesis Issues

Logic synthesis tools may not support named association fully. Also, record assignments using aggregates may not be supported.
