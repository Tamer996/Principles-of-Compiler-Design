# Assignment 3 – Question 48
## Principles of Compiler Design
### Topic: Implement symbol table tracking for macro definitions

---

### Objectives
- Design a symbol table to track macros and their expansions.
- Ensure macro names do not conflict with regular identifiers.
- Handle macro expansion scopes correctly.
- Detect redefinitions or collisions.

---

### Introduction
In this assignment, I implement a **symbol table specifically for macro definitions**.  
Macros are preprocessor directives that define reusable code snippets. Tracking them correctly ensures that macro names do not clash with variables or functions and that expansions happen in the correct scope. This helps prevent semantic errors before code generation.

---

### Design / Approach
1. **Symbol Table Structure**
   - Each entry stores:
     - Macro name
     - Replacement code / body
     - Scope level
   - Recommended data structure: Hash table or dictionary

2. **Insertion**
   - When a new macro is defined:
     - Check if the name exists in the **current scope**
     - If yes → throw error or warning
     - If no → insert into the symbol table

3. **Lookup**
   - To expand a macro:
     - Look up the macro name in the table
     - Use nearest enclosing scope first (block/file scope)
     - Return the replacement body for expansion

4. **Scope Management**
   - Push a new scope when entering a file or block
   - Pop scope when exiting
   - Ensure macro expansions respect the **current active scope**

---

### Pseudocode



symbol_table = new SymbolTable()

def define_macro(name, body):
    if symbol_table.exists_in_current_scope(name):
        error("Macro already defined")
    else:
        symbol_table.insert(name, body)

def expand_macro(name):
    entry = symbol_table.lookup(name)
    if entry is not None:
        return entry.body
    else:
        error("Macro not found")

def enter_scope():
    symbol_table.push_scope()

def exit_scope():
    symbol_table.pop_scope()



### Notes
- Macros can shadow macros from outer scopes; the **inner scope takes precedence**.
- Collisions with variable or function names should be prevented to maintain **semantic correctness**.
- This system can be extended to support **paramete# Assignment 3 – Question 48
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
Macros are preprocessor directives that define reusable code snippets. Tracking them correctly ensures that macro names do not clash with variables or functions, and that expansions happen in the correct scope.  
This helps prevent semantic errors before code generation.

---

## Design / Approach

### 1. Symbol Table Structure
- Each entry stores:
  - Macro name
  - Replacement code / body
  - Scope level
- Recommended data structure: **Hash table** or **dictionary**

### 2. Insertion
- When a new macro is defined:
  - Check if the name exists in the **current scope**
    - If yes → throw an **error** or **warning**
    - If no → insert into the symbol table

### 3. Lookup
- To expand a macro:
  - Look up the macro name in the table
  - Use **nearest enclosing scope first** (block/file scope)
  - Return the replacement body for expansion

### 4. Scope Management
- **Push** a new scope when entering a file or block
- **Pop** scope when exiting
- Ensure macro expansions respect the **current active scope**

---

## Pseudocode

```python
# Initialize symbol table
symbol_table = new SymbolTable()

# Define a macro
def define_macro(name, body):
    if symbol_table.exists_in_current_scope(name):
        error("Macro already defined")
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
rized macros** with arguments.
- Proper scope tracking ensures that macro expansions do not leak outside intended regions.



### References
- Aho, Lam, Sethi, Ullman – *Compilers: Principles, Techniques, Tools*
- Appel – *Modern Compiler Implementation*
- Tutorialspoint – *Compiler Symbol Tables*
- Additional lecture notes and compiler design tutorials
