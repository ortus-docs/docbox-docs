# BoxLang CLI Tool

🦤 DocBox 5.0+ includes a native BoxLang module with a powerful CLI tool for generating documentation directly from the command line.

## 📦 Installation

DocBox can be installed as a BoxLang core module using the `bx-docbox` slug:

### CommandBox Web Runtimes

```bash
box install bx-docbox
```

### BoxLang OS Runtime

```bash
install-bx-module bx-docbox
```

Once installed, the `boxlang module:docbox` command becomes available for generating documentation.

---

## 🎯 Usage

```bash
boxlang module:docbox [options]
```

### ⚙️ Required Options

| Option | Short | Description |
|--------|-------|-------------|
| `--output-dir=<path>` | `-o=<path>` | 📁 Output directory for generated docs |

### 📂 Source Options

| Option | Description |
|--------|-------------|
| `--source=<path>` | Source directory to document |
| `--mapping=<name>` | Base mapping for the source folder |
| `--mappings:<name>=<path>` | Define multiple source mappings |

### ⚙️ Additional Options

| Option | Short | Description |
|--------|-------|-------------|
| `--help` | `-h` | Show help information |
| `--version` | `-v` | Show version information |
| `--excludes=<regex>` | | Regex pattern to exclude files/folders |
| `--project-title=<title>` | | 📖 Project title for documentation |
| `--theme=<name>` | | 🎨 Theme name (`default` or `frames`) |
| `--strategy=<class>` | | Documentation strategy class (default: `docbox.strategy.api.HTMLAPIStrategy`) |

---

## 💡 Examples

### 📌 Basic Usage

Generate documentation for a single source directory:

```bash
boxlang module:docbox --source=/src/models \
                       --mapping=models \
                       --output-dir=/docs
```

### 📌 With Project Title and Excludes

```bash
boxlang module:docbox --source=/src \
                       --mapping=myapp \
                       --excludes="(tests|build)" \
                       --output-dir=/docs \
                       --project-title="My API"
```

### 📌 Short Form Output Directory

```bash
boxlang module:docbox --source=/src \
                       --mapping=app \
                       -o=/docs
```

### 📌 Multiple Source Mappings

Document multiple source directories with different mappings:

```bash
boxlang module:docbox --mappings:v1=/src/v1/models \
                       --mappings:v2=/src/v2/models \
                       --output-dir=/docs \
                       --project-title="API Docs"
```

### 📌 Using Frames Theme

Generate documentation with the traditional frameset layout:

```bash
boxlang module:docbox --source=/src \
                       --mapping=app \
                       --output-dir=/docs \
                       --theme=frames
```

### 📌 JSON Array Format

Specify multiple sources using JSON array notation:

```bash
boxlang module:docbox --source="[{'dir':'/src/models', 'mapping':'models'}, {'dir':'/src/services', 'mapping':'services'}]" \
                       --output-dir=/docs \
                       --project-title="My API"
```

### 📌 Real-World Example: ColdBox Framework

```bash
boxlang module:docbox --source=tests/resources/coldbox \
                       --mapping=coldbox \
                       --excludes="(tests|build)" \
                       --output-dir=tests/apidocs \
                       --project-title="ColdBox Framework" \
                       --theme=default
```

---

## 🔧 Command Output

When you run the CLI tool, you'll see output like this:

```
═══════════════════════════════════════════════════════════════════
  📚 DocBox Documentation Generator
═══════════════════════════════════════════════════════════════════

📂 Source:  /Users/myapp/src/models
🔗 Mapping: models
📁 Output:  /Users/myapp/docs

⏳ Starting generation, please wait...

🥊 Generation complete!
Documentation available at: /Users/myapp/docs
```

---

## 🆘 Getting Help

### Show Help

```bash
boxlang module:docbox --help
```

This displays comprehensive usage information including:
- Command syntax
- All available options
- Multiple examples
- Links to documentation

### Show Version

```bash
boxlang module:docbox --version
```

Displays:
- DocBox version
- Author information
- Website URL

---

## ⚠️ Common Issues

### Missing Source Mappings

**Error:**
```
❌ ERROR: No valid source mappings found.
```

**Solution:** Ensure you provide either:
- `--source` and `--mapping` together
- One or more `--mappings:<name>=<path>` options
- JSON array via `--source`

### Missing Output Directory

**Error:**
```
❌ ERROR: --output-dir is required
```

**Solution:** Always specify where to generate documentation:
```bash
boxlang module:docbox --source=/src --mapping=app --output-dir=/docs
```

### Source Directory Not Found

**Warning:**
```
⚠️  Warning: '/path/to/source' does not exist.
```

**Solution:** Verify the source path exists and is accessible. Use absolute paths or paths relative to your current working directory.

---

## 🎨 Theme Selection

DocBox 5.0+ includes two modern themes:

### Default Theme (Alpine.js SPA)

```bash
boxlang module:docbox --source=/src --mapping=app \
                       --output-dir=/docs \
                       --theme=default
```

Features:
- ⚡ Alpine.js-based SPA
- 🌓 Dark mode support
- 🔍 Real-time search
- 📑 Method tabs
- 💜 Modern purple design

### Frames Theme (Traditional)

```bash
boxlang module:docbox --source=/src --mapping=app \
                       --output-dir=/docs \
                       --theme=frames
```

Features:
- 🗂️ Traditional frameset layout
- 📚 jstree navigation
- 📱 Left sidebar for packages
- 🎯 Bootstrap 5 styling

---

## 🔗 Integration with Build Scripts

### CommandBox Task Runner

Create a `task.cfc` to generate documentation:

```java
component {
    function run() {
        command( "boxlang" )
            .params(
                "module:docbox",
                "--source=#getCWD()#/models",
                "--mapping=models",
                "--output-dir=#getCWD()#/docs",
                "--project-title=My Project",
                "--theme=default"
            )
            .run();
    }
}
```

Run with: `box task run`

### CI/CD Pipeline

Add to your GitHub Actions, GitLab CI, or other CI/CD pipeline:

```yaml
- name: Generate API Documentation
  run: |
    boxlang module:docbox \
      --source=./src \
      --mapping=myapp \
      --output-dir=./build/docs \
      --project-title="My Application" \
      --theme=default
```

---

## 📚 Next Steps

- [Configuration Options](configuration.md) - Learn about strategy properties and advanced configuration
- [HTML Output](../output-formats/html-output.md) - Explore HTML theme features
- [Annotating Your Code](annotating-your-code.md) - Write effective JavaDoc comments
