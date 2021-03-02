---
permalink: packageb.html
layout: refpage
title: "Package Body"
chart-left: "Secondary Library Unit"
chart-right:
tags: [type, subtype, constant, file, alias, attribute, function, procedure, body, package, wait, unconstrained, end, constant, process - postponed]
parent: Declarations
lrm:
    - 93: [2.6]
---



## Syntax

<!-- include the vhdl tag to highlight as vhdl -->
```vhdl
package body package_name is
    -- declarations
    -- deferred constant declarations
    -- subprogram bodies
end package_name;
```

## Rules and Examples

When a procedure or function is declared in a package, its body (the algorithm part) must be placed in the package body:
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

Other declarations made in a package body may be used within that body, but are not visible outside. declarations may typically be any of the following: type, subtype, constant, file, alias, attribute, function, procedure.

A constant declared in a package may be deferred. This means its value is defined in the package body. The value may be changed by re-analyzing only the package body:
```vhdl
package P is
    constant C : integer;
end P;

package body P is
    constant C : integer := 200;
end P;
```

A package body cannot be analyzed unless a matching package exists in the same design library. Each package can only have one body.

The keyword __end__ may be followed by the keyword __package body__, for clarity and consistency.

## Synthesis Issues

Package bodies are usually supported by synthesis tools, provided all the items they declare are compatible with synthesis.

A package body must usually be in the same design file as the package itself.
