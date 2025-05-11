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
  
  - [Workflow JSON](http://docs.comfy.org/specs/workflow_json)
  - [Workflow JSON 0.4](http://docs.comfy.org/specs/workflow_json_0.4)
- Node Definitions

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

Workflow JSON 0.4

# Workflow JSON 0.4

JSON schema for a ComfyUI workflow.

## [​](http://docs.comfy.org#v0-4) v0.4

```json
{
  "$ref": "#/definitions/ComfyWorkflow0_4",
  "definitions": {
    "ComfyWorkflow0_4": {
      "type": "object",
      "properties": {
        "last_node_id": {
          "anyOf": [
            {
              "type": "integer"
            },
            {
              "type": "string"
            }
          ]
        },
        "last_link_id": {
          "type": "number"
        },
        "nodes": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "id": {
                "anyOf": [
                  {
                    "type": "integer"
                  },
                  {
                    "type": "string"
                  }
                ]
              },
              "type": {
                "type": "string"
              },
              "pos": {
                "anyOf": [
                  {
                    "type": "object",
                    "properties": {
                      "0": {
                        "type": "number"
                      },
                      "1": {
                        "type": "number"
                      }
                    },
                    "required": [
                      "0",
                      "1"
                    ],
                    "additionalProperties": true
                  },
                  {
                    "type": "array",
                    "minItems": 2,
                    "maxItems": 2,
                    "items": [
                      {
                        "type": "number"
                      },
                      {
                        "type": "number"
                      }
                    ]
                  }
                ]
              },
              "size": {
                "anyOf": [
                  {
                    "type": "object",
                    "properties": {
                      "0": {
                        "type": "number"
                      },
                      "1": {
                        "type": "number"
                      }
                    },
                    "required": [
                      "0",
                      "1"
                    ],
                    "additionalProperties": true
                  },
                  {
                    "type": "array",
                    "minItems": 2,
                    "maxItems": 2,
                    "items": [
                      {
                        "type": "number"
                      },
                      {
                        "type": "number"
                      }
                    ]
                  }
                ]
              },
              "flags": {
                "type": "object",
                "properties": {
                  "collapsed": {
                    "type": "boolean"
                  },
                  "pinned": {
                    "type": "boolean"
                  },
                  "allow_interaction": {
                    "type": "boolean"
                  },
                  "horizontal": {
                    "type": "boolean"
                  },
                  "skip_repeated_outputs": {
                    "type": "boolean"
                  }
                },
                "additionalProperties": true
              },
              "order": {
                "type": "number"
              },
              "mode": {
                "type": "number"
              },
              "inputs": {
                "type": "array",
                "items": {
                  "type": "object",
                  "properties": {
                    "name": {
                      "type": "string"
                    },
                    "type": {
                      "anyOf": [
                        {
                          "type": "string"
                        },
                        {
                          "type": "array",
                          "items": {
                            "type": "string"
                          }
                        },
                        {
                          "type": "number"
                        }
                      ]
                    },
                    "link": {
                      "type": [
                        "number",
                        "null"
                      ]
                    },
                    "slot_index": {
                      "anyOf": [
                        {
                          "type": "integer"
                        },
                        {
                          "type": "string"
                        }
                      ]
                    }
                  },
                  "required": [
                    "name",
                    "type"
                  ],
                  "additionalProperties": true
                }
              },
              "outputs": {
                "type": "array",
                "items": {
                  "type": "object",
                  "properties": {
                    "name": {
                      "type": "string"
                    },
                    "type": {
                      "anyOf": [
                        {
                          "type": "string"
                        },
                        {
                          "type": "array",
                          "items": {
                            "type": "string"
                          }
                        },
                        {
                          "type": "number"
                        }
                      ]
                    },
                    "links": {
                      "anyOf": [
                        {
                          "type": "array",
                          "items": {
                            "type": "number"
                          }
                        },
                        {
                          "type": "null"
                        }
                      ]
                    },
                    "slot_index": {
                      "anyOf": [
                        {
                          "type": "integer"
                        },
                        {
                          "type": "string"
                        }
                      ]
                    }
                  },
                  "required": [
                    "name",
                    "type"
                  ],
                  "additionalProperties": true
                }
              },
              "properties": {
                "type": "object",
                "properties": {
                  "Node name for S&R": {
                    "type": "string"
                  }
                },
                "additionalProperties": true
              },
              "widgets_values": {
                "anyOf": [
                  {
                    "type": "array"
                  },
                  {
                    "type": "object",
                    "additionalProperties": {}
                  }
                ]
              },
              "color": {
                "type": "string"
              },
              "bgcolor": {
                "type": "string"
              }
            },
            "required": [
              "id",
              "type",
              "pos",
              "size",
              "flags",
              "order",
              "mode",
              "properties"
            ],
            "additionalProperties": true
          }
        },
        "links": {
          "type": "array",
          "items": {
            "type": "array",
            "minItems": 6,
            "maxItems": 6,
            "items": [
              {
                "type": "number"
              },
              {
                "anyOf": [
                  {
                    "type": "integer"
                  },
                  {
                    "type": "string"
                  }
                ]
              },
              {
                "anyOf": [
                  {
                    "type": "integer"
                  },
                  {
                    "type": "string"
                  }
                ]
              },
              {
                "anyOf": [
                  {
                    "type": "integer"
                  },
                  {
                    "type": "string"
                  }
                ]
              },
              {
                "anyOf": [
                  {
                    "type": "integer"
                  },
                  {
                    "type": "string"
                  }
                ]
              },
              {
                "anyOf": [
                  {
                    "type": "string"
                  },
                  {
                    "type": "array",
                    "items": {
                      "type": "string"
                    }
                  },
                  {
                    "type": "number"
                  }
                ]
              }
            ]
          }
        },
        "groups": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "title": {
                "type": "string"
              },
              "bounding": {
                "type": "array",
                "minItems": 4,
                "maxItems": 4,
                "items": [
                  {
                    "type": "number"
                  },
                  {
                    "type": "number"
                  },
                  {
                    "type": "number"
                  },
                  {
                    "type": "number"
                  }
                ]
              },
              "color": {
                "type": "string"
              },
              "font_size": {
                "type": "number"
              },
              "locked": {
                "type": "boolean"
              }
            },
            "required": [
              "title",
              "bounding"
            ],
            "additionalProperties": true
          }
        },
        "config": {
          "anyOf": [
            {
              "anyOf": [
                {
                  "not": {}
                },
                {
                  "type": "object",
                  "properties": {
                    "links_ontop": {
                      "type": "boolean"
                    },
                    "align_to_grid": {
                      "type": "boolean"
                    }
                  },
                  "additionalProperties": true
                }
              ]
            },
            {
              "type": "null"
            }
          ]
        },
        "extra": {
          "anyOf": [
            {
              "anyOf": [
                {
                  "not": {}
                },
                {
                  "type": "object",
                  "properties": {
                    "ds": {
                      "type": "object",
                      "properties": {
                        "scale": {
                          "type": "number"
                        },
                        "offset": {
                          "anyOf": [
                            {
                              "type": "object",
                              "properties": {
                                "0": {
                                  "type": "number"
                                },
                                "1": {
                                  "type": "number"
                                }
                              },
                              "required": [
                                "0",
                                "1"
                              ],
                              "additionalProperties": true
                            },
                            {
                              "type": "array",
                              "minItems": 2,
                              "maxItems": 2,
                              "items": [
                                {
                                  "type": "number"
                                },
                                {
                                  "type": "number"
                                }
                              ]
                            }
                          ]
                        }
                      },
                      "required": [
                        "scale",
                        "offset"
                      ],
                      "additionalProperties": true
                    },
                    "info": {
                      "type": "object",
                      "properties": {
                        "name": {
                          "type": "string"
                        },
                        "author": {
                          "type": "string"
                        },
                        "description": {
                          "type": "string"
                        },
                        "version": {
                          "type": "string"
                        },
                        "created": {
                          "type": "string"
                        },
                        "modified": {
                          "type": "string"
                        },
                        "software": {
                          "type": "string"
                        }
                      },
                      "required": [
                        "name",
                        "author",
                        "description",
                        "version",
                        "created",
                        "modified",
                        "software"
                      ],
                      "additionalProperties": true
                    },
                    "linkExtensions": {
                      "type": "array",
                      "items": {
                        "type": "object",
                        "properties": {
                          "id": {
                            "type": "number"
                          },
                          "parentId": {
                            "type": "number"
                          }
                        },
                        "required": [
                          "id",
                          "parentId"
                        ],
                        "additionalProperties": true
                      }
                    },
                    "reroutes": {
                      "type": "array",
                      "items": {
                        "type": "object",
                        "properties": {
                          "id": {
                            "type": "number"
                          },
                          "parentId": {
                            "type": "number"
                          },
                          "pos": {
                            "anyOf": [
                              {
                                "type": "object",
                                "properties": {
                                  "0": {
                                    "type": "number"
                                  },
                                  "1": {
                                    "type": "number"
                                  }
                                },
                                "required": [
                                  "0",
                                  "1"
                                ],
                                "additionalProperties": true
                              },
                              {
                                "type": "array",
                                "minItems": 2,
                                "maxItems": 2,
                                "items": [
                                  {
                                    "type": "number"
                                  },
                                  {
                                    "type": "number"
                                  }
                                ]
                              }
                            ]
                          },
                          "linkIds": {
                            "anyOf": [
                              {
                                "type": "array",
                                "items": {
                                  "type": "number"
                                }
                              },
                              {
                                "type": "null"
                              }
                            ]
                          }
                        },
                        "required": [
                          "id",
                          "pos"
                        ],
                        "additionalProperties": true
                      }
                    }
                  },
                  "additionalProperties": true
                }
              ]
            },
            {
              "type": "null"
            }
          ]
        },
        "version": {
          "type": "number"
        },
        "models": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "name": {
                "type": "string"
              },
              "url": {
                "type": "string",
                "format": "uri"
              },
              "hash": {
                "type": "string"
              },
              "hash_type": {
                "type": "string"
              },
              "directory": {
                "type": "string"
              }
            },
            "required": [
              "name",
              "url",
              "directory"
            ],
            "additionalProperties": false
          }
        }
      },
      "required": [
        "last_node_id",
        "last_link_id",
        "nodes",
        "links",
        "version"
      ],
      "additionalProperties": true
    }
  },
  "$schema": "http://json-schema.org/draft-07/schema#"
}
```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/specs/workflow_json_0.4.mdx)

[Previous](http://docs.comfy.org/specs/workflow_json)

[Node Definition JSONJSON schema for a ComfyUI Node.  
\
Next](http://docs.comfy.org/specs/nodedef_json)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [v0.4](http://docs.comfy.org#v0-4)