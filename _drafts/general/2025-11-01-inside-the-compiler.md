---
layout: post
title: "Inside the Compiler"
date: 2025-11-01
category: compiler
author: BrassinAI
excerpt: "How source code is transformed into optimized machine instructions - from lexical analysis to SSA form."
---

This article explains how source code is transformed into optimized machine instructions. We'll touch on lexical analysis, syntax trees, intermediate representations (IR), and static single assignment (SSA).

{% include toc.html %}

## The Compilation Pipeline

A typical compiler follows these stages:

```
Source Code → Lexer → Parser → AST → IR → Optimizer → Code Gen → Machine Code
```

### 1. Lexical Analysis (Lexer)

The lexer breaks raw source text into **tokens** - the atomic units of the language:

```
int x = 42;
→ [INT, IDENT("x"), ASSIGN, NUM(42), SEMICOLON]
```

### 2. Parsing

The parser arranges tokens into an **Abstract Syntax Tree (AST)** that captures the program's hierarchical structure.

### 3. Intermediate Representation (IR)

IR is a compiler's internal language - simpler than source code but richer than machine code. LLVM IR is a popular example:

```llvm
define i32 @add(i32 %a, i32 %b) {
  %result = add i32 %a, %b
  ret i32 %result
}
```

## Static Single Assignment (SSA)

SSA is a property of IR where **every variable is assigned exactly once**. This simplifies many optimizations:

- **Constant propagation** - replacing variables with known constants
- **Dead code elimination** - removing unreachable or unused code
- **Register allocation** - mapping virtual registers to hardware registers

> Compilers are the ultimate translators between human and machine - efficient, precise, and ever-evolving.

## Key Optimizations

| Optimization | What It Does |
|-------------|--------------|
| Inlining | Replaces function calls with the function body |
| Loop unrolling | Reduces loop overhead by duplicating the loop body |
| Vectorization | Uses SIMD instructions for data-parallel operations |
| Tail call optimization | Converts recursive calls into loops |

## Going Deeper

Future articles will cover:

- Writing a toy compiler from scratch
- LLVM pass infrastructure
- JIT compilation and runtime optimization
- Profile-guided optimization (PGO)
