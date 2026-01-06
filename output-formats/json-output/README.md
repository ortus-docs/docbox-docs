---
description: >-
  Generate JSON output for easy documentation imports into other documentation
  tools and platforms.
icon: cloud-binary
---

# JSON Output

📋 Generate machine-readable JSON documentation for easy imports into other documentation tools and platforms.

## 🚀 Instantiate DocBox

Begin by creating an instance of `DocBox`:

```javascript
docbox = new DocBox();
```

### ⚙️ Properties

The following are the properties for this strategy:

* `projectTitle` : Used in the top-level `overview-summary.json` file
* `outputDir` : The output directory absolute path

Just pass them in the `docbox.addStrategy()` call:

```javascript
docbox = new DocBox();
docbox.addStrategy( "JSON",
  {
      projectTitle = "DocBox API",
      outputDir = expandPath( "/resources/tmp" )
  } );
```

## 📝 Generate Documentation

Now that you have an instance of DocBox configured with your strategy and its properties, just execute the `generate()` method with its appropriate arguments:

```javascript
docbox.generate(
    source  = "#expandPath( '/docbox' )",
    mapping = "coldbox",
    excludes = "tests"
);
```
