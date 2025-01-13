---
title: Es Module
description: 
published: true
date: 2025-01-13T10:02:55.086Z
tags: 
editor: markdown
dateCreated: 2025-01-07T22:30:48.817Z
---

In the real world, we often deal with thousands of functions and variables. Organizing and managing these can quickly become overwhelming.

- **Simpler with Few Variables**: When dealing with just a few variables, development is straightforward and manageable.
- **Focused Development**: While working on one function, you can focus exclusively on that function without worrying about unrelated parts of the code.

However, as the complexity of your application grows, relying on this approach becomes increasingly unmanageable. Sharing variables across functions without clear boundaries introduces challenges, especially when everything lives in the global scope.

# Old Way Before Modules

- **Downside**: In JavaScript, functions cannot access variables defined inside other functions.
- A common workaround is to share variables by placing them in a higher scope, such as the global scope.

## Problems with the Old Way

- **Script Order**: All `<script>` tags must be in the correct order.
- **Global Scope Issues**: Any function can access or modify global variables, potentially causing unexpected issues.

| ![js_sharing_global_scope.png](/javascript/js_sharing_global_scope.png) | ![js_global_scope_issue.png](/javascript/js_global_scope_issue.png) |

  
## Solution: ES Modules

![es_module_scope.png](/javascript/es_module_scope.png)

- ES Modules offer a better way to organize variables and functions.
- **Module Scope**: Functions and variables within a module are shared only within that module.
- **Exports and Imports**: Explicitly export variables or functions to make them accessible to other modules.
- This explicit relationship helps identify which modules depend on each other, simplifying debugging and maintenance.

## How ES Modules Work

  1. **Dependency Graph**: Modules are linked through imports, forming a dependency graph.

2. **Entry Point**: A designated file serves as the graph's entry point.

3. **Parsing**: The browser parses these files into **Module Records** (data structures).

4. **Instantiation**: Module Records are converted into **Module Instances**, which include both code and state.
  

![es_three_phases.png](/javascript/es_three_phases.png)

## ES Module Specifications


- The **[ES Module Spec](https://tc39.github.io/ecma262/#sec-modules)** defines:
  - How to parse files into Module Records.
  - How to instantiate and evaluate these modules.
- The spec does **not** dictate how files are fetched. 
  - For browsers, file fetching is defined in the **[HTML Spec](https://html.spec.whatwg.org/#fetch-a-module-script-tree)**.

## Lazy Loading with Dynamic Imports

- Use [dynamic imports](https://github.com/tc39/proposal-dynamic-import) like `import(`${path}/foo.js`)`.
- Dynamically imported files serve as entry points for separate dependency graphs.
- These graphs are processed independently from the main graph.

## CommonJS Overview

- **Usage**: Relies on `require()` for module imports.
- **Behavior**:
  - CommonJS operates efficiently with file systems, blocking the main thread to load files.
  - It processes the entire dependency tree (loading, instantiating, evaluating) before returning the module instance.

### CommonJS vs. ES Modules

- **Memory Sharing**: 
  - ES Modules use **live bindings**, so both modules reference the same memory location.
  - CommonJS creates a **copy** of the exported values.
- **Updates**:
  - In ES Modules, changes to an exported value in one module are reflected in the importing module.
  - CommonJS does not reflect such updates dynamically.
## References
- [ES Modules: A Cartoon Deep-Dive](https://hacks.mozilla.org/2018/03/es-modules-a-cartoon-deep-dive/)