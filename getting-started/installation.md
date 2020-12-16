# Installation

There are two main flavors of DocBox: Standalone and CLI.

## Standalone

To generate documentation from your CFML application:

1. Run `box install docbox --saveDev` to install docbox to your application
2. Create a `docbox` mapping that points to the DocBox source code location

You will need to create a CFML script which runs DocBox against your source code. See [Getting Started](README.md) for more details.

## CLI

We also have a [CommandBox module](https://forgebox.io/view/commandbox-docbox) to enable generating documentation from the CLI.

1. Run `box install commandbox-docbox` to install the `docbox` command namespace
2. Run `docbox help` to get a list of commands
3. Run `docbox generate help` to show help for the `docbox generate` command

