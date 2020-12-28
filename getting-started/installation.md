---
description: 'Just use CommandBox! No, really.'
---

# Installation

## Using DocBox in a Standalone Application

Installing and using DocBox consists of three main steps:

### Download

For best results, use [CommandBox](https://commandbox.ortusbooks.com/) to run `box install docbox --saveDev` in your app root.

Alternatively, you can download the docbox source code and drop it into a `docbox` folder in your application.

### Mapping

DocBox requires its components to be accessible from the `docbox` location in the application root. If this

1. Create a `docbox` mapping that points to the DocBox source code location
2. Write a CFML script which runs DocBox against your source code.

See [Configuration](configuration.md) for more details.

## Using DocBox from the Command Line

We also have a CommandBox module called [DocBox Commands ](https://forgebox.io/view/commandbox-docbox)which enables generating documentation from the CLI.

1. Run `box install commandbox-docbox` to install the `docbox` command namespace
2. Run `docbox help` to get a list of commands
3. Run `docbox generate help` to show help for the `docbox generate` command

Please see the [DocBox Commands README](https://github.com/Ortus-Solutions/commandbox-docbox/blob/development/README.md) for more info.

