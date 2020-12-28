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

If DocBox is not installed in the root of your application, you will need to create a `docbox` mapping that points to the DocBox source code location:

```javascript
this.mappings["docbox"] = expandPath( "./libraries/doctorBox" );
```

In addition to the Docbox mapping, **you will need a Coldfusion server mapping for each source code location**. For example, documenting a component with `implements="cbsecurity.interfaces.IAuthService"` will require a mapping of `cbsecurity` to the installed`cbsecurity` source code so DocBox can find the referenced interface.

### Using DocBox

The final step to get DocBox running  is to write a CFML script which initializes, configures, and runs DocBox against your application code.

See [Configuration](configuration.md) for more details.

## Using DocBox from the Command Line

We also have a CommandBox module called [DocBox Commands ](https://forgebox.io/view/commandbox-docbox)which enables generating documentation from the CLI.

1. Run `box install commandbox-docbox` to install the `docbox` command namespace
2. Run `docbox help` to get a list of commands
3. Run `docbox generate help` to show help for the `docbox generate` command

Please see the [DocBox Commands README](https://github.com/Ortus-Solutions/commandbox-docbox/blob/development/README.md) for more info.

