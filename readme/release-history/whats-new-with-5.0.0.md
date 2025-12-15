# What's New With 5.0.0

## 🎉 Major Release - BoxLang Support & Modern UI Overhaul

### BREAKING CHANGES

* Minimum CFML engine requirements updated:
  * Lucee 5.x minimum (dropped Lucee 4.x)
  * Adobe ColdFusion 2018+ (dropped ACF 2016, 2018)
* HTML output now uses Bootstrap 5 (previously Bootstrap 3)
* Default theme structure reorganized with new Alpine.js-based SPA architecture

### NEW - BoxLang Support 🚀

* **Full BoxLang 1.0+ Runtime Support** - DocBox now runs natively on BoxLang
* **BoxLang CLI Module** - New `boxlang module:docbox` command for generating docs from BoxLang CLI
  * `boxlang module:docbox --source=/path --mapping=app --output-dir=/docs`
  * Support for multiple source mappings
  * JSON array format support for complex project structures
  * Built-in help system with `--help` and `--version` flags
* **Dual Format Metadata Handling** - Automatically detects and handles both BoxLang array format and CFML struct format for `implements` metadata
* **ModuleConfig.bx** - Native BoxLang module configuration for seamless integration

### NEW - Modern HTML Theme System 🎨

* **Two Professional Themes**:
  * **Default Theme** - Modern Alpine.js SPA with client-side routing and dynamic filtering
  * **Frames Theme** - Traditional frameset-based layout with Bootstrap 5
* **Theme Selection** - Choose themes via `theme` property:
  ```javascript
  new docbox.DocBox()
      .addStrategy( "HTML", {
          outputDir : "/docs",
          theme     : "default" // or "frames"
      } )
  ```
* **Dark Mode Support** - Full dark/light theme toggle with localStorage persistence
* **Responsive Design** - Mobile-friendly layouts with proper breakpoints

### NEW - Enhanced UI/UX Features 💎

* **Modern Color Scheme** - Purple gradient accents (#5e72e4), softer colors, reduced blue overload
* **Visual Indicators** - Emoji badges throughout:
  * 📚 Packages, 📁 Folders, 🔌 Interfaces, 📦 Classes
  * 🟢 Public, 🔒 Private, ⚡ Static, 📝 Abstract
* **Real-time Method Search** - Live filtering with keyboard navigation
  * Search methods by name or signature
  * Navigate results with Enter/Shift+Enter
  * Visual highlighting and auto-scroll
  * Clear with Escape key
* **Method Tabs** - Tabbed interface for filtering methods (All/Public/Private/Static/Abstract)
* **Bootstrap Tooltips** - Contextual help on visibility badges and deprecated methods
* **Smooth Scrolling** - Enhanced navigation with smooth scroll behavior
* **Auto-expanding Navigation** - jstree automatically expands first 2 levels for better UX

### NEW - Complete Relationship Documentation 📊

* **All Known Implementing Classes** - Interfaces now show all classes that implement them
* **All Known Subclasses/Subinterfaces** - Display complete inheritance hierarchy
* **Fixed Inheritance Queries** - Properly handles both current class and ancestor interfaces
* **Improved Package Highlighting** - Subtle left border instead of full background

### NEW - Developer Experience Improvements 🛠️

* **Enhanced JavaDoc Support** - Comprehensive documentation with `<br>` tags for BoxLang compatibility
* **50+ Updated Code Examples** - All strategy files updated with proper line breaks
* **Improved Error Messages** - Better validation and user-friendly CLI output
* **Modern JavaScript** - ES6+ features with proper spacing conventions
* **CSS Custom Properties** - Comprehensive theming system with CSS variables

### NEW - Strategy Enhancements 📝

* **CommandBox Strategy** - Enhanced CLI command documentation with namespace support
* **JSON Strategy** - Machine-readable JSON with hierarchical package structure
* **XMI/UML Strategy** - Enhanced property inference and generic type support
* **Abstract Template Strategy** - Improved helper methods for all strategies

### IMPROVED

* **Build System** - Updated build process with BoxLang support
* **Testing** - Multi-engine testing (Lucee 5/6, Adobe 2023/2025, BoxLang 1.0/BE)
* **Documentation** - Comprehensive updates for all new features
* **Code Formatting** - Consistent CFFormat rules across entire codebase
* **Performance** - Optimized query operations and template rendering

### FIXED

* **Metadata Format Handling** - `getImplements()` now properly handles both array and struct formats
* **Interface Implementation Display** - Fixed empty queries for implementing classes
* **Package Navigation** - Improved CSS styling for better UX
* **Line Break Handling** - Workaround for BoxLang metadata line break stripping
* **Inheritance Detection** - Properly checks current class before ancestors

### TECHNICAL DETAILS

* **Bootstrap 5.3.2** - Modern component syntax and data-bs-* attributes
* **Bootstrap Icons 1.11.2** - Comprehensive icon set for UI elements
* **Alpine.js** - Lightweight reactive framework for SPA theme
* **CSS Architecture** - CSS custom properties for theming with light/dark mode
* **JavaScript Conventions** - Proper spacing in all control structures and function calls

### MIGRATION NOTES

#### From 4.x to 5.0

1. **Minimum Requirements**: Ensure you're running Lucee 5+, Adobe 2018+, or BoxLang 1.0+
2. **HTML Output**: The default theme now uses Bootstrap 5. If you have custom CSS, review for compatibility
3. **Theme Selection**: Explicitly set `theme="frames"` if you prefer the traditional frameset layout
4. **BoxLang Users**: Use the new `boxlang module:docbox` CLI command for native BoxLang integration

#### Updating HTML Customizations

If you extended the HTML strategy:
* Update Bootstrap 3 classes to Bootstrap 5 equivalents
* Review custom CSS for CSS custom property compatibility
* Test dark mode if you have custom themes

### UPGRADE INSTRUCTIONS

```bash
# CommandBox users
box update docbox

# BoxLang users
boxlang install docbox

# Verify installation
box package show version
```

### COMMUNITY

* GitHub Issues: https://github.com/Ortus-Solutions/DocBox/issues
* Documentation: https://docbox.ortusbooks.com
* Community Forum: https://community.ortussolutions.com
