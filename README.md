# Compiler Design Project - Combined Repository Summary

This repository integrates **five incremental assignments** from the course *Introduction to Compiler Design* by **Prof. Yi-Ping You**. Each assignment builds upon the previous one to ultimately create a full compiler for the **P programming language**, progressing from lexical analysis to RISC-V code generation.

## Repository Structure

Each subdirectory is a Git submodule pointing to the original standalone assignment repository:

```
.
├── assignment1-lexical       # Lexical analysis (scanner using lex/flex)
├── assignment2-parser        # Syntax analysis (parser using yacc/bison)
├── assignment3-ast           # AST construction using flex + bison + C/C++
├── assignment4-semantics     # Semantic analysis + Symbol table
├── assignment5-codegen       # RISC-V code generation
```

To initialize all submodules:

```bash
git submodule update --init --recursive
```

---

## Assignment 1 - Lexical Analysis (Scanner)

* **Goal**: Implement a scanner using lex (flex) to tokenize the P language.
* **Key Features**:

  * Recognizes tokens: identifiers, keywords, constants, operators, delimiters
  * Handles whitespaces, comments, pseudocomments
  * Supports pseudocomment options `//&S+/-` and `//&T+/-`
  * Error handling for illegal characters
* **Example Input**:

  ```p
  var x: integer;
  print "Hello World!";
  ```

  **Output**: formatted token stream with source listing

---

## Assignment 2 - Syntax Analysis (Parser)

* **Goal**: Write a parser using yacc (bison) for the P language based on provided grammar rules
* **Key Features**:

  * Implements full LALR(1) grammar
  * Recognizes P program structure, functions, statements, and expressions
  * Integrates with scanner from Assignment 1
  * Produces syntax error messages with line info
* **Options**: `--src` and `--tok` to control listing output
* **Sample Output on Success**:

  ```
  |--------------------------------|
  |  There is no syntactic error!  |
  |--------------------------------|
  ```

---

## Assignment 3 - AST Construction

* **Goal**: Construct an Abstract Syntax Tree (AST) from the parsed input
* **Key Features**:

  * Defines C/C++ AST node classes (e.g., ProgramNode, PrintNode, etc.)
  * Stores syntactic and semantic attributes
  * Uses visitor pattern to traverse and dump the AST
  * Prints AST with pre-order traversal on `--dump-ast`
* **Bonus**: Implements visitor pattern for AST dumping

---

## Assignment 4 - Semantic Analysis

* **Goal**: Perform semantic checks and symbol table management
* **Key Features**:

  * Builds symbol tables scoped by program/function/block
  * Checks: redeclarations, type compatibility, function argument matching, etc.
  * Implements scope rules, constant/loop var constraints, coercion rules
  * Dumps symbol tables when `//&D+` is used
  * Prints detailed semantic errors with line and column info
* **Success Output**:

  ```
  |---------------------------------------------------|
  |  There is no syntactic error and semantic error!  |
  |---------------------------------------------------|
  ```

---

## Assignment 5 - Code Generation

* **Goal**: Generate RISC-V assembly code from AST
* **Key Features**:

  * Targets integer-only subset of P language (no arrays, strings by default)
  * Follows stack-based instruction model
  * Translates variables, assignments, expressions, function calls, control flow
  * Emits `.S` files compatible with Spike simulator
  * Uses templates for prologue/epilogue and supports `--save-path` option
* **Bonus**: Adds support for boolean, array, string, and real types

---

## How to Use This Repository

### Build and Test Each Assignment

Each assignment is self-contained:

```bash
cd assignmentX-*
make            # build using provided Makefile
make test       # run test cases
```

### Docker

Each assignment includes a Makefile target:

```bash
make docker-pull
./activate_docker.sh
```

---

## Reference

* [Yi-Ping You, NYCU](https://www.cs.nycu.edu.tw/people/bio.php?PID=16)
* RISC-V ISA: [https://riscv.org/](https://riscv.org/)
* Spike Simulator: [https://github.com/riscv/riscv-isa-sim](https://github.com/riscv/riscv-isa-sim)
* Docker: Used for unified build environment across assignments

---

## License & Acknowledgments

* Course Material and Specifications: Copyright © Prof. Yi-Ping You
* Assignment Source Repositories: \[individual private repositories, now linked as submodules]
