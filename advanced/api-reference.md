---
description: Complete API reference for DocBox classes and methods
icon: code
---

# API Reference

This page provides detailed API documentation for DocBox's core classes and methods.

## 📚 DocBox.cfc

The main entry point for DocBox documentation generation.

### Constructor

```javascript
DocBox function init(
    any strategy,
    struct properties = {}
)
```

Creates a new DocBox instance with optional initial strategy.

**Parameters:**
* `strategy` - (Optional) Strategy name ("HTML", "JSON", "XMI", "CommandBox") or instance
* `properties` - (Optional) Strategy configuration properties

**Returns:** DocBox instance

**Examples:**

```javascript
// No initial strategy
docbox = new docbox.DocBox();

// With strategy alias
docbox = new docbox.DocBox( strategy: "HTML", properties: {
    outputDir: "/docs",
    projectTitle: "My API"
} );

// With strategy instance
docbox = new docbox.DocBox(
    strategy: new docbox.strategy.api.HTMLAPIStrategy(
        outputDir: "/docs",
        projectTitle: "My API"
    )
);
```

### addStrategy()

```javascript
DocBox function addStrategy(
    required any strategy,
    struct properties = {}
)
```

Adds a documentation generation strategy to the collection.

**Parameters:**
* `strategy` - Strategy alias ("HTML", "JSON", "XMI", "CommandBox") or instance
* `properties` - Strategy configuration properties (if using alias)

**Returns:** DocBox instance (for chaining)

**Examples:**

```javascript
// Single strategy
docbox.addStrategy( "HTML", {
    outputDir: "/docs",
    projectTitle: "My Docs"
} );

// Multiple strategies
docbox
    .addStrategy( "HTML", { outputDir: "/docs/html" } )
    .addStrategy( "JSON", { outputDir: "/docs/json" } );

// Strategy instance
docbox.addStrategy(
    new docbox.strategy.api.HTMLAPIStrategy(
        outputDir: "/docs"
    )
);
```

### setStrategy()

```javascript
DocBox function setStrategy(
    required any strategy,
    struct properties = {}
)
```

**Deprecated:** Use `addStrategy()` instead. Kept for backward compatibility.

### generate()

```javascript
DocBox function generate(
    required any source,
    required string mapping,
    string excludes = "",
    boolean throwOnError = false
)
```

Generates documentation for the specified source code.

**Parameters:**
* `source` - Source directory path(s). Can be:
  * String: Single directory path
  * Array: Multiple source definitions
* `mapping` - Base mapping for the source code
* `excludes` - Regex pattern to exclude files/folders (applied to relative paths)
* `throwOnError` - Whether to throw exceptions for invalid components

**Returns:** DocBox instance

**Examples:**

```javascript
// Basic usage
docbox.generate(
    source: expandPath( "/src" ),
    mapping: "myapp"
);

// With exclusions
docbox.generate(
    source: expandPath( "/src" ),
    mapping: "myapp",
    excludes: "(tests|build|\.git)"
);

// Multiple sources
docbox.generate(
    source: [
        { dir: expandPath( "/src/models" ), mapping: "models" },
        { dir: expandPath( "/src/services" ), mapping: "services" }
    ]
);
```

### getStrategies()

```javascript
array function getStrategies()
```

Returns the array of registered strategies.

**Returns:** Array<AbstractTemplateStrategy>

---

## 🎨 AbstractTemplateStrategy.cfc

Base class for all documentation strategies. Provides common functionality for HTML, JSON, XMI, and custom strategies.

### Properties

```javascript
property name="outputDir" type="string";
property name="projectTitle" type="string" default="Untitled";
```

### run()

```javascript
IStrategy function run( required query qMetaData )
```

Executes the documentation generation strategy. Must be implemented by child classes.

**Parameters:**
* `qMetaData` - Query object containing component metadata

**Returns:** Strategy instance

### Helper Methods

#### getPackageQuery()

```javascript
query function getPackageQuery( required query qMetaData, required string package )
```

Returns components for a specific package.

**Parameters:**
* `qMetaData` - Full metadata query
* `package` - Package name

**Returns:** Filtered query

#### getFunctionQuery()

```javascript
query function getFunctionQuery(
    required struct metadata,
    string access = ""
)
```

Returns methods from component metadata.

**Parameters:**
* `metadata` - Component metadata structure
* `access` - Filter by access level ("public", "private", "remote", "package")

**Returns:** Query of methods

#### getPropertyQuery()

```javascript
query function getPropertyQuery( required struct metadata )
```

Returns properties from component metadata.

**Parameters:**
* `metadata` - Component metadata structure

**Returns:** Query of properties

#### buildPackageTree()

```javascript
struct function buildPackageTree( required array packageNames )
```

Converts flat package list into hierarchical tree structure.

**Parameters:**
* `packageNames` - Array of package names

**Returns:** Nested struct representing package hierarchy

**Example:**
```javascript
// Input: [ "coldbox.system.web", "coldbox.system.cache" ]
// Output: { coldbox: { system: { web: {}, cache: {} } } }
```

#### visitPackageTree()

```javascript
void function visitPackageTree(
    required struct tree,
    required any visitor,
    string prefix = ""
)
```

Traverses package tree and calls visitor function for each node.

**Parameters:**
* `tree` - Package tree structure
* `visitor` - Function to call for each package
* `prefix` - Current package prefix (used in recursion)

---

## 🌐 HTMLAPIStrategy.cfc

Generates HTML documentation with modern themes.

### Constructor

```javascript
HTMLAPIStrategy function init(
    required string outputDir,
    string projectTitle = "Untitled",
    string theme = "default"
)
```

**Parameters:**
* `outputDir` - Output directory for HTML files
* `projectTitle` - Title for documentation
* `theme` - Theme name ("default" or "frames")

