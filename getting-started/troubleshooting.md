---
description: Common issues and solutions when using DocBox
icon: wrench
---

# Troubleshooting

This guide covers common issues you might encounter when using DocBox and their solutions.

## 🚨 Common Errors

### "Output directory does not exist"

**Error Message:**

```
The output directory [/path/to/docs] does not exist
```

**Cause:**
The specified output directory doesn't exist on the filesystem.

**Solution:**
Create the output directory before running DocBox, or ensure that the path is correct. You can create it manually or programmatically:

```javascript
// Option 1: Create the directory first
directoryCreate( expandPath( "/docs" ), true );

// Option 2: Use an existing directory
new docbox.DocBox()
    .addStrategy( "HTML", {
        outputDir: expandPath( "/existing/path" )
    } )
    .generate( source: "/src", mapping: "app" );
```

### Missing Source Mappings (CLI)

**Error Message:**

```
❌ ERROR: No valid source mappings found.
```

**Cause:** The BoxLang CLI command wasn't provided with source directory information.

**Solution:**
Ensure you provide either:

- `--source` and `--mapping` together
- One or more `--mappings:<name>=<path>` options
- JSON array via `--source`

```bash
# Correct usage
boxlang module:docbox --source=/src --mapping=app --output-dir=/docs

# Or with mappings
boxlang module:docbox --mappings:app=/src --output-dir=/docs
```

### "Cannot read properties of undefined (reading 'toLowerCase')"

**Cause:** JavaScript error in HTML templates when filtering methods with missing properties.

**Solution:** This was fixed in DocBox 5.0. Update to the latest version:

```bash
box update docbox
```

### Class Not Found

**Error Message:**

```
Class [myapp.MyClass] not found
```

**Cause:** The mapping specified doesn't match the actual package structure.

**Solution:**
Ensure your mapping matches your component path structure:

```javascript
// If your component is at: /src/models/User.cfc
// And its component declaration is: component { }
// And you access it via: new models.User()

new docbox.DocBox()
    .addStrategy( "HTML", { outputDir: "/docs" } )
    .generate(
        source  = expandPath( "/src" ),      // Source directory
        mapping = "models"                    // Base mapping
    );
```

### Exclusion Pattern Not Working

**Problem:** Files are still being documented despite exclusion pattern.

**Cause:** Exclusion patterns are applied to relative file paths, not absolute paths.

**Solution:**
Use patterns that match the relative path structure:

```javascript
// Correct - matches relative paths
excludes = "(tests|build|\.git)"

// Incorrect - won't match absolute paths
excludes = "/full/path/to/tests"
```

## 🔍 Metadata Issues

### Empty Documentation Pages

**Problem:** Generated docs show components but no methods/properties.

**Cause:** Components lack JavaDoc comments or metadata.

**Solution:**
Add proper documentation to your components:

```javascript
/**
 * User management service
 *
 * @author Your Name
 */
component {

    /**
     * Gets a user by ID
     *
     * @id The user ID
     * @return User object or null
     */
    public function getUser( required numeric id ) {
        // implementation
    }
}
```

### Generic Types Not Showing

**Problem:** Generic type annotations like `Array<User>` not appearing in docs.

**Cause:** Using standard `@returntype` instead of `@doc.type`.

**Solution:**
Use the `@doc.type` annotation:

```javascript
/**
 * Gets all active users
 *
 * @return Array of User objects
 * @doc.type Array<User>
 */
public array function getUsers() {
    return [];
}
```

### Implements Not Detected

**Problem:** Interface implementations not showing in documentation.

**Cause:** Engine-specific metadata format differences.

**Solution:**
DocBox 5.0+ handles both formats automatically. If using older versions, update:

```bash
box update docbox
```

## 🎨 HTML/UI Issues

### Dark Mode Not Persisting

**Problem:** Dark mode preference resets on page reload.

**Cause:** Browser localStorage might be disabled or cleared.

**Solution:**

1. Check browser console for localStorage errors
2. Enable localStorage in browser settings
3. Clear site data and try again

### Search Not Working

**Problem:** Method search doesn't filter results.

**Cause:** JavaScript not loading or Alpine.js initialization issue.

**Solution:**

1. Check browser console for errors
2. Ensure you're using a modern browser (Chrome, Firefox, Edge, Safari)
3. Clear browser cache and reload
4. Check network tab for failed asset loads

### Theme Not Loading

**Problem:** Documentation appears unstyled or broken.

**Cause:** Asset paths incorrect or theme not specified properly.

**Solution:**

```javascript
// Explicitly specify theme
new docbox.DocBox()
    .addStrategy( "HTML", {
        outputDir: "/docs",
        theme: "default"  // or "frames"
    } )
    .generate( source: "/src", mapping: "app" );
```

