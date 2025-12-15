---
description: Just use CommandBox! No, really.
---

# Installation

## 🦤 BoxLang Module Installation (Recommended for CLI)

DocBox 5.0+ can be installed as a native BoxLang core module, providing access to the powerful CLI tool.

### CommandBox Web Runtimes

```bash
box install bx-docbox
```

### BoxLang OS Runtime

```bash
install-bx-module bx-docbox
```

Once installed, you can use the `boxlang module:docbox` CLI command to generate documentation. See the [BoxLang CLI Tool](boxlang-cli.md) page for complete usage details and examples.

## Using DocBox in a Standalone Application

Installing and using DocBox consists of three main steps:

### Download

For best results, use [CommandBox](https://commandbox.ortusbooks.com/) to run `box install docbox --saveDev` in your app root.

Alternatively, you can download the DocBox source code and drop it into a `docbox` folder in your application.

### Mapping

If DocBox is not installed in the root of your application, you will need to create a `docbox` mapping that points to the DocBox source code location:

```javascript
this.mappings[ "docbox" ] = expandPath( "./libraries/doctorBox" );
```

In addition to the Docbox mapping, **you will need a Coldfusion server mapping for each source code location**. For example, documenting a component with `implements="cbsecurity.interfaces.IAuthService"` will require a mapping of `cbsecurity` to the installed`cbsecurity` source code so DocBox can find the referenced interface.

### Using DocBox

The final step to get DocBox running is to write a CFML script that initializes, configures, and runs DocBox against your application code.

See [Configuration](configuration.md) for more details.

## Using DocBox from the Command Line

We offer multiple ways to use DocBox from the command line:

### BoxLang CLI Module (New in 5.0)

DocBox now includes a native BoxLang CLI module for generating documentation:

```bash
# Basic usage
boxlang module:docbox --source=/path/to/code --mapping=myapp --output-dir=/docs

# With project title and excludes
boxlang module:docbox --source=/src --mapping=myapp \
                       --excludes="(tests|build)" \
                       --output-dir=/docs \
                       --project-title="My API"

# Multiple source mappings
boxlang module:docbox --mappings:v1=/src/v1/models \
                       --mappings:v2=/src/v2/models \
                       --output-dir=/docs

# Using frames theme
boxlang module:docbox --source=/src --mapping=app \
                       --output-dir=/docs \
                       --theme=frames

# Show help
boxlang module:docbox --help

# Show version
boxlang module:docbox --version
```

### CommandBox Module

We also have a CommandBox module called [DocBox Commands](https://forgebox.io/view/commandbox-docbox), which enables generating documentation from the CLI.

1. Run `box install commandbox-docbox` to install the `docbox` command namespace
2. Run `docbox help` to get a list of commands
3. Run `docbox generate help` to show help for the `docbox generate` command

Please see the [DocBox Commands README](https://github.com/Ortus-Solutions/commandbox-docbox/blob/development/README.md) for more info.
