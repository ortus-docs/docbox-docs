# Configuration

## Supported Output Formats

DocBox offers several built-in output formats as well as enabling you to [create your own](../output-formats/custom-output-strategy.md):

* [HTML](../output-formats/html-output.md) - Modern HTML documentation with two theme options
* [JSON](../output-formats/json-output/README.md) - Machine-readable JSON format
* [UML](../output-formats/uml-output.md) - XMI/UML diagram generation

Each format is configured by its alias name, such as `"JSON"`, `"HTML"`, or `"XMI"`.

```javascript
var docbox = new docbox.DocBox();
docbox.addStrategy( "UML", { outputFile : "./tmp/docs/app-diagram.uml" })
```

## Basic Configuration

### Single Strategy

```javascript
new docbox.DocBox()
    .addStrategy( "HTML", {
        projectTitle : "My API Documentation",
        outputDir    : expandPath( './docs' ),
        theme        : "default"  // or "frames"
    } )
    .generate(
        source   = expandPath( "/app" ),
        mapping  = "app",
        excludes = "(tests|build)"
    );
```

### Multiple Strategies

You can call the `.addStrategy()` method multiple times to generate multiple output formats:

```javascript
new docbox.DocBox()
    .addStrategy( "HTML", {
        projectTitle : "My Docs",
        outputDir    : expandPath( '/docs/html' ),
        theme        : "default"
    } )
    .addStrategy( "JSON", {
        projectTitle : "My Docs",
        outputDir    : expandPath( '/docs/json' )
    } )
    .addStrategy( "XMI", {
        outputFile : expandPath( '/docs/diagram.uml' )
    } )
    .generate(
        source   = expandPath( "/app" ),
        mapping  = "app",
        excludes = "(tests|build)"
    );
```

## HTML Strategy Options (New in 5.0)

The HTML strategy now supports theme selection:

```javascript
// Use the modern SPA theme (default)
docbox.addStrategy( "HTML", {
    projectTitle : "My API",
    outputDir    : expandPath( './docs' ),
    theme        : "default"
} );

// Use the traditional frames theme
docbox.addStrategy( "HTML", {
    projectTitle : "My API",
    outputDir    : expandPath( './docs' ),
    theme        : "frames"
} );
```

### Theme Features

**Default Theme:**
* Alpine.js SPA architecture
* Dark mode toggle with persistence
* Real-time method search
* Tabbed method summaries
* Modern purple gradient design
* Bootstrap 5 components

**Frames Theme:**
* Traditional three-panel frameset
* Left sidebar navigation
* Bootstrap 5 styling
* Dark mode support
* Classic documentation UX

## Generate Method Parameters

The `generate()` method accepts the following parameters:

* `source` : A path to the source location or an array of structs of locations that must have a `dir` and `mapping` key
* `mapping` : The base mapping for the folder source (used only if `source` is a path)
* `excludes` : A regular expression that will be evaluated against all CFCs. If the regex matches the CFC name and path, the CFC will be excluded

### Single Source

```javascript
docbox.generate(
    source   = expandPath( '/myapp' ),
    mapping  = 'myapp',
    excludes = '(tests|build)'
);
```

### Multiple Sources

```javascript
docbox.generate(
    source = [
        { dir: expandPath( '/app/models' ), mapping: 'app.models' },
        { dir: expandPath( '/app/handlers' ), mapping: 'app.handlers' },
        { dir: expandPath( '/plugins' ), mapping: 'plugins' }
    ],
    excludes = '(tests|specs)'
);
```

## BoxLang CLI Usage (New in 5.0)

DocBox 5.0 includes a native BoxLang CLI module:

```bash
# Basic usage
boxlang module:docbox --source=/path/to/code \
                       --mapping=myapp \
                       --output-dir=/docs

# With options
boxlang module:docbox --source=/app \
                       --mapping=myapp \
                       --output-dir=/docs \
                       --project-title="My API" \
                       --theme=frames \
                       --excludes="(tests|build)"

# Multiple sources
boxlang module:docbox --mappings:models=/app/models \
                       --mappings:handlers=/app/handlers \
                       --output-dir=/docs
```

See `boxlang module:docbox --help` for complete CLI documentation.

## Backwards Compatibility

For backwards compatibility, specifying the full class path is still supported, as is specifying a single strategy when initializing DocBox:

```javascript
variables.docbox = new docbox.DocBox(
    strategy   = "docbox.strategy.uml2tools.XMIStrategy",
    properties = {
        projectTitle : "DocBox Tests",
        outputFile   : variables.testOutputFile
    }
);
```
