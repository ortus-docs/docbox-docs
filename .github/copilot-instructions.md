# DocBox Documentation - AI Coding Instructions

This is the GitBook documentation repository for DocBox, a JavaDoc-style API documentation generator for CFML/BoxLang. The docs are structured as Markdown files and published via GitBook.

## Repository Structure & Architecture

**GitBook Integration**: This repository uses GitBook for documentation hosting:
- `SUMMARY.md` - Table of contents defining navigation structure (required by GitBook)
- `README.md` - Landing page/introduction
- Front matter headers - YAML metadata (description, icon) used by GitBook for page configuration
- Organized in logical sections: `getting-started/`, `output-formats/`, `advanced/`, `readme/`

**Documentation Organization**:
- `getting-started/` - Installation, configuration, CLI tools, annotations, troubleshooting
- `output-formats/` - HTML, JSON, UML, CommandBox output strategy docs
- `advanced/` - API reference for DocBox classes and methods
- `readme/` - Release history, contributing guidelines

**Content References**: Documentation references the main DocBox project at `/Users/lmajano/Sites/projects/DocBox` for code examples and implementation details.

## Critical Documentation Patterns

**Front Matter**: Every markdown file requires GitBook front matter:
```markdown
---
description: Brief summary for SEO and page previews
icon: house  # Optional FontAwesome icon (e.g., house, wrench, code, book, rocket)
---
# Page Title
```

**FontAwesome Icons**: GitBook supports FontAwesome icons in front matter. Common icons used in this project:
- `house` - Home/introduction pages
- `download` - Installation pages
- `wrench` - Configuration/troubleshooting
- `code` - API reference/technical docs
- `book` - Guides and tutorials
- `rocket` - Getting started/quick start
- `handshake` - Contributing

**SUMMARY.md Structure**: Controls sidebar navigation - must be updated when adding/removing pages:
```markdown
* [Page Title](path/to/file.md)
  * [Nested Page](path/to/nested.md)

## Section Header

* [Another Page](another/page.md)
```

**Cross-References**: Link to other docs pages using relative paths:
- Same directory: `[text](file.md)`
- Parent directory: `[text](../file.md)`
- Specific section: `[text](file.md#section-anchor)`

**Code Examples**: Use fenced code blocks with language identifiers:
```javascript
// CFML/JavaScript examples
```
```bash
# Shell commands
```

## Documentation Writing Guidelines

**Emoji Usage**: Docs heavily use emojis for visual hierarchy and scanability:
- Section headers: 📚 🎨 🚀 🔧 💡 ⚠️ 📊 🎯
- Feature lists: ✨ 🌓 🔍 📱 💜
- Status indicators: ✅ ❌ ⚠️

**Examples Format**: Always provide complete, runnable examples:
```javascript
// Good - full context
new docbox.DocBox()
    .addStrategy( "HTML", {
        outputDir: expandPath( "/docs" ),
        projectTitle: "My API"
    })
    .generate(
        source: "/src",
        mapping: "app"
    );

// Bad - incomplete fragment
.addStrategy( "HTML", { ... })
```

**Strategy Documentation**: When documenting strategies, include:
1. Overview with key features (bullet list)
2. Properties table (name, type, required, description)
3. Basic usage example
4. Real-world examples (multiple scenarios)
5. Generated structure (file tree)
6. Technical details (class paths, template locations)

**CLI Commands**: Format with proper syntax highlighting and examples:
```bash
# With explanation
boxlang module:docbox --source=/src --mapping=app --output-dir=/docs

# Multiple examples showing different use cases
```

## Content Synchronization

**Source of Truth**: The main DocBox project (`/Users/lmajano/Sites/projects/DocBox`) is the source of truth for:
- Code examples and API signatures
- Strategy implementations and features
- Build processes and workflows
- Version numbers and release information

**Documentation Updates**: When DocBox code changes:
1. Update API reference (`advanced/api-reference.md`) with new methods/properties
2. Update configuration docs (`getting-started/configuration.md`) with new options
3. Update release history (`readme/release-history/whats-new-with-X.X.X.md`)
4. Update troubleshooting (`getting-started/troubleshooting.md`) with new issues/solutions

**Version References**: Keep version numbers consistent:
- System requirements in `README.md`
- Release history in `readme/release-history/`
- Installation commands showing latest stable version

## Key Documentation Files

**Core Guides**:
- `getting-started/installation.md` - Installation methods (BoxLang module, CFML library, CommandBox)
- `getting-started/configuration.md` - Strategy configuration and multi-strategy examples
- `getting-started/annotating-your-code.md` - JavaDoc tags and `@doc_generic` annotation
- `getting-started/troubleshooting.md` - Common errors and debug tips

**Output Format Docs**:
- `output-formats/html-output.md` - HTML themes (default SPA, frames layout)
- `output-formats/json-output/` - JSON schema and structure
- `output-formats/commandbox-output.md` - CommandBox CLI documentation strategy
- `output-formats/custom-output-strategy.md` - Creating custom strategies

**Reference**:
- `advanced/api-reference.md` - Complete API for DocBox.cfc, strategies, and interfaces

## Common Documentation Tasks

**Adding New Feature Documentation**:
1. Create/update relevant section file (e.g., `getting-started/new-feature.md`)
2. Add front matter with description and icon
3. Update `SUMMARY.md` to include new page in navigation
4. Add examples showing the feature in action
5. Update API reference if adding new methods/properties
6. Consider troubleshooting section for common issues

**Updating for New DocBox Release**:
1. Create new release notes in `readme/release-history/whats-new-with-X.X.X.md`
2. Update `SUMMARY.md` to link new release notes
3. Update system requirements in `README.md` if needed
4. Review and update all affected docs (features, config, API)
5. Add troubleshooting entries for breaking changes

**Code Example Standards**:
- Use `expandPath()` for file paths in CFML examples
- Show both shorthand and verbose syntax where applicable
- Include comments explaining non-obvious parameters
- Provide both basic and advanced examples for complex features
- Use realistic variable/path names (not `foo`, `/path/to/thing`)

## GitBook-Specific Conventions

**Anchors**: GitBook auto-generates anchors from headers:
- `# My Section` becomes `#my-section`
- Reference: `[link text](#my-section)`
- Cross-page: `[link](file.md#anchor)`

**Callouts**: Use blockquotes for notes, tips, warnings (styled by GitBook):
```markdown
> **Note:** Important information
> **Warning:** Critical caution
> **Tip:** Helpful suggestion
```

**Tables**: Use standard markdown tables with proper alignment:
```markdown
| Column 1 | Column 2 | Column 3 |
|----------|----------|----------|
| Value    | Value    | Value    |
```

**Assets**: Reference images/assets from `.gitbook/assets/` if needed:
```markdown
![Alt text](.gitbook/assets/image.png)
```

## Documentation Quality Standards

**Completeness**: Every feature should have:
- Clear explanation of what it does and why to use it
- At least one basic example
- At least one real-world example
- Parameter/option documentation
- Links to related documentation

**Accuracy**: Verify examples against actual DocBox implementation:
- Test code examples in a real DocBox environment
- Verify file paths and directory structures
- Confirm API signatures match current version
- Check output format examples against generated files

**Consistency**: Maintain uniform style:
- Emoji usage patterns
- Code block formatting
- Section header hierarchy (h2 for major sections, h3 for subsections)
- Link formatting (relative paths, proper anchors)
- Example structure (comments, variable names, paths)
