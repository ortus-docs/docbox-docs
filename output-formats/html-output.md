---
description: Generate browsable HTML documentation for your application CFCs
---

# HTML Output

The HTML API Strategy is used to create CFC documentation based on [Javadoc](https://www.oracle.com/java/technologies/javase/javadoc-tool.html). DocBox does not fully support all the Javadoc syntax, but hopefully it will soon.

## Instantiate DocBox

Begin by creating an instance of `DocBox`:

```javascript
docbox = new DocBox();
```

### Properties

The following are the properties for this strategy:

* `projectTitle` : The HTML title used in the documentation
* `outputDir` : The output directory absolute path

Just pass them in the `docbox.addStrategy()` call:

```javascript
docbox = new DocBox();
docbox.addStrategy( "HTML",
  {
      projectTitle = "My Docs",
      outputDir = expandPath( "/mydocs" )  
  } );
```

## Generate Documentation

Now that you have an instance of DocBox configured with your strategy and its properties, just execute the `generate()` method with its appropriate arguments:

```javascript
docbox.generate(
    source  = "#expandPath( '/docbox' )",
    mapping = "coldbox",
    excludes = "tests"
);
```

