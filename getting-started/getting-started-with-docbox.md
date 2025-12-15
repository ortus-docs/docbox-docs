# Getting Started with DocBox

## 🚀 Quick Start Guide

1. 📦 [Installation](installation.md) - Install via CommandBox or BoxLang
2. ⚙️ [Configuration](configuration.md) - Set up output strategies and options
3. 📝 [Annotating Your Code](annotating-your-code.md) - Add JavaDoc-style comments

## ✨ What's New in 5.0

DocBox 5.0 is a major release with significant improvements:

* **Full BoxLang Support** - Native BoxLang runtime and CLI integration
* **Modern HTML Themes** - Two professional themes with dark mode
* **Enhanced UI/UX** - Real-time search, method tabs, smooth scrolling
* **Complete Documentation** - All relationships (implements, extends, subclasses)
* **CLI Module** - New `boxlang module:docbox` command

See [What's New With 5.0.0](../readme/release-history/whats-new-with-5.0.0.md) for complete details.

## 📊 Supported Output Formats

DocBox supports several output formats:

* 🌐 [HTML Output](../output-formats/html-output.md) - Modern browsable documentation with two themes
* 📋 [JSON Output](../output-formats/json-output/README.md) - Machine-readable JSON format
* 📐 [UML Output](../output-formats/uml-output.md) - XMI/UML diagram generation

Each format is configured by its alias name, such as `"JSON"` or `"HTML"`.

```javascript
var docbox = new docbox.DocBox();
docbox.addStrategy( "HTML", {
    projectTitle : "My API",
    outputDir    : "./docs",
    theme        : "default"  // or "frames"
})
```

## 💡 Quick Examples

### 🥊 Using BoxLang CLI (New in 5.0)

```bash
boxlang module:docbox --source=/path/to/code \
                       --mapping=myapp \
                       --output-dir=/docs \
                       --project-title="My API"
```

### 💎 Using CFML

```javascript
new docbox.DocBox()
    .addStrategy( "HTML", {
        projectTitle : "My API Documentation",
        outputDir    : expandPath( './docs' ),
        theme        : "default"
    } )
    .generate(
        source   = expandPath( '/myapp' ),
        mapping  = 'myapp',
        excludes = '(tests|build)'
    );
```

### Multiple Output Formats

```javascript
new docbox.DocBox()
    .addStrategy( "HTML", {
        projectTitle : "My API",
        outputDir    : expandPath( './docs/html' )
    } )
    .addStrategy( "JSON", {
        projectTitle : "My API",
        outputDir    : expandPath( './docs/json' )
    } )
    .generate(
        source   = expandPath( '/myapp' ),
        mapping  = 'myapp'
    );
```

For backwards compatibility, specifying the full class path is still supported, as is specifying a single strategy when initializing DocBox:

```javascript
variables.docbox = new docbox.DocBox(
  strategy = "docbox.strategy.uml2tools.XMIStrategy",
  properties={
    projectTitle = "DocBox Tests",
    outputFile   = variables.testOutputFile
  }
);
```

### Custom Output Strategy

In addition to the mainstream output formats, you can extend DocBox's `AbstractTemplateStrategy` component to generate your own custom-formatted documentation. See [Custom Output Strategy](../output-formats/custom-output-strategy.md) for details.

```javascript
component extends="docbox.strategy.AbstractTemplateStrategy" accessors="true"{
    /**
     * Generate custom documentation
     *
     * @metadata All component metadata, sourced from DocBox.
     */
    component function run( required query metadata ){
        // generate custom documentation format from arguments.metadata
    }
}
```
