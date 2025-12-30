# VS Code LaTeX Setup Guide for CV Creation

This guide covers setting up Visual Studio Code as a professional LaTeX CV/Resume creation environment on Windows.

---

## Table of Contents
1. [Prerequisites Installation](#1-prerequisites-installation)
2. [VS Code Extension Setup](#2-vs-code-extension-setup)
3. [Why pdfLaTeX Doesn't Work for CVs](#3-why-pdflatex-doesnt-work-for-cvs)
4. [LaTeX Compilers Comparison](#4-latex-compilers-comparison)
5. [Understanding Tools vs Recipes](#5-understanding-tools-vs-recipes)
6. [Configuring XeLaTeX as Default Compiler](#6-configuring-xelatex-as-default-compiler)

---

## 1. Prerequisites Installation

### 1.1 Install MiKTeX (LaTeX Distribution)

MiKTeX is a LaTeX distribution for Windows that includes all the necessary packages and compilers.

1. Download MiKTeX from: https://miktex.org/download
2. Run the installer and follow the setup wizard
3. Choose **"Install missing packages on-the-fly: Yes"** (recommended)
4. Complete the installation

**Verify Installation:**
```powershell
pdflatex --version
xelatex --version
```

### 1.2 Install Strawberry Perl

Strawberry Perl is required for `latexmk` (the build automation tool used by LaTeX Workshop).

**What is latexmk?**

`latexmk` is a Perl script that **automates the LaTeX build process**:
- Automatically detects which tools are needed (biber, bibtex, makeindex, etc.)
- Runs the correct number of compilation passes until all references are resolved
- Tracks file dependencies and only recompiles what's necessary
- Can watch files and auto-recompile on save

Using `latexmk` is the recommended practice because it handles all the complexity of multi-pass compilation automatically.

**Installation:**

1. Download Strawberry Perl from: https://strawberryperl.com/
2. Run the installer with default settings
3. Restart your terminal/VS Code after installation

**Verify Installation:**
```powershell
perl --version
latexmk --version
```

---

## 2. VS Code Extension Setup

### Install LaTeX Workshop Extension

1. Open VS Code
2. Press `Ctrl+Shift+X` to open Extensions
3. Search for **"LaTeX Workshop"** by James Yu
4. Click **Install**

**Extension Features:**
- Syntax highlighting for `.tex` files
- Auto-compilation on save
- PDF preview (side-by-side or external)
- IntelliSense for LaTeX commands
- Error/warning diagnostics

---

## 3. Why pdfLaTeX Doesn't Work for CVs

### The Problem

When compiling a modern CV template with pdfLaTeX, you may encounter this error:

```
Fatal Package fontspec Error: The fontspec package requires either XeTeX or LuaTeX.

You must change your typesetting engine to,
e.g., "xelatex" or "lualatex" instead of
"latex" or "pdflatex".
```

### The Reason: Font Compatibility

Modern CV templates typically use these packages:

| Package        | Purpose                    | pdfLaTeX Compatible? |
| -------------- | -------------------------- | -------------------- |
| `fontspec`     | Use system fonts (TTF/OTF) | ❌ No                 |
| `fontawesome5` | Professional icons         | ⚠️ Limited            |
| `unicode-math` | Unicode math symbols       | ❌ No                 |

**Why `fontspec` Requires XeTeX/LuaTeX:**

- **pdfLaTeX** uses legacy Type1 fonts and cannot access modern TrueType (TTF) or OpenType (OTF) fonts installed on your system
- **`fontspec`** package is designed to work with system fonts directly, which only XeTeX and LuaTeX engines support
- Professional CVs need custom fonts (like Roboto, Open Sans, etc.) for a polished look

### Common CV Packages That Require XeLaTeX/LuaLaTeX

```latex
\usepackage{fontspec}        % System font access
\usepackage{fontawesome5}    % Icons (LinkedIn, GitHub, etc.)
\usepackage{unicode-math}    % Modern math fonts
```

---

## 4. LaTeX Compilers Comparison

### Overview

| Feature             | pdfLaTeX    | XeLaTeX   | LuaLaTeX  |
| ------------------- | ----------- | --------- | --------- |
| **Speed**           | ⭐⭐⭐ Fastest | ⭐⭐ Medium | ⭐ Slowest |
| **System Fonts**    | ❌ No        | ✅ Yes     | ✅ Yes     |
| **Unicode Support** | ⚠️ Limited   | ✅ Full    | ✅ Full    |
| **Microtype**       | ✅ Full      | ⚠️ Partial | ✅ Full    |
| **Scripting**       | ❌ No        | ❌ No      | ✅ Lua     |
| **Legacy Support**  | ✅ Best      | ✅ Good    | ✅ Good    |

---

### pdfLaTeX

**Pros:**
- Fastest compilation speed
- Most stable and mature engine
- Best compatibility with older packages
- Full `microtype` support (font expansion, protrusion)
- Extensive documentation and community support

**Cons:**
- Cannot use system fonts (TTF/OTF)
- Limited Unicode support (requires `inputenc` package)
- Cannot use `fontspec` package
- Restricted to legacy Type1 fonts

**Best For:** Academic papers, math-heavy documents, legacy templates

---

### XeLaTeX ✓ (Recommended for CVs)

**Pros:**
- Full access to system fonts (TTF/OTF)
- Native Unicode support (UTF-8 by default)
- Works with `fontspec` and `fontawesome5`
- **Faster compilation than LuaLaTeX**
- Good balance of features and speed
- Excellent for multilingual documents

**Cons:**
- Slower than pdfLaTeX
- Partial `microtype` support
- Some legacy packages may not work
- Cannot use `inputenc` package

**Best For:** CVs/Resumes, modern documents, custom fonts, international text

---

### LuaLaTeX

**Pros:**
- Full access to system fonts (TTF/OTF)
- Native Unicode support
- Lua scripting capabilities for advanced automation
- Full `microtype` support
- Most powerful and flexible engine
- Best for very complex typography

**Cons:**
- **Slowest compilation speed** (2-3x slower than XeLaTeX)
- Higher memory usage
- Some packages may have compatibility issues
- Overkill for simple documents

**Best For:** Complex documents, advanced scripting needs, typography-heavy projects

---

### Why Choose XeLaTeX for CV Creation?

| Criteria                 | XeLaTeX            | LuaLaTeX    |
| ------------------------ | ------------------ | ----------- |
| Compilation Speed        | ✅ Faster           | ❌ Slower    |
| Font Support             | ✅ Full             | ✅ Full      |
| CV Package Compatibility | ✅ Excellent        | ✅ Excellent |
| Resource Usage           | ✅ Moderate         | ❌ Higher    |
| Scripting Needs          | Not needed for CVs | Overkill    |

**Conclusion:** XeLaTeX provides all the font capabilities needed for professional CVs while maintaining reasonable compilation speed. LuaLaTeX's additional Lua scripting features are unnecessary for CV creation and only add compilation overhead.

---

## 5. Understanding Tools vs Recipes

In LaTeX Workshop, **Tool** and **Recipe** are different concepts:

| Term       | What it is                     | Example                                     |
| ---------- | ------------------------------ | ------------------------------------------- |
| **Tool**   | A single compiler/command      | `xelatex`, `pdflatex`, `biber`, `bibtex`    |
| **Recipe** | A sequence of tools to execute | `xelatex` → `biber` → `xelatex` → `xelatex` |

### Why Recipes Exist

Some documents require **multiple compilation passes** to resolve all references:

**Simple CV (1 pass):**
```
xelatex  →  PDF done ✓
```

**Document with Bibliography (4 passes):**
```
xelatex  →  biber  →  xelatex  →  xelatex  →  PDF done ✓
   ↓          ↓          ↓            ↓
Creates    Processes   Inserts     Fixes
.aux file  citations   bibliography references
```

### How They Work in settings.json

```json
{
  "latex-workshop.latex.tools": [
    { "name": "xelatex", "command": "xelatex", ... },  // Tool 1: Compiler
    { "name": "biber", "command": "biber", ... }       // Tool 2: Bibliography processor
  ],
  "latex-workshop.latex.recipes": [
    {
      "name": "xelatex",                              // Simple recipe (1 tool)
      "tools": ["xelatex"]
    },
    {
      "name": "xelatex + biber",                      // Complex recipe (4 tools)
      "tools": ["xelatex", "biber", "xelatex", "xelatex"]
    }
  ]
}
```

### For CV Creation

Since CVs typically don't have bibliographies, a simple single-pass recipe with just `xelatex` is sufficient.

---

## 6. Configuring XeLaTeX as Default Compiler

### Option 1: Using Extension Sidebar

You can select a compiler directly from the LaTeX Workshop extension panel:

1. Open the **LaTeX** panel in VS Code's sidebar (click the TeX icon)
2. Expand **COMMANDS** → **Build LaTeX project**
3. Choose from available recipes:
   - `Recipe: latexmk (xelatex)` ✓ Recommended
   - `Recipe: latexmk (lualatex)`
   - `Recipe: latexmk`
   - etc.

> [!Note]
> The full recipe list is only visible when no default compiler is set in `settings.json`. If you have configured a default recipe in settings, only that recipe will appear.

![](assets/Screenshot%202025-12-30%20144015.png)
![](assets/Screenshot%202025-12-30%20143908.png)

---

### Option 2: Workspace Settings (Recommended)

Create or edit `.vscode/settings.json` in your project folder:

```json
{
  "latex-workshop.latex.recipe.default": "latexmk (xelatex)",
  "latex-workshop.latex.tools": [
    {
      "name": "latexmk (xelatex)",
      "command": "latexmk",
      "args": [
        "-xelatex",
        "-synctex=1",
        "-interaction=nonstopmode",
        "-file-line-error",
        "%DOC%"
      ]
    }
  ],
  "latex-workshop.latex.recipes": [
    {
      "name": "latexmk (xelatex)",
      "tools": ["latexmk (xelatex)"]
    }
  ]
}
```

> **Note:** Using `latexmk` is the recommended approach as it automatically handles multi-pass compilation when needed (e.g., for bibliographies, cross-references).

---

### Settings Explanation

| Setting                               | Purpose                                    |
| ------------------------------------- | ------------------------------------------ |
| `latex-workshop.latex.recipe.default` | Sets the default build recipe              |
| `latex-workshop.latex.tools`          | Defines available compilation tools        |
| `latex-workshop.latex.recipes`        | Defines build recipes (sequences of tools) |

**Tool Arguments Explained:**

| Argument                   | Purpose                                                    |
| -------------------------- | ---------------------------------------------------------- |
| `-xelatex`                 | Tells latexmk to use XeLaTeX engine                        |
| `-synctex=1`               | Enables PDF-source synchronization (Ctrl+Click navigation) |
| `-interaction=nonstopmode` | Continues compilation without stopping for errors          |
| `-file-line-error`         | Shows file name and line number in error messages          |
| `%DOC%`                    | Placeholder for the document name                          |

---

## Quick Start Checklist

- [ ] Install MiKTeX
- [ ] Install Strawberry Perl
- [ ] Install LaTeX Workshop extension in VS Code
- [ ] Create `.vscode/settings.json` with XeLaTeX configuration
- [ ] Save your .tex file to trigger compilation
- [ ] View PDF with `Ctrl+Alt+V` or side panel

---

## Troubleshooting

### "latexmk not found"
- Ensure Strawberry Perl is installed
- Restart VS Code after Perl installation

### "fontspec requires XeTeX or LuaTeX"
- Configure settings.json as shown above

### Missing packages during compilation
- MiKTeX will auto-install missing packages (if enabled)
- Or run: `miktex-console` and update packages manually

---

## References

- [Install LaTeX Workshop and compile PDF in VSCode LaTeX (Windows)](https://youtu.be/4lyHIQl4VM8)
- [MiKTeX Documentation](https://miktex.org/howto)
- [LaTeX Workshop Wiki](https://github.com/James-Yu/LaTeX-Workshop/wiki)
- [fontspec Package Documentation](https://ctan.org/pkg/fontspec)
- [Overleaf latex documentation](https://www.overleaf.com/learn/latex/Learn_LaTeX_in_30_minutes)
---

*Last Updated: December 2025*
