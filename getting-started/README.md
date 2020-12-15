## Getting Started

1. [Installation](installation.md)
2. [Configuration](configuration.md)
3. [Supported Output Formats](#supported-formats)

## Supported Output Formats

DocBox supports several output formats:

* [HTML](output-formats/html.md)
* [JSON](output-formats/json.md)
* [UML](output-formats/uml.md)

Each format is configured by its alias name, such as `"JSON"` or `"HTML"`.

```js
var docbox = new docbox.DocBox();
docbox.addStrategy( "UML", { outputFile : "./tmp/docs/app-diagram.uml" })
```

For backwards compatibility, specifying the full class path is still supported, as is specifying a single strategy when initializing DocBox:

```js
variables.docbox = new docbox.DocBox(
  strategy = "docbox.strategy.uml2tools.XMIStrategy",
  properties={ 
    projectTitle = "DocBox Tests",
    outputFile   = variables.testOutputFile
  }
);
```

### Custom Output Strategy

In addition to the mainstream output formats, you can extend DocBox's `AbstractTemplateStrategy` component to generate your own custom-formatted documentation:

```js
component extends="docbox.strategy.AbstractTemplateStrategy" accessors="true"{
   /**
    * Generate JSON documentation
    * 
    * @metadata All component metadata, sourced from DocBox.
    */
   component function run( required query metadata ){
      // generate custom documentation format from arguments.metadata
   }
}
```