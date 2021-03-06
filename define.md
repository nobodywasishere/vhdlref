---
layout: page
title: Definitions
nav_order: 0
---

<!-- {: .todo }
Change this to follow the new layout -->

# Definitions

Analysis
: The syntax checking and compilation of a VHDL design into a design library

Architecture
: A library unit associated with an entity which describes its internal operation or organization

Component
: A definition of the interface to a sub-module, rather like a "socket", to which an entity may be bound

Concurrent Statements
: Statements within an architecture which execute concurrently, independently of their order

Configuration
: Defines the "binding" of each component instance to an entity, and each entity to an architecture; can be defined using a configuration library unit or from within an architecture

Design File
: A text file containing source code for one or more design units

Design Library
: A data structure containing analyzed design units (library units)

Design Unit
: A VHDL module contained in a design file, consisting of the source code for a library unit preceded by any required Library or Use clauses; analysis of a design unit defines the corresponding library unit in a design library

Elaboration
: The building of a simulatable model through the top-down binding of its structural hierarchy, according to the configuration selected

Entity
: A library unit which describes the external interface of a hardware module

Function
: A group of sequential statements which can be "called" from different places in a model, reading one or more input parameters and returning a single value

Library Unit
: An analysed design unit; the five types of library units are: entity, architecture, package, package body and configuration

Overloading
: The definition of multiple functions or procedures with the same name, which operate on different parameter combinations or types

Package
: A primary unit containing a collection of declarations and/or specifications which may be used in other library units

Package Body
: A secondary unit associated with a package, whose main purpose is to contain the full code for any functions or procedures which have been declared in the associated package

Primary Unit
: A library unit which can exist in a design library; the primary design units are entity, package and configuration

Procedure
: A group of sequential statements which can be "called" from different places in a model. It may have parameters of modes in, out, or inout

Process
: A concurrent statement which contains a collection of sequential statements, and which can interact concurrently with other concurrent statements

Resolution
: The determination of the value of a signal when it is simultaneously driven by more than one source

Scope
: The region of VHDL code within which a declared item (e.g. a constant) may be used

Secondary Unit
: A library unit which defines a body associated with a primary unit which has already been analyzed into the same design library; the secondary units are architecture (associated with entity) and package body (associated with package)

Sequential Statements
: Statements which are executed in the order they are written, as with "conventional" software languages

<!-- Generated using https://www.tablesgenerator.com/markdown_tables -->

<!-- <table class="define">
    <thead>
        <tr>
            <th>Word/Phrase</th>
            <th>Definition</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Analysis</td>
            <td>The syntax checking and compilation of a VHDL design into a design library.</td>
        </tr>
        <tr>
            <td>Architecture</td>
            <td>A library unit associated with an entity which describes its internal operation or organisation. Multiple architectures may be defined for a single entity</td>
        </tr>
        <tr>
            <td>Component</td>
            <td>A definition of the interface to a sub-module, rather like a "socket", to which an entity may later be bound.</td>
        </tr>
        <tr>
            <td>Concurrent Statements</td>
            <td>Statements within an architecture which execute concurrently in simulated time, independently of their order.</td>
        </tr>
        <tr>
            <td>Configuration</td>
            <td>Defines the "binding" of each component instance to an entity, and each entity to an architecture. Can be defined using a configuration library unit or from within an architecture.</td>
        </tr>
        <tr>
            <td>Design File</td>
            <td>A text file containing source code for one or more design units.</td>
        </tr>
        <tr>
            <td>Design Library</td>
            <td>A data structure containing analysed design units (library units).</td>
        </tr>
        <tr>
            <td>Design Unit</td>
            <td>A VHDL module contained in a design file, consisting of the source code for a library unit preceded by any required Library or Use clauses. Analysis of a design unit defines the corresponding library unit in a design library. </td>
        </tr>
        <tr>
            <td>Elaboration</td>
            <td>The building of a simulateable model through the top-down binding of its structural hierarchy, according to the configuration selected. </td>
        </tr>
        <tr>
            <td>Entity</td>
            <td>A library unit which describes the external interface of a hardware module.</td>
        </tr>
        <tr>
            <td>Function</td>
            <td>A group of sequential statements which can be "called" from different places in a model, reading one or more input parameters and returning a single value. </td>
        </tr>
        <tr>
            <td>Library Unit</td>
            <td>An analysed design unit. The five types of library unit are: entity, architecture, package, package body and configuration. </td>
        </tr>
        <tr>
            <td>Overloading</td>
            <td>The definition of multiple functions or procedures with the same name, which operate on different parameter combinations or types. </td>
        </tr>
        <tr>
            <td>Package</td>
            <td>A primary unit containing a collection of declarations and/or specifications which may be used in other library units. </td>
        </tr>
        <tr>
            <td>Package Body</td>
            <td>A secondary unit associated with a package, whose main purpose is to contain the full code for any functions or procedures which have been declared in the associated package. It may also contain declarations and specifications which
                are explained in the Reference Guide section of this document. </td>
        </tr>
        <tr>
            <td>Primary Unit</td>
            <td>a library unit which can exist in a design library. The primary design units are entity, package and configuration. </td>
        </tr>
        <tr>
            <td>Procedure</td>
            <td>A group of sequential statements which can be "called" from different places in a model. It may have parameters of modes in, out or inout.</td>
        </tr>
        <tr>
            <td>Process</td>
            <td>A concurrent statement which contains a collection of sequential statements and which can interact concurrently with other concurrent statements.</td>
        </tr>
        <tr>
            <td>Resolution</td>
            <td>The determination of the value of a signal when it is simultaneously driven by more than one source.</td>
        </tr>
        <tr>
            <td>Scope</td>
            <td>The region of VHDL code within which a declared item (e.g. a constant) may be used</td>
        </tr>
        <tr>
            <td>Secondary Unit</td>
            <td>A library init which defines a body associated with a primary unit which has already been analysed into the same design library. The secondary units are architecture (associated with entity) and package body (associated with package).
            </td>
        </tr>
        <tr>
            <td>Sequential Statements</td>
            <td>Statements which are executed in the order they are written, as with "conventional" software languages. </td>
        </tr>
    </tbody>
</table>
-->
