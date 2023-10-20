# Configuration

### **Supported Output Formats**

DocBox offers several built-in output formats as well as enabling you to [create your own](../output-formats/custom-output-strategy.md):

* [HTML](https://app.gitbook.com/s/-MO7676VkvjpkgbE8J5a/getting-started/output-formats/html.md)
* [JSON](https://app.gitbook.com/s/-MO7676VkvjpkgbE8J5a/getting-started/output-formats/json.md)
* [UML](https://app.gitbook.com/s/-MO7676VkvjpkgbE8J5a/getting-started/output-formats/uml.md)

Each format is configured by its alias name, such as `"JSON"` or `"HTML"`.

```javascript
var docbox = new docbox.DocBox();
docbox.addStrategy( "UML", { outputFile : "./tmp/docs/app-diagram.uml" })
```

### Backwards Compatibility

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

```javascript
new docbox.DocBox()
    .addStrategy( "HTML", {
        projectTitle : "CommandBox",
        outputDir : expandPath( './docs' )
    } )
    .generate(
       source = expandPath( "/app" ),
       mapping = "app",
       excludes="(coldbox)"
    );
```

### Generating Multiple Outputs

You can call the `.addStrategy()` method multiple times to specify multiple output formats:

```javascript
new docbox.DocBox()
   .addStrategy( "HTML", {
      projectTitle="My Docs",
      outputDir="#expandPath( '/docs/html' )#"
   } )
   .addStrategy( "JSON", {
      projectTitle="My Docs",
      outputDir="#expandPath( '/docs/json' )#"
   } )
   .generate(
      source = expandPath( "/app" ),
      mapping = "app",
      excludes="(coldbox)"
   );
```
