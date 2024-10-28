# WLP4 Compiler

## Overview of the WLP4 Compiler

This compiler converts WLP4 code into MIPS assembly language by handling various processes, including scanning, parsing, context-sensitive analysis, and code generation. The goal is to fully translate WLP4 programs into MIPS assembly. The source code of this project is private (due to university regulations); please contact mrabee@uwaterloo.ca if you wish to view it.

## What is WLP4?

WLP4 (pronounced "Wool P Four") is a streamlined version of C++ that stands for "Waterloo, Language, Plus, Pointers, Plus, Procedures." It incorporates functions, integers, pointers, arrays, conditionals, and loops, and is taught as part of the ["Foundations of Sequential Programs"](https://www.student.cs.uwaterloo.ca/~cs241) course at the University of Waterloo.

To learn more about WLP4, check out:
- [WLP4 Programming Language Tutorial](https://www.student.cs.uwaterloo.ca/~cs241/wlp4/WLP4tutorial.html)
- [WLP4 Programming Language Specification](https://www.student.cs.uwaterloo.ca/~cs241/wlp4/WLP4.html)

### Compilation Phases:

#### 1) Scanning
The scanning phase tokenizes WLP4 code using a [Simplified Maximal Munch Algorithm](https://en.wikipedia.org/wiki/Maximal_munch). This approach processes input until it cannot continue, determining whether the input is in an accepting state. Tokens are produced when in an accepting state, otherwise, the input is rejected. This step uses a [Nondeterministic Finite Automaton (NFA)](https://en.wikipedia.org/wiki/Nondeterministic_finite_automaton), and the lexical rules can be found [here](https://student.cs.uwaterloo.ca/~cs241/wlp4/WLP4.html).

#### 2) Parsing
Parsing uses a [Pushdown Automaton](https://en.wikipedia.org/wiki/Pushdown_automaton) to identify if the code adheres to a [Context-Free Grammar (CFG)](https://en.wikipedia.org/wiki/Context-free_grammar). The WLP4 context-free syntax is detailed [here](https://student.cs.uwaterloo.ca/~cs241/wlp4/WLP4.html). A successful parse results in a derivation of the input string, forming a parse tree that represents the program's structure. This compiler employs [Bottom-Up Parsing](https://en.wikipedia.org/wiki/Bottom-up_parsing), specifically the [SLR(1) Parser](https://en.wikipedia.org/wiki/Simple_LR_parser).

#### 3) Context-Sensitive Analysis
This phase checks whether the code satisfies WLP4's context-sensitive rules, such as:
- Avoiding multiple declarations of the same variable
- Ensuring variables are used only after declaration

The complete semantic/type-inference rules are outlined [here](https://student.cs.uwaterloo.ca/~cs241/wlp4/typerules.pdf), and the context-sensitive rules are available [here](https://student.cs.uwaterloo.ca/~cs241/wlp4/WLP4.html). The analysis uses the previously generated parse tree to validate adherence to these rules.

#### 4) Code Generation
The final step translates WLP4 code to MIPS assembly language. It supports generating code for main procedures, integer variables, constants, declarations, assignments, arithmetic, control flow, printing, and advanced features like pointers, procedures, and dynamic memory allocation.