## 🛠️ Build Issues

### CLI Command Not Found

**Error Message:**

```
Command [module:docbox] not found
```

**Cause:** bx-docbox module not installed.

**Solution:**

```bash
# For CommandBox web runtimes
box install bx-docbox

# For BoxLang OS runtime
install-bx-module bx-docbox

# Verify installation
boxlang module:docbox --version
```

### Memory Issues with Large Codebases

**Problem:** DocBox runs out of memory when processing large projects.

**Solution:**

1. Increase JVM heap size

```bash
box config set server.jvm.heapSize=1024
```

1. Process in smaller chunks:

```javascript
// Document modules separately
new docbox.DocBox()
    .addStrategy( "HTML", { outputDir: "/docs/module1" } )
    .generate( source: "/src/module1", mapping: "module1" );

new docbox.DocBox()
    .addStrategy( "HTML", { outputDir: "/docs/module2" } )
    .generate( source: "/src/module2", mapping: "module2" );
```

1. Use more aggressive exclusion patterns:

```javascript
excludes = "(tests|specs|build|node_modules|\.git|vendor)"
```

### Build Hangs or Takes Too Long

**Problem:** Documentation generation appears to hang.

**Cause:** Processing too many files or infinite recursion in inheritance.

**Solution:**

1. Add verbose logging to see progress
2. Check for circular dependencies in your code
3. Exclude unnecessary directories
4. Run in smaller batches

## 🦤 BoxLang-Specific Issues

### BoxLang Module Not Loading

**Problem:** Module loads but CLI command errors out.

**Cause:** Module registration issue or conflicts.

**Solution:**

```bash
# Reinstall the module
box uninstall bx-docbox
box install bx-docbox

# Or force module reload
box reload
```

### Metadata Format Differences

**Problem:** Documentation differs between CFML and BoxLang engines.

**Cause:** BoxLang uses different metadata structure for some properties.

**Solution:**
DocBox 5.0+ automatically handles both formats. If you're on an older version:

```bash
box update docbox
```

## 📊 Strategy-Specific Issues

### JSON Output Empty

**Problem:** JSON files generated but contain no data.

**Cause:** Source directory or mapping incorrect.

**Solution:**
Verify your paths and mappings:

```javascript
new docbox.DocBox()
    .addStrategy( "JSON", {
        projectTitle: "My API",
        outputDir: expandPath( "/docs/json" )
    } )
    .generate(
        source: expandPath( "/src" ),  // Use expandPath()
        mapping: "app"
    );
```

### XMI/UML Strategy Fails

**Problem:** XMI strategy throws errors.

**Cause:** Missing or invalid output file path.

**Solution:**

```javascript
new docbox.DocBox()
    .addStrategy( "XMI", {
        outputFile: expandPath( "/docs/diagram.uml" )  // Not outputDir!
    } )
    .generate( source: "/src", mapping: "app" );
```

## 🔧 Debug Tips

### Enable Verbose Logging

Add debugging output to your generation script:

```javascript
try {
    var docbox = new docbox.DocBox()
        .addStrategy( "HTML", {
            outputDir: expandPath( "/docs" )
        } );

    writeDump( "Starting documentation generation..." );

    docbox.generate(
        source: expandPath( "/src" ),
        mapping: "app"
    );

    writeDump( "Generation complete!" );
} catch ( any e ) {
    writeDump( var=e, label="DocBox Error" );
    rethrow;
}
```

### Check Component Metadata

Verify your component metadata is readable:

```javascript
component = createObject( "component", "myapp.MyClass" );
metadata = getComponentMetadata( component );
writeDump( metadata );
```

### Validate Output Directory Permissions

Ensure DocBox can write to the output directory:

```javascript
testFile = expandPath( "/docs/test.txt" );
fileWrite( testFile, "test" );
fileDelete( testFile );
writeDump( "Output directory is writable" );
```

## 📞 Getting Help

If you're still experiencing issues:

1. **Check Documentation**: [docbox.ortusbooks.com](https://docbox.ortusbooks.com/)
2. **Search Issues**: [Jira Issue Tracker](https://ortussolutions.atlassian.net/projects/DOCBOX)
3. **Community Forums**: [Ortus Community](https://community.ortussolutions.com/)
4. **CFML Slack**: #box-products channel at [cfml-slack.herokuapp.com](http://cfml-slack.herokuapp.com/)
5. **Professional Support**: [Ortus Solutions](https://www.ortussolutions.com/services/support)

## 📝 Reporting Bugs

When reporting issues, please include:

* DocBox version (`box info docbox` or `boxlang module:docbox --version`)
* CFML engine and version
* Operating system
* Complete error message and stack trace
* Minimal code example to reproduce
* Expected vs actual behavior
