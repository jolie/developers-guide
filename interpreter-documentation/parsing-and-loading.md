# Parsing and Loading

This document describes the sequence of stages in the parsing and loading process of Jolie programs.

## Process

We describe the stages of the process in the following list. ERROR is an unrecoverable error that the user should be notified of.

1. A ModuleParser is created to parse the main program module \(file\). ModuleParser is described later on the document.
2. A SymbolTableGenerator is called on the AST from the previous step to generate its symbol table. See below for what a symbol table is.
3. ModuleCrawler is called on the symbol table from the previous stage. It stores a list of module names \(the modules that we still have to parse\) and a map from absolute module URIs to AST and symbol table \(the modules that we have parsed already\).

   1. The list is initialised with all modules mentioned by the column "Scope" in the symbol table of the main program \(given as initial input\).
   2. The map is initialised with the name of the program module \(probably "." ?\) mapped to the initial AST given as input from the previous stage.
   3. A loop is entered:
      1. If there is a module name in the list, take it out of the list, otherwise exit the loop.
      2. If the map does not contain a mapping for that module name, then:
         1. Find the module using a ModuleFinder. If no module can be found, ERROR.
         2. Use a ModuleParser to parse the found module.
         3. Use a SymbolTableGenerator to generate the symbol table from the AST of the previous step.
         4. Store the result of the previous two steps in the map.
         5. For each import statement mentioned in the AST of the module that has just been parsed: if the module mentioned by the import statement is not in the map's keys, add it to the list \(since we'll have to parse it later on\).

   When this stage is completed, we have the AST and the symbol table of each module that we are going to need.

4. GlobalSymbolReferenceResolver is now called on each module AST \(including the main one\), to resolve all symbol references \(type links, interfaces, etc.\). This happens in two phases.
   1. In phase 1, the symbol table of each module is visited such that: for each symbol S1 with scope "external\(M, S2\)", S2 is found in the symbol table of M and the pointer of S1 is set to the pointer of S2. If S2 has no pointer, ERROR.
   2. In phase 2, the AST of each module is visited such that:
      1. The AST is visited to find all references, e.g., TypeDefinitionLink.
      2. The reference node that refers to symbol S, e.g., a TypeDefinitionLink referring to "S", is now resolved by pointing to the pointer given by the symbol table for S. If the symbol is not found in the symbol table, ERROR.
5. The Interpreter can now call OOITBuilder on the AST of the main module.

## ModuleParser

ModuleParser parses a module \(a Jolie file\).

1. First, it uses OLParser to get an AST.
2. Second, it uses OLParseTreeOptimizer to optimize the AST.

ModuleParser **does not resolve references for any symbol**. The following are a few relevant examples:

1. Import statements are not resolved, e.g., from M import S is just parsed as an AST node called ImportStatement that contains the module name M and the symbol S.
2. Type links are not resolved \(not even for operation declarations\).
3. Calls to procedure definitions are not resolved, as in the current implementation.
4. References to interfaces within output ports.

## SymbolTable

A symbol table \(SymbolTable\) is a data structure that maps symbols to their scope and AST nodes: Map&lt; String, SymbolInfo &gt;. Class SymbolInfo has three fields:

* scope: can be either "local" or "external\(M,S\)", where M is a module and S a symbol name. \(Thus, scope is implemented as an enum with two cases.\) Local means that the symbol is defined within the module of this symbol table; external\(M,S\) means that this symbol is actually defined in module M as symbol S. For example, if a module has an import statement "from fibo import F as MyF", then the symbol table for such module will contain an entry for MyF with scope external\(fibo, F\).
* pointer: a reference to the OLSyntaxNode that defines the symbol.

