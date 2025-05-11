[ComfyUI home page![logo](https://mintlify.s3.us-west-1.amazonaws.com/dripart/logo.png)](http://docs.comfy.org/)

Search or ask...

Development

##### ComfyUI Server

- [Server Overview](http://docs.comfy.org/essentials/comfyui-server/comms_overview)
- [Messages](http://docs.comfy.org/essentials/comfyui-server/comms_messages)
- [Execution Model Inversion Guide](http://docs.comfy.org/essentials/comfyui-server/execution_model_inversion_guide)

##### CLI

- [Getting Started](http://docs.comfy.org/comfy-cli/getting-started)
- [Reference](http://docs.comfy.org/comfy-cli/reference)

##### Develop Custom Nodes

- [Overview](http://docs.comfy.org/custom-nodes/overview)
- [Getting Started](http://docs.comfy.org/custom-nodes/walkthrough)
- Backend
- UI
- [Workflow templates](http://docs.comfy.org/custom-nodes/workflow_templates)
- [Tips](http://docs.comfy.org/custom-nodes/tips)

##### Registry

- [Overview](http://docs.comfy.org/registry/overview)
- [Publishing Nodes](http://docs.comfy.org/registry/publishing)
- [Standards](http://docs.comfy.org/registry/standards)
- [Custom Node CI/CD](http://docs.comfy.org/registry/cicd)
- [pyproject.toml](http://docs.comfy.org/registry/specifications)
- [](http://docs.comfy.org/)

##### Specifications

- Workflow JSON
- Node Definitions
  
  - [Node Definition JSON](http://docs.comfy.org/specs/nodedef_json)
  - [Node Definition JSON 1.0](http://docs.comfy.org/specs/nodedef_json_1_0)

<!--THE END-->

- [comfyanonymous/ComfyUI](https://github.com/comfyanonymous/ComfyUI)
  
  ![US](https://purecatamphetamine.github.io/country-flag-icons/1x1/US.svg)
  
  English

[ComfyUI home page![logo](https://mintlify.s3.us-west-1.amazonaws.com/dripart/logo.png)](http://docs.comfy.org/)

![US](https://purecatamphetamine.github.io/country-flag-icons/1x1/US.svg)

English

Search or ask...

- [comfyanonymous/ComfyUI](https://github.com/comfyanonymous/ComfyUI)
- [comfyanonymous/ComfyUI](https://github.com/comfyanonymous/ComfyUI)

Search...

Navigation

Node Definition JSON 1.0

# Node Definition JSON 1.0

JSON schema for a ComfyUI Node.

## [​](http://docs.comfy.org#v1-0) v1.0

Node Definition v1.0

```json
{
  "$ref": "#/definitions/ComfyNodeDefV1",
  "definitions": {
    "ComfyNodeDefV1": {
      "type": "object",
      "properties": {
        "input": {
          "type": "object",
          "properties": {
            "required": {
              "type": "object",
              "additionalProperties": {
                "anyOf": [
                  {
                    "type": "array",
                    "minItems": 2,
                    "maxItems": 2,
                    "items": [
                      {
                        "type": "string",
                        "const": "INT"
                      },
                      {
                        "anyOf": [
                          {
                            "not": {}
                          },
                          {
                            "type": "object",
                            "properties": {
                              "default": {
                                "anyOf": [
                                  {
                                    "type": "number"
                                  },
                                  {
                                    "type": "array",
                                    "items": {
                                      "type": "number"
                                    }
                                  }
                                ]
                              },
                              "defaultInput": {
                                "type": "boolean"
                              },
                              "forceInput": {
                                "type": "boolean"
                              },
                              "tooltip": {
                                "type": "string"
                              },
                              "hidden": {
                                "type": "boolean"
                              },
                              "advanced": {
                                "type": "boolean"
                              },
                              "rawLink": {
                                "type": "boolean"
                              },
                              "lazy": {
                                "type": "boolean"
                              },
                              "min": {
                                "type": "number"
                              },
                              "max": {
                                "type": "number"
                              },
                              "step": {
                                "type": "number"
                              },
                              "display": {
                                "type": "string",
                                "enum": [
                                  "slider",
                                  "number",
                                  "knob"
                                ]
                              },
                              "control_after_generate": {
                                "type": "boolean"
                              }
                            },
                            "additionalProperties": true
                          }
                        ]
                      }
                    ]
                  },
                  {
                    "type": "array",
                    "minItems": 2,
                    "maxItems": 2,
                    "items": [
                      {
                        "type": "string",
                        "const": "FLOAT"
                      },
                      {
                        "anyOf": [
                          {
                            "not": {}
                          },
                          {
                            "type": "object",
                            "properties": {
                              "default": {
                                "anyOf": [
                                  {
                                    "type": "number"
                                  },
                                  {
                                    "type": "array",
                                    "items": {
                                      "type": "number"
                                    }
                                  }
                                ]
                              },
                              "defaultInput": {
                                "type": "boolean"
                              },
                              "forceInput": {
                                "type": "boolean"
                              },
                              "tooltip": {
                                "type": "string"
                              },
                              "hidden": {
                                "type": "boolean"
                              },
                              "advanced": {
                                "type": "boolean"
                              },
                              "rawLink": {
                                "type": "boolean"
                              },
                              "lazy": {
                                "type": "boolean"
                              },
                              "min": {
                                "type": "number"
                              },
                              "max": {
                                "type": "number"
                              },
                              "step": {
                                "type": "number"
                              },
                              "display": {
                                "type": "string",
                                "enum": [
                                  "slider",
                                  "number",
                                  "knob"
                                ]
                              },
                              "round": {
                                "anyOf": [
                                  {
                                    "type": "number"
                                  },
                                  {
                                    "type": "boolean",
                                    "const": false
                                  }
                                ]
                              }
                            },
                            "additionalProperties": true
                          }
                        ]
                      }
                    ]
                  },
                  {
                    "type": "array",
                    "minItems": 2,
                    "maxItems": 2,
                    "items": [
                      {
                        "type": "string",
                        "const": "BOOLEAN"
                      },
                      {
                        "anyOf": [
                          {
                            "not": {}
                          },
                          {
                            "type": "object",
                            "properties": {
                              "default": {
                                "type": "boolean"
                              },
                              "defaultInput": {
                                "type": "boolean"
                              },
                              "forceInput": {
                                "type": "boolean"
                              },
                              "tooltip": {
                                "type": "string"
                              },
                              "hidden": {
                                "type": "boolean"
                              },
                              "advanced": {
                                "type": "boolean"
                              },
                              "rawLink": {
                                "type": "boolean"
                              },
                              "lazy": {
                                "type": "boolean"
                              },
                              "label_on": {
                                "type": "string"
                              },
                              "label_off": {
                                "type": "string"
                              }
                            },
                            "additionalProperties": true
                          }
                        ]
                      }
                    ]
                  },
                  {
                    "type": "array",
                    "minItems": 2,
                    "maxItems": 2,
                    "items": [
                      {
                        "type": "string",
                        "const": "STRING"
                      },
                      {
                        "anyOf": [
                          {
                            "not": {}
                          },
                          {
                            "type": "object",
                            "properties": {
                              "default": {
                                "type": "string"
                              },
                              "defaultInput": {
                                "type": "boolean"
                              },
                              "forceInput": {
                                "type": "boolean"
                              },
                              "tooltip": {
                                "type": "string"
                              },
                              "hidden": {
                                "type": "boolean"
                              },
                              "advanced": {
                                "type": "boolean"
                              },
                              "rawLink": {
                                "type": "boolean"
                              },
                              "lazy": {
                                "type": "boolean"
                              },
                              "multiline": {
                                "type": "boolean"
                              },
                              "dynamicPrompts": {
                                "type": "boolean"
                              },
                              "defaultVal": {
                                "type": "string"
                              },
                              "placeholder": {
                                "type": "string"
                              }
                            },
                            "additionalProperties": true
                          }
                        ]
                      }
                    ]
                  },
                  {
                    "type": "array",
                    "minItems": 2,
                    "maxItems": 2,
                    "items": [
                      {
                        "type": "array",
                        "items": {
                          "type": [
                            "string",
                            "number"
                          ]
                        }
                      },
                      {
                        "anyOf": [
                          {
                            "not": {}
                          },
                          {
                            "type": "object",
                            "properties": {
                              "default": {},
                              "defaultInput": {
                                "type": "boolean"
                              },
                              "forceInput": {
                                "type": "boolean"
                              },
                              "tooltip": {
                                "type": "string"
                              },
                              "hidden": {
                                "type": "boolean"
                              },
                              "advanced": {
                                "type": "boolean"
                              },
                              "rawLink": {
                                "type": "boolean"
                              },
                              "lazy": {
                                "type": "boolean"
                              },
                              "control_after_generate": {
                                "type": "boolean"
                              },
                              "image_upload": {
                                "type": "boolean"
                              },
                              "image_folder": {
                                "type": "string",
                                "enum": [
                                  "input",
                                  "output",
                                  "temp"
                                ]
                              },
                              "allow_batch": {
                                "type": "boolean"
                              },
                              "video_upload": {
                                "type": "boolean"
                              },
                              "remote": {
                                "type": "object",
                                "properties": {
                                  "route": {
                                    "anyOf": [
                                      {
                                        "type": "string",
                                        "format": "uri"
                                      },
                                      {
                                        "type": "string",
                                        "pattern": "^\\/"
                                      }
                                    ]
                                  },
                                  "refresh": {
                                    "anyOf": [
                                      {
                                        "type": "number",
                                        "minimum": -9007199254740991,
                                        "maximum": 9007199254740991
                                      },
                                      {
                                        "type": "number",
                                        "maximum": 9007199254740991,
                                        "minimum": -9007199254740991
                                      }
                                    ]
                                  },
                                  "response_key": {
                                    "type": "string"
                                  },
                                  "query_params": {
                                    "type": "object",
                                    "additionalProperties": {
                                      "type": "string"
                                    }
                                  },
                                  "refresh_button": {
                                    "type": "boolean"
                                  },
                                  "control_after_refresh": {
                                    "type": "string",
                                    "enum": [
                                      "first",
                                      "last"
                                    ]
                                  },
                                  "timeout": {
                                    "type": "number",
                                    "minimum": 0
                                  },
                                  "max_retries": {
                                    "type": "number",
                                    "minimum": 0
                                  }
                                },
                                "required": [
                                  "route"
                                ],
                                "additionalProperties": false
                              },
                              "options": {
                                "type": "array",
                                "items": {
                                  "type": [
                                    "string",
                                    "number"
                                  ]
                                }
                              }
                            },
                            "additionalProperties": true
                          }
                        ]
                      }
                    ]
                  },
                  {
                    "type": "array",
                    "minItems": 2,
                    "maxItems": 2,
                    "items": [
                      {
                        "type": "string",
                        "const": "COMBO"
                      },
                      {
                        "anyOf": [
                          {
                            "not": {}
                          },
                          {
                            "type": "object",
                            "properties": {
                              "default": {},
                              "defaultInput": {
                                "type": "boolean"
                              },
                              "forceInput": {
                                "type": "boolean"
                              },
                              "tooltip": {
                                "type": "string"
                              },
                              "hidden": {
                                "type": "boolean"
                              },
                              "advanced": {
                                "type": "boolean"
                              },
                              "rawLink": {
                                "type": "boolean"
                              },
                              "lazy": {
                                "type": "boolean"
                              },
                              "control_after_generate": {
                                "type": "boolean"
                              },
                              "image_upload": {
                                "type": "boolean"
                              },
                              "image_folder": {
                                "type": "string",
                                "enum": [
                                  "input",
                                  "output",
                                  "temp"
                                ]
                              },
                              "allow_batch": {
                                "type": "boolean"
                              },
                              "video_upload": {
                                "type": "boolean"
                              },
                              "remote": {
                                "type": "object",
                                "properties": {
                                  "route": {
                                    "anyOf": [
                                      {
                                        "type": "string",
                                        "format": "uri"
                                      },
                                      {
                                        "type": "string",
                                        "pattern": "^\\/"
                                      }
                                    ]
                                  },
                                  "refresh": {
                                    "anyOf": [
                                      {
                                        "type": "number",
                                        "minimum": -9007199254740991,
                                        "maximum": 9007199254740991
                                      },
                                      {
                                        "type": "number",
                                        "maximum": 9007199254740991,
                                        "minimum": -9007199254740991
                                      }
                                    ]
                                  },
                                  "response_key": {
                                    "type": "string"
                                  },
                                  "query_params": {
                                    "type": "object",
                                    "additionalProperties": {
                                      "type": "string"
                                    }
                                  },
                                  "refresh_button": {
                                    "type": "boolean"
                                  },
                                  "control_after_refresh": {
                                    "type": "string",
                                    "enum": [
                                      "first",
                                      "last"
                                    ]
                                  },
                                  "timeout": {
                                    "type": "number",
                                    "minimum": 0
                                  },
                                  "max_retries": {
                                    "type": "number",
                                    "minimum": 0
                                  }
                                },
                                "required": [
                                  "route"
                                ],
                                "additionalProperties": false
                              },
                              "options": {
                                "type": "array",
                                "items": {
                                  "type": [
                                    "string",
                                    "number"
                                  ]
                                }
                              }
                            },
                            "additionalProperties": true
                          }
                        ]
                      }
                    ]
                  },
                  {
                    "type": "array",
                    "minItems": 2,
                    "maxItems": 2,
                    "items": [
                      {
                        "type": "string"
                      },
                      {
                        "anyOf": [
                          {
                            "not": {}
                          },
                          {
                            "type": "object",
                            "properties": {
                              "default": {},
                              "defaultInput": {
                                "type": "boolean"
                              },
                              "forceInput": {
                                "type": "boolean"
                              },
                              "tooltip": {
                                "type": "string"
                              },
                              "hidden": {
                                "type": "boolean"
                              },
                              "advanced": {
                                "type": "boolean"
                              },
                              "rawLink": {
                                "type": "boolean"
                              },
                              "lazy": {
                                "type": "boolean"
                              }
                            },
                            "additionalProperties": true
                          }
                        ]
                      }
                    ]
                  }
                ]
              }
            },
            "optional": {
              "type": "object",
              "additionalProperties": {
                "anyOf": [
                  {
                    "type": "array",
                    "minItems": 2,
                    "maxItems": 2,
                    "items": [
                      {
                        "type": "string",
                        "const": "INT"
                      },
                      {
                        "anyOf": [
                          {
                            "not": {}
                          },
                          {
                            "type": "object",
                            "properties": {
                              "default": {
                                "anyOf": [
                                  {
                                    "type": "number"
                                  },
                                  {
                                    "type": "array",
                                    "items": {
                                      "type": "number"
                                    }
                                  }
                                ]
                              },
                              "defaultInput": {
                                "type": "boolean"
                              },
                              "forceInput": {
                                "type": "boolean"
                              },
                              "tooltip": {
                                "type": "string"
                              },
                              "hidden": {
                                "type": "boolean"
                              },
                              "advanced": {
                                "type": "boolean"
                              },
                              "rawLink": {
                                "type": "boolean"
                              },
                              "lazy": {
                                "type": "boolean"
                              },
                              "min": {
                                "type": "number"
                              },
                              "max": {
                                "type": "number"
                              },
                              "step": {
                                "type": "number"
                              },
                              "display": {
                                "type": "string",
                                "enum": [
                                  "slider",
                                  "number",
                                  "knob"
                                ]
                              },
                              "control_after_generate": {
                                "type": "boolean"
                              }
                            },
                            "additionalProperties": true
                          }
                        ]
                      }
                    ]
                  },
                  {
                    "type": "array",
                    "minItems": 2,
                    "maxItems": 2,
                    "items": [
                      {
                        "type": "string",
                        "const": "FLOAT"
                      },
                      {
                        "anyOf": [
                          {
                            "not": {}
                          },
                          {
                            "type": "object",
                            "properties": {
                              "default": {
                                "anyOf": [
                                  {
                                    "type": "number"
                                  },
                                  {
                                    "type": "array",
                                    "items": {
                                      "type": "number"
                                    }
                                  }
                                ]
                              },
                              "defaultInput": {
                                "type": "boolean"
                              },
                              "forceInput": {
                                "type": "boolean"
                              },
                              "tooltip": {
                                "type": "string"
                              },
                              "hidden": {
                                "type": "boolean"
                              },
                              "advanced": {
                                "type": "boolean"
                              },
                              "rawLink": {
                                "type": "boolean"
                              },
                              "lazy": {
                                "type": "boolean"
                              },
                              "min": {
                                "type": "number"
                              },
                              "max": {
                                "type": "number"
                              },
                              "step": {
                                "type": "number"
                              },
                              "display": {
                                "type": "string",
                                "enum": [
                                  "slider",
                                  "number",
                                  "knob"
                                ]
                              },
                              "round": {
                                "anyOf": [
                                  {
                                    "type": "number"
                                  },
                                  {
                                    "type": "boolean",
                                    "const": false
                                  }
                                ]
                              }
                            },
                            "additionalProperties": true
                          }
                        ]
                      }
                    ]
                  },
                  {
                    "type": "array",
                    "minItems": 2,
                    "maxItems": 2,
                    "items": [
                      {
                        "type": "string",
                        "const": "BOOLEAN"
                      },
                      {
                        "anyOf": [
                          {
                            "not": {}
                          },
                          {
                            "type": "object",
                            "properties": {
                              "default": {
                                "type": "boolean"
                              },
                              "defaultInput": {
                                "type": "boolean"
                              },
                              "forceInput": {
                                "type": "boolean"
                              },
                              "tooltip": {
                                "type": "string"
                              },
                              "hidden": {
                                "type": "boolean"
                              },
                              "advanced": {
                                "type": "boolean"
                              },
                              "rawLink": {
                                "type": "boolean"
                              },
                              "lazy": {
                                "type": "boolean"
                              },
                              "label_on": {
                                "type": "string"
                              },
                              "label_off": {
                                "type": "string"
                              }
                            },
                            "additionalProperties": true
                          }
                        ]
                      }
                    ]
                  },
                  {
                    "type": "array",
                    "minItems": 2,
                    "maxItems": 2,
                    "items": [
                      {
                        "type": "string",
                        "const": "STRING"
                      },
                      {
                        "anyOf": [
                          {
                            "not": {}
                          },
                          {
                            "type": "object",
                            "properties": {
                              "default": {
                                "type": "string"
                              },
                              "defaultInput": {
                                "type": "boolean"
                              },
                              "forceInput": {
                                "type": "boolean"
                              },
                              "tooltip": {
                                "type": "string"
                              },
                              "hidden": {
                                "type": "boolean"
                              },
                              "advanced": {
                                "type": "boolean"
                              },
                              "rawLink": {
                                "type": "boolean"
                              },
                              "lazy": {
                                "type": "boolean"
                              },
                              "multiline": {
                                "type": "boolean"
                              },
                              "dynamicPrompts": {
                                "type": "boolean"
                              },
                              "defaultVal": {
                                "type": "string"
                              },
                              "placeholder": {
                                "type": "string"
                              }
                            },
                            "additionalProperties": true
                          }
                        ]
                      }
                    ]
                  },
                  {
                    "type": "array",
                    "minItems": 2,
                    "maxItems": 2,
                    "items": [
                      {
                        "type": "array",
                        "items": {
                          "type": [
                            "string",
                            "number"
                          ]
                        }
                      },
                      {
                        "anyOf": [
                          {
                            "not": {}
                          },
                          {
                            "type": "object",
                            "properties": {
                              "default": {},
                              "defaultInput": {
                                "type": "boolean"
                              },
                              "forceInput": {
                                "type": "boolean"
                              },
                              "tooltip": {
                                "type": "string"
                              },
                              "hidden": {
                                "type": "boolean"
                              },
                              "advanced": {
                                "type": "boolean"
                              },
                              "rawLink": {
                                "type": "boolean"
                              },
                              "lazy": {
                                "type": "boolean"
                              },
                              "control_after_generate": {
                                "type": "boolean"
                              },
                              "image_upload": {
                                "type": "boolean"
                              },
                              "image_folder": {
                                "type": "string",
                                "enum": [
                                  "input",
                                  "output",
                                  "temp"
                                ]
                              },
                              "allow_batch": {
                                "type": "boolean"
                              },
                              "video_upload": {
                                "type": "boolean"
                              },
                              "remote": {
                                "type": "object",
                                "properties": {
                                  "route": {
                                    "anyOf": [
                                      {
                                        "type": "string",
                                        "format": "uri"
                                      },
                                      {
                                        "type": "string",
                                        "pattern": "^\\/"
                                      }
                                    ]
                                  },
                                  "refresh": {
                                    "anyOf": [
                                      {
                                        "type": "number",
                                        "minimum": -9007199254740991,
                                        "maximum": 9007199254740991
                                      },
                                      {
                                        "type": "number",
                                        "maximum": 9007199254740991,
                                        "minimum": -9007199254740991
                                      }
                                    ]
                                  },
                                  "response_key": {
                                    "type": "string"
                                  },
                                  "query_params": {
                                    "type": "object",
                                    "additionalProperties": {
                                      "type": "string"
                                    }
                                  },
                                  "refresh_button": {
                                    "type": "boolean"
                                  },
                                  "control_after_refresh": {
                                    "type": "string",
                                    "enum": [
                                      "first",
                                      "last"
                                    ]
                                  },
                                  "timeout": {
                                    "type": "number",
                                    "minimum": 0
                                  },
                                  "max_retries": {
                                    "type": "number",
                                    "minimum": 0
                                  }
                                },
                                "required": [
                                  "route"
                                ],
                                "additionalProperties": false
                              },
                              "options": {
                                "type": "array",
                                "items": {
                                  "type": [
                                    "string",
                                    "number"
                                  ]
                                }
                              }
                            },
                            "additionalProperties": true
                          }
                        ]
                      }
                    ]
                  },
                  {
                    "type": "array",
                    "minItems": 2,
                    "maxItems": 2,
                    "items": [
                      {
                        "type": "string",
                        "const": "COMBO"
                      },
                      {
                        "anyOf": [
                          {
                            "not": {}
                          },
                          {
                            "type": "object",
                            "properties": {
                              "default": {},
                              "defaultInput": {
                                "type": "boolean"
                              },
                              "forceInput": {
                                "type": "boolean"
                              },
                              "tooltip": {
                                "type": "string"
                              },
                              "hidden": {
                                "type": "boolean"
                              },
                              "advanced": {
                                "type": "boolean"
                              },
                              "rawLink": {
                                "type": "boolean"
                              },
                              "lazy": {
                                "type": "boolean"
                              },
                              "control_after_generate": {
                                "type": "boolean"
                              },
                              "image_upload": {
                                "type": "boolean"
                              },
                              "image_folder": {
                                "type": "string",
                                "enum": [
                                  "input",
                                  "output",
                                  "temp"
                                ]
                              },
                              "allow_batch": {
                                "type": "boolean"
                              },
                              "video_upload": {
                                "type": "boolean"
                              },
                              "remote": {
                                "type": "object",
                                "properties": {
                                  "route": {
                                    "anyOf": [
                                      {
                                        "type": "string",
                                        "format": "uri"
                                      },
                                      {
                                        "type": "string",
                                        "pattern": "^\\/"
                                      }
                                    ]
                                  },
                                  "refresh": {
                                    "anyOf": [
                                      {
                                        "type": "number",
                                        "minimum": -9007199254740991,
                                        "maximum": 9007199254740991
                                      },
                                      {
                                        "type": "number",
                                        "maximum": 9007199254740991,
                                        "minimum": -9007199254740991
                                      }
                                    ]
                                  },
                                  "response_key": {
                                    "type": "string"
                                  },
                                  "query_params": {
                                    "type": "object",
                                    "additionalProperties": {
                                      "type": "string"
                                    }
                                  },
                                  "refresh_button": {
                                    "type": "boolean"
                                  },
                                  "control_after_refresh": {
                                    "type": "string",
                                    "enum": [
                                      "first",
                                      "last"
                                    ]
                                  },
                                  "timeout": {
                                    "type": "number",
                                    "minimum": 0
                                  },
                                  "max_retries": {
                                    "type": "number",
                                    "minimum": 0
                                  }
                                },
                                "required": [
                                  "route"
                                ],
                                "additionalProperties": false
                              },
                              "options": {
                                "type": "array",
                                "items": {
                                  "type": [
                                    "string",
                                    "number"
                                  ]
                                }
                              }
                            },
                            "additionalProperties": true
                          }
                        ]
                      }
                    ]
                  },
                  {
                    "type": "array",
                    "minItems": 2,
                    "maxItems": 2,
                    "items": [
                      {
                        "type": "string"
                      },
                      {
                        "anyOf": [
                          {
                            "not": {}
                          },
                          {
                            "type": "object",
                            "properties": {
                              "default": {},
                              "defaultInput": {
                                "type": "boolean"
                              },
                              "forceInput": {
                                "type": "boolean"
                              },
                              "tooltip": {
                                "type": "string"
                              },
                              "hidden": {
                                "type": "boolean"
                              },
                              "advanced": {
                                "type": "boolean"
                              },
                              "rawLink": {
                                "type": "boolean"
                              },
                              "lazy": {
                                "type": "boolean"
                              }
                            },
                            "additionalProperties": true
                          }
                        ]
                      }
                    ]
                  }
                ]
              }
            },
            "hidden": {
              "type": "object",
              "additionalProperties": {}
            }
          },
          "additionalProperties": false
        },
        "output": {
          "type": "array",
          "items": {
            "anyOf": [
              {
                "type": "string"
              },
              {
                "type": "array",
                "items": {
                  "type": [
                    "string",
                    "number"
                  ]
                }
              }
            ]
          }
        },
        "output_is_list": {
          "type": "array",
          "items": {
            "type": "boolean"
          }
        },
        "output_name": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "output_tooltips": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "name": {
          "type": "string"
        },
        "display_name": {
          "type": "string"
        },
        "description": {
          "type": "string"
        },
        "category": {
          "type": "string"
        },
        "output_node": {
          "type": "boolean"
        },
        "python_module": {
          "type": "string"
        },
        "deprecated": {
          "type": "boolean"
        },
        "experimental": {
          "type": "boolean"
        }
      },
      "required": [
        "name",
        "display_name",
        "description",
        "category",
        "output_node",
        "python_module"
      ],
      "additionalProperties": false
    }
  },
  "$schema": "http://json-schema.org/draft-07/schema#"
}
```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/specs/nodedef_json_1_0.mdx)

[Previous  
\
Node Definition JSONJSON schema for a ComfyUI Node.](http://docs.comfy.org/specs/nodedef_json)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [v1.0](http://docs.comfy.org#v1-0)