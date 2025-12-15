---
description: Generate browsable HTML documentation for your application CFCs
---

# HTML Output

The HTML API Strategy is used to create CFC documentation based on [Javadoc](https://www.oracle.com/java/technologies/javase/javadoc-tool.html). DocBox does not fully support all the Javadoc syntax, but hopefully it will soon.

## Modern Themes (New in 5.0)

DocBox 5.0 introduces a completely redesigned HTML output with two professional themes:

### Default Theme - Modern SPA

The default theme features:

* **Alpine.js-based SPA** - Client-side routing and dynamic filtering
* **Dark Mode Support** - Toggle between light and dark themes with persistence
* **Real-time Search** - Live method filtering with keyboard navigation (Enter/Shift+Enter)
* **Modern UI** - Bootstrap 5, purple gradient accents, emoji indicators
* **Responsive Design** - Mobile-friendly layouts
* **Method Tabs** - Filter by All/Public/Private/Static/Abstract
* **Smooth Scrolling** - Enhanced navigation experience

### Frames Theme - Traditional Layout

The frames theme provides:

* **Frameset-based Layout** - Classic three-panel documentation view
* **Bootstrap 5 Styling** - Modern component design
* **Package Navigation** - Left sidebar with hierarchical tree
* **Dark Mode Support** - Consistent theming across all panels
* **Traditional UX** - Familiar navigation pattern

## Instantiate DocBox

Begin by creating an instance of `DocBox`:

```javascript
docbox = new DocBox();
```

### Properties

The following are the properties for this strategy:

* `projectTitle` : The HTML title used in the documentation
* `outputDir` : The output directory absolute path
* `theme` : (Optional) Theme name - `"default"` or `"frames"` (defaults to `"default"`)

Just pass them in the `docbox.addStrategy()` call:

```javascript
docbox = new DocBox();
docbox.addStrategy( "HTML", {
    projectTitle : "My Docs",
    outputDir    : expandPath( "/mydocs" ),
    theme        : "default"  // or "frames"
} );
```

### Using the Frames Theme

To use the traditional frameset layout:

```javascript
docbox = new DocBox();
docbox.addStrategy( "HTML", {
    projectTitle : "My API Docs",
    outputDir    : expandPath( "/mydocs" ),
    theme        : "frames"
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
