# Assignment 3 – Question 48
## Principles of Compiler Design
### Topic: Implement Symbol Table Tracking for Macro Definitions

---

## Objectives
- Design a symbol table to track macros and their expansions.
- Ensure macro names do not conflict with regular identifiers.
- Handle macro expansion scopes correctly.
- Detect redefinitions or collisions.

---

## Introduction
In this assignment, we implement a **symbol table specifically for macro definitions**.  
Macros are preprocessor directives that define reusable code snippets. Tracking them correctly ensures that macro names do not clash with variables or functions and that expansions occur in the correct scope.  
This helps prevent semantic errors before code generation.

---

## Design / Approach

### 1. Symbol Table Structure
Each entry stores:
- Macro name
- Replacement code (macro body)
- Scope level  

Recommended data structure: **Hash table** or **dictionary**

### 2. Insertion
When a new macro is defined:
- Check if the macro name exists in the **current scope**
- If yes → report a **redefinition error**
- If no → insert the macro into the symbol table

### 3. Lookup
During macro expansion:
- Look up the macro name in the symbol table
- Prefer the **nearest enclosing scope**
- Retrieve the macro body for expansion

### 4. Scope Management
- Push a new scope when entering a file or block
- Pop the scope when exiting
- Ensure macro definitions are valid only within their scope

---

## Pseudocode

```python
# Initialize symbol table
symbol_table = SymbolTable()

# Define a macro
def define_macro(name, body):
    if symbol_table.exists_in_current_scope(name):
        error("Macro already defined in this scope")
    else:
        symbol_table.insert(name, body)

# Expand a macro
def expand_macro(name):
    entry = symbol_table.lookup(name)
    if entry is not None:
        return entry.body
    else:
        error("Macro not found")

# Enter a new scope
def enter_scope():
    symbol_table.push_scope()

# Exit the current scope
def exit_scope():
    symbol_table.pop_scope()

```



## Notes
Inner-scope macros may shadow outer-scope macros.

Macro names should not collide with variables or function identifiers.

This design can be extended to support parameterized macros.

Proper scope handling prevents macro leakage across blocks.

## References
Aho, Lam, Sethi, Ullman – Compilers: Principles, Techniques, Tools

Appel – Modern Compiler Implementation

Tutorialspoint – Compiler Symbol Tables

Compiler design lecture notes