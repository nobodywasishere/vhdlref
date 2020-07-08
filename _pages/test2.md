---
permalink: /notabout
layout: page
title: "Test 2"
---

# this is another test


| /* ... */              | Comment out from /* to */                                                                                                                                                                                               |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| #include "FILENAME"    | Include another file here                                                                                                                                                                                               |
| #define LABEL          | Define LABEL for #ifdef, #ifndef and #elif                                                                                                                                                                              |
| #define LABEL "STRING" | Replace LABEL by STRING; must be a single word                                                                                                                                                                          |
| #rand LABEL FORMAT     | Replace LABEL by generated random characters according to FORMAT.   FORMAT has an alphabet for radix and a digit number for generating, The radix character can be set by 'B'(bin),'D'(dec), 'H'(hex) and 'A'(alphabet) |
| #undef LABEL           | Undefine LABEL by #define and #rand                                                                                                                                                                                     |
| #ifdef LABEL           | If LABEL is defined, then the following is valid until #elif, #else or #endif (Nest depth < 30)                                                                                                                         |
| #ifndef LABEL          | If LABEL is not defined, then following program is valid until #elif, #else or #endif                                                                                                                                   |
| #elif                  | Equal to describing #else and #ifdef                                                                                                                                                                                    |
| #else                  | Reverse condition for #ifdef, #ifndef and #elif                                                                                                                                                                         |
| #endif                 | Terminator for #ifdef, #ifndef, #elif and #else                                                                                                                                                                         |
| #for LABEL             | Duplicate program code until #endfor LABEL times. These cannot be nested.                                                                                                                                               |
| #endfor                | Terminator for #for                                                                                                                                                                                                     |
| #message "STRING"      | Print STRING to the standard output stream                                                                                                                                                                              |
