+++
title = "GSOC 2025 Submission for GRAME: faustlsp"
date = 2025-05-15T00:00:00Z
period = "May 2025 – Sep 2025"
summary = "Language Server Protocol (LSP) implementation for Faust audio DSP language with Tree-Sitter AST parsing in Go, plus a VS Code extension with Topiary Rust formatting."
tags = ["Go", "Rust", "TypeScript", "Tree-Sitter", "LSP", "GSoC"]
aliases = ["/experience/grame/"]
+++

> **Official GSoC 2025 Submission Gist:**  
> [https://gist.github.com/carn181/0e953b5463de9f528ff58183d55fcfdc](https://gist.github.com/carn181/0e953b5463de9f528ff58183d55fcfdc)

---

### Project Summary

The primary objective of this project was to enhance the developer experience for the **Faust** programming language by creating a suite of three interconnected tools:
1. **`faustlsp`**: An LSP (Language Server Protocol) server.
2. **VS Code Client Extension**: Dedicated editor integration.
3. **`faustfmt`**: A standalone, high-performance code formatter.

These tools aim to provide modern IDE features such as real-time diagnostics, intelligent code completion, hover documentation, and consistent code formatting, thereby making Faust development more efficient and enjoyable.

---

### Summary of Coding and Development

The project was structured into three distinct development phases:

1. **Foundational Parser Work (`tree-sitter-faust`):**  
   The initial phase focused on the foundational component: the `tree-sitter-faust` parser. This involved extensive work to improve the parser's robustness, ensuring it could accurately and completely parse all valid Faust syntax. This step was crucial as the entire project relies on a perfectly parsed Abstract Syntax Tree (AST) to function correctly. *(First ~2 weeks)*

2. **Core Applications Architecture:**  
   - **LSP Server (`faustlsp`):** Built from the ground up in **Go**, chosen for its strong concurrency primitives and performance, which are well-suited for a server handling multiple concurrent requests.
   - **VS Code Extension:** Developed in **TypeScript** to seamlessly integrate with the VS Code API.
   - **Code Formatter (`faustfmt`):** Implemented as a standalone command-line tool in **Rust**, leveraging its performance and memory safety for efficient code manipulation.

3. **LSP Features & Refinement:**  
   The final and most extensive phase was dedicated to implementing and refining the planned LSP features. This involved building core logic in Go to handle JSON-RPC requests, integrating `tree-sitter` and the native Faust compiler for code analysis and error reporting, and implementing features like code completion, syntax error detection, and `Goto Definition`.

---

### Achieved Goals

#### 1) `faustlsp` (LSP Server)
* **Repository:** [github.com/carn181/faustlsp](https://github.com/carn181/faustlsp)

The LSP server currently operates on both Linux and macOS with the following features:
- **Diagnostics:** Provides real-time syntax errors (detected via `tree-sitter-faust`) and compiler errors (reported by native Faust compiler on line 1).
- **Document Symbols:** Provides hierarchical symbol structure of Faust files for document outlines, breadcrumbs, and code-folding.
- **Formatting:** Rapid and consistent code formatting via `faustfmt`.
- **Goto Definition:** Quickly navigates to symbol definitions across the current file or external libraries.
- **Hover Documentation:** Analyzes comments directly preceding symbol definitions and renders them as hover documentation.
- **Code Completion:** Identifies valid symbols at cursor position for auto-completion suggestions.

#### 2) VS Code Extension
* **Repository:** [github.com/carn181/vscode-faust](https://github.com/carn181/vscode-faust)

Serves as the client interface layer, sending LSP requests to `faustlsp` and displaying responses in VS Code. *(See also [Kamil Kisiel's fork](https://github.com/kisielk/vscode-faust) adding WASM compilation and interactive block diagrams).*

#### 3) `faustfmt` (Faust Code Formatter)
* **Repository:** [github.com/carn181/faustfmt](https://github.com/carn181/faustfmt)

Standalone command-line tool written in Rust. Parses Faust source files and formats contents according to `tree-sitter` style rules.

---

### Goals Not Achieved

- **Find References:** The only planned feature not implemented was *Find References*. Due to `tree-sitter` ASTs lacking built-in scope information, implementing an algorithm to reliably locate all symbol references across complex scopes extended beyond the project timeline.

---

### Possible Future Improvements

- **Improved Documentation:** Make documentation across all components more comprehensive for new users.
- **Improved Formatting:** Expand `faustfmt` query rules for complex Faust expressions and constructs.
- **Windows Support:** Extend `faustlsp` to support the Windows operating system.
- **VS Code Integration:** Contribute directly to official `vscode-faust` extension main branch.
- **Enhanced Stability:** Address edge-case mutex lock issues under heavy edit traffic.
- **Compiler File-Include Integration:** Improve support for files passed directly to the Faust compiler.
- **Better Document Symbols:** Expand document symbol reporting for environments and iterations.
- **Bugfixes through Better Testing:** Implement automated LSP end-to-end testing cycles.

---

### Lessons Learned

- **Parser Limitations:** While `tree-sitter` is powerful and accessible, hand-written parsers offer superior flexibility for domain-specific language behavior.
- **Importance of Logging:** Since LSP features are difficult to test with traditional unit tests, comprehensive logging proved essential for debugging JSON-RPC client-server communication.
- **Go Tooling:** Go's concurrency model simplified multi-client request handling, and clean error handling made modifying the codebase straightforward.

---

### Acknowledgements

Special thanks to my GSoC mentors **Thomas Rushton**, **Karl Hiner**, and **Stéphane Letz** for their guidance and support, **Kamil Kisiel** for testing assistance, and the **Faust & GRAME community** for their encouragement.
