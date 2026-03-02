# Quarto Inspect

## Overview

The `quarto inspect` command produces a JSON object with information about the configuration of a Quarto project or document. This information is particularly useful for authors of downstream tools and libraries which analyze Quarto content.

Whenever possible, we recommend using `quarto inspect` instead of direct inspection of documents or projects.

## Information available

`quarto inspect` provides information for Quarto projects, for individual documents outside of projects, and for documents within a project.

### Document-level information

Document-level information is obtained by calling `quarto inspect <DOCUMENT>`. If no additional parameters are given, the output is produced on standard output. If an additional parameter is given, the output is written to the specified path.

- `quarto`: an object describing the quarto version
- `engines`: the engine used in the document, as a singleton array (for simplicity of the schema, in compatibility with the project-wide information below)
- `formats`: an object whose keys are the document format name, and values are metadata associated with the document.
- `resources`: an array of paths describing additional resources required for the document to be rendered.
- `fileInformation`: an object whose keys are file names, and values are objects describing:
  - `includeMap`: an array of `source` and `target` paths describing the use of `include` shortcodes
  - `codeCells`: an array of objects describing the code cells in the document (including those referenced to from an include). The object has:
    - `start`: the line where the code cell starts
    - `end`: the line where the code cell ends
    - `file`: the path of the file where the code cell resides (this can be different from the original file because of includes)
    - `source`: the content of the code cell
    - `language`: the language of the code cell
    - `metadata`: the cell-level metadata for the code cell
- `project`: If the document is part of a project, then this contains the output that would be produced by `quarto inspect` on the project

### Project-level information

Project-level information is obtained by calling `quarto inspect` within a project, or explicitly passing a path, `quarto inspect <PATH_TO_PROJECT>`. If no additional parameters are given, the output is produced on standard output. If an additional parameter is given, the output is written to the specified path.

- `quarto`: an object describing the quarto version
- `dir`: the path to the directory where the project resides
- `engines`: an array of strings listing the engines used in the project.
- `config`: the project configuration metadata in JSON format
- `files`: information about the project files in an object. The object has:
  - `input`: an array of paths listing the input files
  - `resources`: an array of paths describing additional resources required for the project to be rendered.
  - `config`: the YAML configuration files that make up this project’s configuration
  - `configResources`: an array of paths describing resources that are implied by the project configuration.
- `fileInformation`: an object containing information about each of the documents to be rendered by the project. The keys of this object are the document paths, and the values are themselves objects with the following keys:
  - `includeMap`: an array of `source` and `target` paths describing the use of `include` shortcodes
  - `codeCells`: an array of objects describing the code cells in the document (including those referenced to from an include). The object has:
    - `start`: the line where the code cell starts
    - `end`: the line where the code cell ends
    - `file`: the path of the file where the code cell resides (this can be different from the original file because of includes)
    - `source`: the content of the code cell
    - `language`: the language of the code cell
    - `metadata`: the cell-level metadata for the code cell
- `extensions`: an array of objects containing information about extensions installed in the project. The precise description of the information provided in each object is given by the [TypeScript interface `Extension` in Quarto’s source code](https://github.com/quarto-dev/quarto-cli/blob/main/src/extension/types.ts#L29-L44) (We do not expect this interface to change, but we reserve the right to do so if needed).

## JSON Schemas

### Project data

This schema is also available as a [standalone file](./quarto-inspect-project-json-schema.json).

``` json
{
    "type": "object",
    "title": "Project Information",
    "description": "Information about a Quarto project",
    "properties": {
        "quarto": {
            "type": "object",
            "properties": {
                "version": { "type": "string" }
            }
        },
        "dir": {
            "type": "string",
            "description": "The path of the project directory"
        },
        "engines": {
            "type": "array",
            "items": { "type": "string" },
            "description": "The engines used in the project"
        },
        "config": {
            "type": "object",
            "description": "Resolved project configuration in JSON format"
        },
        "files": {
            "type": "object",
            "properties": {
                "input": {
                    "type": "array",
                    "items": { "type": "string" },
                    "description": "The input files in the project"
                },
                "resources": {
                    "type": "object",
                    "properties": {
                        "type": "array",
                        "items": { "type": "string" },
                        "description": "The resource files explicitly provided in the project"
                    }
                },
                "configResources": {
                    "type": "object",
                    "properties": {
                        "type": "array",
                        "items": { "type": "string" },
                        "description": "The resource files implied by the project configuration"
                    }
                },
                "config": {
                    "type": "array",
                    "items": { "type": "string" },
                    "description": "The configuration files in the project"
                }
            }
        },
        "fileInformation": {
            "additionalProperties": {
                "type": "object",
                "properties": {
                    "includeMap": {
                        "type": "array",
                        "items": {
                            "type": "object",
                            "properties": {
                                "source": { "type": "string" },
                                "target": { "type": "string" }
                            }
                        }
                    },
                    "codeCells": {
                        "type": "array",
                        "items": {
                            "type": "object",
                            "properties": {
                                "start": { "type": "integer" },
                                "end": { "type": "integer" },
                                "file": { "type": "string" },
                                "source": { "type": "string" },
                                "language": { "type": "string" },
                                "metadata": { "type": "object" }
                            }
                        }
                    }
                }
            }
        },
        "extensions": { "type": "array", "items": { "type": "object" } }        
    }
}
```

### Document data

This schema is also available as a [standalone file](./quarto-inspect-document-json-schema.json).

``` json
{
    "type": "object",
    "properties": {
        "quarto": {
            "type": "object",
            "properties": {
                "version": { "type": "string" }
            },
            "description": "The version of Quarto used to inspect the document"
        },
        "engines": {
            "type": "array",
            "items": { "type": "string" },
            "description": "The engines used in the document"
        },
        "formats": {
            "type": "object",
            "additionalProperties": { "type": "object" },
            "description": "An object representing the formats used in the document (keys) and their configuration (values)"
        },
        "resources": {
            "type": "array",
            "items": { "type": "string" },
            "description": "The resource files explicitly provided in the document"
        },
        "fileInformation": {
            "additionalProperties": {
                "type": "object",
                "properties": {
                    "includeMap": {
                        "type": "array",
                        "items": {
                            "type": "object",
                            "properties": {
                                "source": { "type": "string" },
                                "target": { "type": "string" }
                            }
                        }
                    },
                    "codeCells": {
                        "type": "array",
                        "items": {
                            "type": "object",
                            "properties": {
                                "start": { "type": "integer" },
                                "end": { "type": "integer" },
                                "file": { "type": "string" },
                                "source": { "type": "string" },
                                "language": { "type": "string" },
                                "metadata": { "type": "object" }
                            }
                        }
                    }
                }
            }
        },
        "project": {
            "$ref": "quarto-inspect-project-json-schema.json"
        }
    }
}
```
