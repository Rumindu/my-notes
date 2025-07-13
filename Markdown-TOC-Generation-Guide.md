# Markdown Table of Contents (TOC) Generation Guide
<!-- no toc -->

## 📋 Table of Contents
- [Markdown Table of Contents (TOC) Generation Guide](#markdown-table-of-contents-toc-generation-guide)
  - [📋 Table of Contents](#%F0%9F%93%8B-table-of-contents)
  - [🎯 Problem Statement](#%F0%9F%8E%AF-problem-statement)
  - [📚 Markdown All in One Extension Overview](#%F0%9F%93%9A-markdown-all-in-one-extension-overview)
    - [Basic TOC Generation](#basic-toc-generation)
    - [Configuration Options](#configuration-options)
    - [Available slugifyMode Options](#available-slugifymode-options)
  - [⚠️ The %20 Spacing Challenge](#%E2%9A%A0%EF%B8%8F-the-20-spacing-challenge)
    - [Problem Description](#problem-description)
    - [Why Standard Settings Don't Work](#why-standard-settings-dont-work)
    - [Attempted Solutions](#attempted-solutions)
  - [💡 Workaround Solutions](#%F0%9F%92%A1-workaround-solutions)
    - [Solution 1: Disable Auto-Update](#solution-1-disable-auto-update)
    - [Solution 2: Use `<!-- no toc -->` Comment](#solution-2-use----no-toc----comment)
    - [Solution 3: Post-Processing with sed Command](#solution-3-post-processing-with-sed-command)
    - [Solution 4: Custom Python Script](#solution-4-custom-python-script)
    - [Solution 5: VS Code Tasks for Automation](#solution-5-vs-code-tasks-for-automation)
    - [Solution 6: Find and Replace with Regex](#solution-6-find-and-replace-with-regex)
    - [Solution 7: Keyboard Shortcut for Quick Conversion](#solution-7-keyboard-shortcut-for-quick-conversion)
  - [🔧 Alternative Extensions](#%F0%9F%94%A7-alternative-extensions)
    - [Markdown TOC Extension](#markdown-toc-extension)
    - [Markdown Preview Enhanced](#markdown-preview-enhanced)
  - [📝 Settings Configuration](#%F0%9F%93%9D-settings-configuration)
    - [VS Code settings.json Configuration](#vs-code-settingsjson-configuration)
    - [Troubleshooting Settings](#troubleshooting-settings)
  - [🎯 Best Practices](#%F0%9F%8E%AF-best-practices)
  - [🔮 Future Considerations](#%F0%9F%94%AE-future-considerations)
  - [📖 References](#%F0%9F%93%96-references)
  - [🚨 Common Pitfalls and Solutions](#%F0%9F%9A%A8-common-pitfalls-and-solutions)
    - [Issue 1: Over-Encoding with Emojis](#issue-1-over-encoding-with-emojis)
    - [Issue 2: Special Characters Breaking Links](#issue-2-special-characters-breaking-links)
    - [Issue 3: Nested List Indentation](#issue-3-nested-list-indentation)
    - [Issue 4: Case Sensitivity Issues](#issue-4-case-sensitivity-issues)
  - [🔍 Testing and Validation](#%F0%9F%94%8D-testing-and-validation)
    - [Verify Links Work Correctly](#verify-links-work-correctly)
    - [Validation Script](#validation-script)
    - [Cross-Platform Compatibility](#cross-platform-compatibility)
  - [🛠 Advanced Configuration](#%F0%9F%9B%A0-advanced-configuration)
    - [Workspace-Specific Settings](#workspace-specific-settings)
    - [Git Hooks for Consistency](#git-hooks-for-consistency)
    - [EditorConfig for Markdown](#editorconfig-for-markdown)
  - [📊 Comparison Matrix](#%F0%9F%93%8A-comparison-matrix)
  - [🎯 Quick Reference Cheat Sheet](#%F0%9F%8E%AF-quick-reference-cheat-sheet)
    - [Emergency Fix (2 minutes)](#emergency-fix-2-minutes)
    - [VS Code Commands](#vs-code-commands)
    - [Settings to Remember](#settings-to-remember)
    - [Test Your Links](#test-your-links)
  - [🤔 Decision Tree: Which Solution to Choose?](#%F0%9F%A4%94-decision-tree-which-solution-to-choose)

---

## 🎯 Problem Statement

When generating Table of Contents (TOC) in Markdown files using VS Code extensions, the default behavior replaces spaces in headings with hyphens (`-`) in the anchor links. However, some use cases require spaces to be replaced with `%20` (URL encoding) instead.

**Example of the issue:**
- **Desired**: `[Spring Boot CRUD Application](#spring%20boot%20crud%20application)`
- **Default**: `[Spring Boot CRUD Application](#spring-boot-crud-application)`

---

## 📚 Markdown All in One Extension Overview

The "Markdown All in One" extension is the most popular TOC generator for VS Code with the following features:

### Basic TOC Generation

1. **Command**: Run "Create Table of Contents" from Command Palette (`Ctrl+Shift+P`)
2. **Auto-Update**: TOC updates automatically on file save (configurable)
3. **Indentation**: Supports both tabs and spaces

### Configuration Options

```json
{
  "markdown.extension.toc.updateOnSave": true,
  "markdown.extension.toc.levels": "2..6",
  "markdown.extension.toc.slugifyMode": "github",
  "markdown.extension.list.indentationSize": "adaptive"
}
```

### Available slugifyMode Options

| Mode     | Behavior                        | Example Output                        |
| -------- | ------------------------------- | ------------------------------------- |
| `github` | GitHub-style slugs with hyphens | `#spring-boot-crud-application`       |
| `vscode` | VS Code-style with URL encoding | `#spring%20boot%20crud%20application` |
| `gitlab` | GitLab-style slugs              | `#spring-boot-crud-application`       |

---

## ⚠️ The %20 Spacing Challenge

### Problem Description

When trying to generate TOC links with `%20` for spaces instead of `-`, several issues arise:

1. **Setting `slugifyMode: "vscode"`** should theoretically work but often produces unexpected results
2. **Emoji handling**: Complex characters get over-encoded (e.g., `#%F0%9F%93%8B-table-of-contents`)
3. **Auto-regeneration**: Manual changes get overwritten when the extension auto-updates

### Why Standard Settings Don't Work

The extension's `slugifyMode` options are designed for compatibility with specific platforms:
- `github`: Optimized for GitHub's anchor link format
- `vscode`: Intended for VS Code's internal linking, not necessarily `%20` formatting
- `gitlab`: Optimized for GitLab's anchor link format

### Attempted Solutions

1. **Changed slugifyMode to "vscode"**:
   ```json
   "markdown.extension.toc.slugifyMode": "vscode"
   ```
   **Result**: Generated complex encoded strings instead of simple `%20`

2. **Manual replacement**:
   - Manually replaced `-` with `%20`
   - **Problem**: Extension auto-reverted changes on save

---

## 💡 Workaround Solutions

### Solution 1: Disable Auto-Update

**Best for**: Files where you want manual control over TOC

```json
{
  "markdown.extension.toc.updateOnSave": false
}
```

**Steps**:
1. Add the setting to `settings.json`
2. Generate TOC using "Create Table of Contents" command
3. Manually replace `-` with `%20` in the generated TOC
4. Save file (TOC won't auto-regenerate)

**Pros**: ✅ Gives full control over TOC format  
**Cons**: ❌ Manual maintenance required for TOC updates

### Solution 2: Use `<!-- no toc -->` Comment

**Best for**: Specific sections you want to protect from auto-generation

```markdown
<!-- no toc -->
- [Spring Boot CRUD Application](#spring%20boot%20crud%20application)
  - [📋 Table of Contents](#%20table%20of%20contents)
  - [🚀 Features](#%20features)
```

**Steps**:
1. Add `<!-- no toc -->` above your manually created TOC
2. The extension will ignore this section
3. Manually maintain the TOC with `%20` formatting

**Pros**: ✅ Protects specific TOC from auto-generation  
**Cons**: ❌ Manual maintenance, no auto-updates

### Solution 3: Post-Processing with sed Command

**Best for**: Automated workflows or when you frequently need this conversion

```bash
# Replace all hyphens with %20 in TOC lines only
sed -i '/^-/ s/-/%20/g' /path/to/your-file.md

# More specific: only in links (between parentheses)
sed -i 's/](#[^)]*-[^)]*)$/&/g; s/-/%20/g' /path/to/your-file.md
```

**Workflow**:
1. Generate TOC normally with the extension
2. Run the sed command to post-process
3. Repeat as needed

**Pros**: ✅ Automated, can be scripted  
**Cons**: ❌ Extra step, may affect other parts of file

### Solution 4: Custom Python Script

**Best for**: Complex processing or integration into build pipelines

```python
import re

def convert_toc_to_percent_encoding(file_path):
    """Convert TOC links from hyphens to %20 encoding"""
    with open(file_path, 'r', encoding='utf-8') as file:
        content = file.read()
    
    # Pattern to match TOC lines with links
    toc_pattern = r'^(\s*- \[.*?\]\(#)(.*?)(\))$'
    
    def replace_hyphens(match):
        prefix = match.group(1)  # "- [Title](#"
        link = match.group(2)    # "spring-boot-crud"
        suffix = match.group(3)  # ")"
        
        # Replace hyphens with %20 in the link part
        converted_link = link.replace('-', '%20')
        return f"{prefix}{converted_link}{suffix}"
    
    # Apply replacement line by line
    lines = content.split('\n')
    processed_lines = []
    
    for line in lines:
        if re.match(r'^\s*- \[.*?\]\(#.*?\)$', line):
            line = re.sub(toc_pattern, replace_hyphens, line)
        processed_lines.append(line)
    
    # Write back to file
    with open(file_path, 'w', encoding='utf-8') as file:
        file.write('\n'.join(processed_lines))

# Usage
convert_toc_to_percent_encoding('/path/to/your-file.md')
```

**Pros**: ✅ Precise control, handles complex cases  
**Cons**: ❌ Requires Python, additional complexity

### Solution 5: VS Code Tasks for Automation

**Best for**: Frequent TOC updates with automated post-processing

Create a VS Code task to automate the TOC generation and conversion process:

**File**: `.vscode/tasks.json`
```json
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "Generate TOC with %20",
            "type": "shell",
            "command": "sed",
            "args": [
                "-i",
                "/^\\s*- \\[.*\\](#.*)/s/-/%20/g",
                "${file}"
            ],
            "group": "build",
            "detail": "Generate TOC and convert hyphens to %20"
        }
    ]
}
```

**Usage**:
1. Generate TOC with "Create Table of Contents" command
2. Run task with `Ctrl+Shift+P` → "Tasks: Run Task" → "Generate TOC with %20"

**Pros**: ✅ Integrated into VS Code workflow, one-click solution  
**Cons**: ❌ Requires task setup, may need adjustment for complex cases

### Solution 6: Find and Replace with Regex

**Best for**: Quick manual fixes without external tools

**Steps**:
1. Generate TOC normally
2. Open Find and Replace (`Ctrl+H`)
3. Enable Regex mode (`Alt+R`)
4. Find: `(- \[.*?\]\(#.*?)-`
5. Replace: `$1%20`
6. Replace All in Selection (select TOC first)

**Regex Explanation**:
- `(- \[.*?\]\(#.*?)` - Captures TOC line up to the first hyphen
- `-` - Matches the hyphen to replace
- `$1%20` - Replaces with captured group + %20

**Pros**: ✅ No external tools, built into VS Code  
**Cons**: ❌ Manual process, requires regex knowledge

### Solution 7: Keyboard Shortcut for Quick Conversion

**Best for**: Power users who frequently need this conversion

**File**: `keybindings.json`
```json
[
    {
        "key": "ctrl+alt+t",
        "command": "workbench.action.terminal.sendSequence",
        "args": {
            "text": "sed -i '/^\\s*- \\[.*\\](#.*)/s/-/%20/g' '${file}'\n"
        },
        "when": "editorLangId == markdown"
    }
]
```

**Usage**: Press `Ctrl+Alt+T` to instantly convert TOC in current file

**Pros**: ✅ Fastest method, customizable  
**Cons**: ❌ Requires terminal, setup needed

---

## 🔧 Alternative Extensions

### Markdown TOC Extension

**Extension ID**: `AlanWalk.markdown-toc`

**Features**:
- Different configuration options
- May have different slugification behavior
- Worth testing for `%20` support

**Installation**:
```bash
code --install-extension AlanWalk.markdown-toc
```

### Markdown Preview Enhanced

**Extension ID**: `shd101wyy.markdown-preview-enhanced`

**Features**:
- Advanced Markdown features
- Custom TOC generation options
- More configuration flexibility

**Installation**:
```bash
code --install-extension shd101wyy.markdown-preview-enhanced
```

---

## 📝 Settings Configuration

### VS Code settings.json Configuration

**Location**: `~/.config/Code/User/settings.json` (Linux)

**Complete configuration for TOC management**:
```json
{
  // Markdown All in One TOC Settings
  "markdown.extension.toc.updateOnSave": false,
  "markdown.extension.toc.levels": "2..6",
  "markdown.extension.toc.slugifyMode": "github",
  "markdown.extension.list.indentationSize": "adaptive",
  
  // Disable auto-update to prevent overwriting manual changes
  "markdown.extension.toc.omittedFromToc": {
    "README.md": [
      "# Introduction"
    ]
  },
  
  // Other useful Markdown settings
  "markdown.extension.completion.respectVscodeSearchExclude": true,
  "markdown.extension.italic.indicator": "*",
  "markdown.extension.bold.indicator": "**"
}
```

### Troubleshooting Settings

**If settings don't apply**:
1. Restart VS Code
2. Check for conflicting extensions
3. Verify settings.json syntax with JSON validator
4. Check workspace settings vs user settings

---

## 🎯 Best Practices

1. **Choose Your Approach Early**: Decide on TOC formatting strategy before creating extensive documentation

2. **Document Your Choice**: Add comments to explain why you're using specific formatting

3. **Automation**: If you frequently need `%20` formatting, create scripts or shortcuts

4. **Team Consistency**: Ensure team members use the same approach

5. **Version Control**: Consider adding pre-commit hooks to enforce TOC formatting

6. **Testing Links**: Always test that your TOC links work correctly in your target environment

---

## 🔮 Future Considerations

1. **Feature Requests**: Consider submitting feature requests to extension developers for native `%20` support

2. **Custom Extensions**: For organizations with specific needs, developing a custom TOC extension might be worthwhile

3. **Build Pipeline Integration**: Integrate TOC processing into CI/CD pipelines for consistent formatting

4. **Documentation Standards**: Establish organization-wide standards for Markdown TOC formatting

---

## 📖 References

- [Markdown All in One Documentation](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one)
- [VS Code Markdown Features](https://code.visualstudio.com/docs/languages/markdown)
- [Markdown TOC Extension](https://marketplace.visualstudio.com/items?itemName=AlanWalk.markdown-toc)
- [URL Encoding Standards (RFC 3986)](https://tools.ietf.org/html/rfc3986)
- [GitHub Flavored Markdown Specification](https://github.github.com/gfm/)

---

## 🚨 Common Pitfalls and Solutions

### Issue 1: Over-Encoding with Emojis

**Problem**: Emojis in headings create complex encoded strings
```markdown
# 📋 Table of Contents
# Generates: #%F0%9F%93%8B-table-of-contents
```

**Solution**: Remove emojis from headings or use alternative Unicode:
```markdown
# Table of Contents 📋
# Generates: #table%20of%20contents%20
```

### Issue 2: Special Characters Breaking Links

**Problem**: Characters like `&`, `@`, `#` in headings cause issues

**Solution**: Use the `<!-- omit from toc -->` comment for problematic headings:
```markdown
# API & Authentication Guide <!-- omit from toc -->
```

### Issue 3: Nested List Indentation

**Problem**: Multi-level TOC indentation gets corrupted during conversion

**Solution**: Use more specific regex that preserves indentation:
```bash
sed -i '/^\s*- \[.*\](#.*)/s/\(]\(#[^)]*\)-/\1%20/g' file.md
```

### Issue 4: Case Sensitivity Issues

**Problem**: TOC links don't match actual heading anchors due to case differences

**Solution**: Ensure headings follow consistent casing patterns or use case-insensitive matching

---

## 🔍 Testing and Validation

### Verify Links Work Correctly

After converting to `%20` format, test your links:

1. **Preview in VS Code**: Use `Ctrl+Shift+V` to preview
2. **Test in Browser**: Open the `.md` file in browser
3. **GitHub/GitLab**: Push to repository and test online
4. **Static Site Generators**: Test with your specific generator (Jekyll, Hugo, etc.)

### Validation Script

Create a simple validation script to check TOC links:

```bash
#!/bin/bash
# validate-toc.sh
echo "Validating TOC links in $1"
grep -n "](#.*%20" "$1" | while read line; do
    echo "Found %20 link: $line"
done
```

### Cross-Platform Compatibility

**Important Note**: `%20` encoding may behave differently across platforms:
- ✅ **Works well**: GitHub, GitLab, most static site generators
- ⚠️ **May have issues**: Some Wiki systems, older Markdown parsers
- ❌ **Avoid**: Internal VS Code navigation (use `-` for VS Code preview)

---

## 🛠 Advanced Configuration

### Workspace-Specific Settings

For project-specific TOC requirements, use workspace settings:

**File**: `.vscode/settings.json`
```json
{
    "markdown.extension.toc.updateOnSave": false,
    "markdown.extension.toc.slugifyMode": "github",
    "files.associations": {
        "*.md": "markdown"
    }
}
```

### Git Hooks for Consistency

Ensure team consistency with pre-commit hooks:

**File**: `.git/hooks/pre-commit`
```bash
#!/bin/sh
# Convert TOC hyphens to %20 before commit
find . -name "*.md" -exec sed -i '/^- \[.*\](#.*)/s/-/%20/g' {} \;
git add -A
```

### EditorConfig for Markdown

**File**: `.editorconfig`
```ini
[*.md]
indent_style = space
indent_size = 2
trim_trailing_whitespace = true
insert_final_newline = true
```

---

## 📊 Comparison Matrix

| Solution            | Speed | Automation | Accuracy | Setup Complexity | Best For           |
| ------------------- | ----- | ---------- | -------- | ---------------- | ------------------ |
| Disable Auto-Update | ⭐⭐    | ❌          | ⭐⭐⭐      | ⭐                | One-time docs      |
| `<!-- no toc -->`   | ⭐⭐    | ❌          | ⭐⭐⭐      | ⭐                | Specific sections  |
| sed Command         | ⭐⭐⭐   | ⭐⭐         | ⭐⭐       | ⭐⭐               | Regular use        |
| Python Script       | ⭐⭐    | ⭐⭐⭐        | ⭐⭐⭐      | ⭐⭐⭐              | Complex processing |
| VS Code Tasks       | ⭐⭐⭐   | ⭐⭐⭐        | ⭐⭐       | ⭐⭐               | VS Code workflow   |
| Find & Replace      | ⭐⭐⭐   | ❌          | ⭐⭐       | ⭐                | Quick fixes        |
| Keyboard Shortcut   | ⭐⭐⭐   | ⭐⭐         | ⭐⭐       | ⭐⭐               | Power users        |

**Legend**: ⭐ = Low, ⭐⭐ = Medium, ⭐⭐⭐ = High

---

## 🎯 Quick Reference Cheat Sheet

### Emergency Fix (2 minutes)
```bash
# Quick sed command for current file
sed -i '/^- \[.*\](#.*)/s/-/%20/g' filename.md
```

### VS Code Commands
- **Generate TOC**: `Ctrl+Shift+P` → "Create Table of Contents"
- **Find & Replace**: `Ctrl+H` → Enable Regex → Find: `(- \[.*?\]\(#.*?)-` Replace: `$1%20`
- **Preview**: `Ctrl+Shift+V`

### Settings to Remember
```json
{
  "markdown.extension.toc.updateOnSave": false,
  "markdown.extension.toc.slugifyMode": "github"
}
```

### Test Your Links
1. Preview in VS Code (`Ctrl+Shift+V`)
2. Check in target platform (GitHub, GitLab, etc.)
3. Validate with browser if deploying to web

---

## 🤔 Decision Tree: Which Solution to Choose?

```
Do you need %20 formatting frequently?
├─ YES → Use VS Code Tasks or Keyboard Shortcuts
└─ NO → Do you need it for one file?
   ├─ YES → Use Find & Replace or sed command
   └─ NO → Is this for a team project?
      ├─ YES → Set up Git hooks + Documentation
      └─ NO → Use <!-- no toc --> + manual editing
```

---
