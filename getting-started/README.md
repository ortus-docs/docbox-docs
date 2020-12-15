## Getting Started

1. [Installation](installation.md)
2. [Configuration](configuration.md)
3. [Supported Output Formats](#supported-formats)

## SYSTEM REQUIREMENTS

- Lucee 5+
- ColdFusion 2016+

## Supported Formats

DocBox supports several output formats:

* [HTML](output-formats/html.md)
* [JSON](output-formats/json.md)
* [UML](output-formats/uml.md)

Each format can be configured by its alias name (such as `"JSON"` or `"HTML"`) or its full class path, such as `docbox.strategy.api.HTMLAPIStrategy`. This enables you to create your own documentation strategy and use it to produce documentation in a custom, proprietary format.