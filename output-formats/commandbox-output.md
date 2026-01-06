---
description: Generate CommandBox CLI command documentation with namespace organization
icon: terminal
---

# CommandBox Output

🎯 The CommandBox Strategy is a specialized output format designed specifically for documenting CommandBox CLI commands and namespaces. It extends the HTML API Strategy with CLI-focused terminology and navigation.

## 🚀 Overview

The CommandBox Strategy transforms CommandBox command components into searchable, navigable HTML documentation with command-specific features:

* **Command-Centric Navigation** - Organizes by command namespaces (not packages)
* **CLI Terminology** - Uses "commands" and "namespaces" instead of "classes" and "packages"
* **Qualified Names** - Displays full command paths (e.g., `server start`, `package show`)
* **Namespace Hierarchy** - Visualizes command organization and nesting
* **Frames Theme** - Uses traditional frameset layout for CLI documentation

## 📦 Properties

The CommandBox Strategy accepts the following configuration properties:

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `outputDir` | string | Yes | Output directory absolute path |
| `projectTitle` | string | No | HTML title for documentation (default: "Untitled") |

## 🎯 Basic Usage

### Using Strategy Alias

```javascript
new docbox.DocBox()
    .addStrategy( "CommandBox", {
        projectTitle : "My CommandBox Commands",
        outputDir    : expandPath( "/docs/commands" )
    } )
    .generate(
        source  = expandPath( "/modules/my-commands/commands/" ),
        mapping = "my-commands"
    );
```

### Using Full Class Path

```javascript
new docbox.DocBox()
    .addStrategy(
        new docbox.strategy.CommandBox.CommandBoxStrategy(
            outputDir    = expandPath( "/docs/commandbox" ),
            projectTitle = "CommandBox CLI Reference"
        )
    )
    .generate(
        source  = "/commandbox/cfml/system/modules_app/",
        mapping = "commandbox.commands"
    );
```

## 📂 Generated Structure

The CommandBox Strategy generates the following file structure:

```
outputDir/
├── index.html                  - Main entry point (frameset)
├── overview-summary.html       - Namespace overview
├── overview-frame.html         - Navigation sidebar
├── css/                        - CSS stylesheets
├── js/                         - JavaScript files
├── bootstrap/                  - Bootstrap assets
└── {namespace}/
    ├── package-summary.html    - Namespace detail page
    └── {command}.html          - Individual command documentation
```

## 🎨 Features

### Command Path Display

Unlike standard class documentation, CommandBox Strategy shows the full command path:

```
server start
server stop
package show
package set
```

### Namespace Organization

Commands are grouped by their namespace hierarchy:

* `server` namespace
  * `start` command
  * `stop` command
  * `restart` command
* `package` namespace
  * `show` command
  * `set` command
  * `install` command

### CLI-Focused Templates

The strategy uses specialized templates that:

* Display command syntax and usage
* Show command examples in CLI format
* Highlight command parameters and flags
* Use CLI-appropriate terminology

## 📋 Real-World Examples

### Documenting CommandBox Core

Generate documentation for CommandBox's built-in commands:

```javascript
new docbox.DocBox()
    .addStrategy( "CommandBox", {
        projectTitle : "CommandBox CLI Reference",
        outputDir    : expandPath( "/docs/commandbox-core" )
    } )
    .generate(
        source  = "/commandbox/cfml/system/modules_app/",
        mapping = "commandbox.commands",
        excludes = "(tests|build)"
    );
```

### Custom CommandBox Module

Document your own CommandBox module commands:

```javascript
new docbox.DocBox()
    .addStrategy( "CommandBox", {
        projectTitle : "My CLI Module",
        outputDir    : expandPath( "/docs/my-module" )
    } )
    .generate(
        source  = expandPath( "/modules/my-module/commands/" ),
        mapping = "my-module.commands"
    );
```

### Multiple Command Modules

Document multiple CommandBox modules together:

```javascript
var docbox = new docbox.DocBox()
    .addStrategy( "CommandBox", {
        projectTitle : "All Command Modules",
        outputDir    : expandPath( "/docs/all-commands" )
    } );

docbox.generate(
    source = [
        { dir: expandPath( "/modules/module1/commands/" ), mapping: "module1" },
        { dir: expandPath( "/modules/module2/commands/" ), mapping: "module2" }
    ]
);
```

## 🔧 Technical Details

### Strategy Implementation

The CommandBox Strategy:

* **Extends**: `docbox.strategy.api.HTMLAPIStrategy`
* **Template Path**: `/docbox/strategy/CommandBox/resources/templates`
* **Assets Path**: `/docbox/strategy/api/themes/frames/resources/static`

### Metadata Augmentation

The strategy augments the standard metadata query with additional columns:

* `command` - The command name extracted from the component
* `namespace` - The namespace path for the command

### Template Overrides

CommandBox Strategy overrides specific templates:

* `class.cfm` - Modified to show command syntax
* `package-summary.cfm` - Shows namespace commands
* `overview-summary.cfm` - Lists all namespaces

## ⚠️ Important Notes

1. **Theme Locked**: CommandBox Strategy always uses the frames theme for consistency
2. **Command Components**: Expects CommandBox command component structure
3. **Namespace Detection**: Automatically extracts namespace from component metadata
4. **Asset Sharing**: Reuses frames theme assets for stability

## 🔗 Related Documentation

* [HTML Output](html-output.md) - Parent strategy documentation
* [Custom Output Strategy](custom-output-strategy.md) - Creating your own strategies
* [Configuration](../getting-started/configuration.md) - Strategy configuration options

## 💡 Tips

* Use consistent naming conventions for command components
* Add comprehensive JavaDoc comments to commands
* Document command parameters with `@hint` attributes
* Include usage examples in command descriptions
* Group related commands under the same namespace
