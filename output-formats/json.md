## JSON Output Format

## Schema

The JSON strategy outputs three types of files:

- [JSON Output Format](#json-output-format)
- [Schema](#schema)
- [Overview Summary](#overview-summary)
- [Package Summary](#package-summary)
- [myClass.json](#myclassjson)

## Overview Summary

DocBox's JSON strategy outputs a single `overview-summary.json` file in the root of the configured `outputDir` directory that documents all packages (component directories) and classes in the configured `source`.

```json
{
    "$id": "point-to-public-json-schema.json",
    "$schema": "http://json-schema.org/draft-07/schema#",
    "title": "Package documentation index",
    "description": "This class index links to each generated class documentation JSON file.",
    "required": [],
    "type": "object",
    "properties": {
        "title": {
            "type": "string"
        },
        "classes": {
            "type": "array",
            "items": {
                "type": "object",
                "properties": {
                    "name": {
                        "type": "string"
                    },
                    "path": {
                        "type": "string"
                    }
                }
            }
        },
        "packages": {
            "type": "object",
            "items": {
                "type": "object",
                "properties": {
                    "name": {
                        "type": "string"
                    },
                    "path": {
                        "type": "string"
                    }
                }
            }
        }
    }
}
```

See an example at [JSONSchemaValidator.net](https://www.jsonschemavalidator.net/s/1GwKCCI3)

## Package Summary

DocBox's JSON strategy outputs a `package-summary.json` file for every directory found in the configured `source` directory that contains at least one ColdFusion component.

* `source/autos/autoBuilder.cfc` will generate a `docs/source/autos/package-summary.json`

```json
{
    "$id": "point-to-public-json-schema.json",
    "$schema": "http://json-schema.org/draft-07/schema#",
    "title": "Package documentation index",
    "description": "Index file documenting each coldfusion component inside a package level - i.e. per directory.",
    "required": [],
    "type": "object",
    "properties": {
        "title": {
            "type": "string"
        },
        "classes": {
            "type": "array",
            "items": {
                "type": "object",
                "properties": {
                    "name": {
                        "type": "string"
                    },
                    "path": {
                        "type": "string"
                    }
                }
            }
        }
    }
}
```

See an example at [JSONSchemaValidator.net](https://www.jsonschemavalidator.net/s/98ToeO23)

## myClass.json

DocBox's JSON strategy outputs a single `class.json` file for every `.cfc` component found in the configured `source` directory.

The name of the file will reflect the component name, and the location will match the source directory hierarchy:

* `source/app/autos/autoBuilder.cfc` becomes `docs/source/app/autos/autoBuilder.json`
* `source/main.cfc` becomes `docs/source/main.json`

The component documentation will match this schema:

```json
{
    "$id": "point-to-public-json-schema.json",
    "$schema": "http://json-schema.org/draft-07/schema#",
    "title": "Class documentation",
    "description": "Documents a single class in a ColdFusion package.",
    "required": [],
    "definitions": {
        "function" : {
            "type" : "object",
            "properties": {
                "name" : { "type" : "string" },
                "hint" : { "type" : "string" },
                "description" : { "type" : "string" },
                "access" : { "type" : "string" },
                "parameters" : {
                    "type" : "array",
                    "items": { "$ref" : "#/definitions/parameter" }
                },
                "returnType" : { "type" : "string" },
                "returnFormat" : { "type" : "string" },
                "position" : {
                    "type" : "object",
                    "properties" : {
                        "start" : { "type" : "integer" },
                        "end" : { "type" : "integer" }
                    }
                }
            }
        },
        "parameter" : {
            "type" : "object",
            "properties": {
                "type" : { "type" : "string" },
                "name" : { "type" : "string" },
                "required" : { "type" : "boolean" },
                "default" : { "type" : "string" }
            }
        }
    },
    "type": "object",
    "properties": {
        "name" : { "type": "string" },
        "package" : { "type": "string" },
        "type" : { "type": "string" },
        "extends" : { "type" : "string" },
        "implements" : { "type" : "string" },
        "hint" : { "type" : "string" },
        "description" : { "type" : "string" },
        "properties" : {
            "description" : "Literally the component properties set via `property` or `cfproperty`.",
            "type" : "object",
            "properties": {
                "type" : { "type" : "string" },
                "name" : { "type" : "string" },
                "access" : { "type" : "string" },
                "hint" : { "type" : "string" },
                "default" : { "type" : "string" },
                "required" : { "type" : "boolean" }
            }
        },
        "constructor" : { "$ref": "#/definitions/function" },
        "functions" : {
            "type" : "array",
            "items" : { "$ref": "#/definitions/function" }
        }
    }
  }
```

See an example at [JSONSchemaValidator.net](https://www.jsonschemavalidator.net/s/6Py2AIDk)