**Example:**

```javascript
strategy = new docbox.strategy.api.HTMLAPIStrategy(
    outputDir: expandPath( "/docs" ),
    projectTitle: "My API",
    theme: "default"
);
```

### Properties

```javascript
property name="outputDir" type="string";
property name="projectTitle" type="string" default="Untitled";
property name="theme" type="string" default="default";
```

### Methods

#### run()

```javascript
IStrategy function run( required query qMetaData )
```

Generates HTML documentation using the selected theme.

---

## 📋 JSONAPIStrategy.cfc

Generates machine-readable JSON documentation.

### Constructor

```javascript
JSONAPIStrategy function init(
    required string outputDir,
    string projectTitle = "Untitled"
)
```

**Parameters:**
* `outputDir` - Output directory for JSON files
* `projectTitle` - Project title

### Properties

```javascript
property name="outputDir" type="string";
property name="projectTitle" type="string" default="Untitled";
```

---

## 📐 XMIStrategy.cfc

Generates UML/XMI diagrams.

### Constructor

```javascript
XMIStrategy function init( required string outputFile )
```

**Parameters:**
* `outputFile` - Output file path for XMI file (not a directory!)

**Example:**

```javascript
strategy = new docbox.strategy.uml2tools.XMIStrategy(
    outputFile: expandPath( "/docs/diagram.uml" )
);
```

### Properties

```javascript
property name="outputFile" type="string";
```

---

## 🎯 CommandBoxStrategy.cfc

Specialized strategy for CommandBox CLI commands.

### Constructor

```javascript
CommandBoxStrategy function init(
    required string outputDir,
    string projectTitle = "Untitled"
)
```

**Parameters:**
* `outputDir` - Output directory for HTML files
* `projectTitle` - Title for documentation

**Example:**

```javascript
strategy = new docbox.strategy.CommandBox.CommandBoxStrategy(
    outputDir: expandPath( "/docs/commands" ),
    projectTitle: "My CLI Commands"
);
```

---

## 🔌 IStrategy.cfc

Interface that all strategies must implement.

### run()

```javascript
IStrategy function run( required query metadata )
```

Executes the documentation generation strategy.

**Parameters:**
* `metadata` - Query object containing component metadata with columns:
  * `package` - Package name
  * `name` - Component name
  * `metadata` - Complete component metadata structure
  * `type` - Component type (component, interface, etc.)
  * `extends` - Extended component name
  * `implements` - Implemented interfaces
  * `fullextends` - Full inheritance chain
  * `currentMapping` - Base mapping

**Returns:** Strategy instance

---

## 📊 Common Metadata Query Structure

All strategies receive a query object with the following columns:

```javascript
qMetaData = queryNew(
    "package,name,extends,metadata,type,implements,fullextends,currentMapping",
    "varchar,varchar,varchar,any,varchar,varchar,varchar,varchar"
);
```

**Column Descriptions:**

* `package` - Package name (e.g., "coldbox.system.web")
* `name` - Component name (e.g., "Controller")
* `extends` - Direct parent component
* `metadata` - Full component metadata structure
* `type` - Component type ("component" or "interface")
* `implements` - Comma-separated list of interfaces
* `fullextends` - Full inheritance chain
* `currentMapping` - Base mapping used for generation

---

## 🛠️ Creating Custom Strategies

To create a custom strategy:

1. **Extend AbstractTemplateStrategy**

```javascript
component extends="docbox.strategy.AbstractTemplateStrategy" {

    property name="outputDir" type="string";

    function init( required string outputDir ) {
        variables.outputDir = arguments.outputDir;
        return this;
    }

    function run( required query qMetaData ) {
        // Your implementation here
        return this;
    }
}
```

2. **Implement the run() method**

Process the metadata query and generate your output format.

3. **Use helper methods**

Leverage AbstractTemplateStrategy's helper methods:
* `getPackageQuery()` - Filter by package
* `getFunctionQuery()` - Get methods
* `getPropertyQuery()` - Get properties
* `buildPackageTree()` - Create package hierarchy

4. **Register your strategy**

```javascript
new docbox.DocBox()
    .addStrategy( new path.to.MyCustomStrategy(
        outputDir: "/docs"
    ) )
    .generate( source: "/src", mapping: "app" );
```

---

## 💡 Usage Patterns

### Method Chaining

DocBox supports fluent method chaining:

```javascript
new docbox.DocBox()
    .addStrategy( "HTML", { outputDir: "/docs/html" } )
    .addStrategy( "JSON", { outputDir: "/docs/json" } )
    .generate( source: "/src", mapping: "app" );
```

### Multiple Strategies

Generate multiple output formats in one pass:

```javascript
var docbox = new docbox.DocBox();

docbox.addStrategy( "HTML", {
    outputDir: "/docs/html",
    projectTitle: "My API",
    theme: "default"
} );

docbox.addStrategy( "JSON", {
    outputDir: "/docs/json",
    projectTitle: "My API"
} );

docbox.addStrategy( "XMI", {
    outputFile: "/docs/diagram.uml"
} );

docbox.generate(
    source: expandPath( "/src" ),
    mapping: "myapp",
    excludes: "(tests|build)"
);
```

### Error Handling

```javascript
try {
    new docbox.DocBox()
        .addStrategy( "HTML", { outputDir: "/docs" } )
        .generate(
            source: "/src",
            mapping: "app",
            throwOnError: true  // Throw on invalid components
        );
} catch ( any e ) {
    // Handle errors
    writeLog( e.message );
    rethrow;
}
```

---

## 🔗 See Also

* [Configuration](../getting-started/configuration.md)
* [Custom Output Strategy](../output-formats/custom-output-strategy.md)
* [Troubleshooting](../getting-started/troubleshooting.md)
