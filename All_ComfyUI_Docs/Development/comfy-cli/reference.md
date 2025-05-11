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

Reference

# Reference

# [​](http://docs.comfy.org#cli) CLI

## [​](http://docs.comfy.org#nodes) Nodes

**Usage**:

```plaintext
$ comfy node [OPTIONS] COMMAND [ARGS]...
```

**Options**:

- `--install-completion`: Install completion for the current shell.
- `--show-completion`: Show completion for the current shell, to copy it or customize the installation.
- `--help`: Show this message and exit.

**Commands**:

- `deps-in-workflow`
- `disable`
- `enable`
- `fix`
- `install`
- `install-deps`
- `reinstall`
- `restore-dependencies`
- `restore-snapshot`
- `save-snapshot`: Save a snapshot of the current ComfyUI…
- `show`
- `simple-show`
- `uninstall`
- `update`

### [​](http://docs.comfy.org#deps-in-workflow) `deps-in-workflow`

**Usage**:

```plaintext
$ deps-in-workflow [OPTIONS]
```

**Options**:

- `--workflow TEXT`: Workflow file (.json/.png) \[required]
- `--output TEXT`: Workflow file (.json/.png) \[required]
- `--channel TEXT`: Specify the operation mode
- `--mode TEXT`: \[remote|local|cache]
- `--help`: Show this message and exit.

### [​](http://docs.comfy.org#disable) `disable`

**Usage**:

```plaintext
$ disable [OPTIONS] ARGS...
```

**Arguments**:

- `ARGS...`: disable custom nodes \[required]

**Options**:

- `--channel TEXT`: Specify the operation mode
- `--mode TEXT`: \[remote|local|cache]
- `--help`: Show this message and exit.

### [​](http://docs.comfy.org#enable) `enable`

**Usage**:

```plaintext
$ enable [OPTIONS] ARGS...
```

**Arguments**:

- `ARGS...`: enable custom nodes \[required]

**Options**:

- `--channel TEXT`: Specify the operation mode
- `--mode TEXT`: \[remote|local|cache]
- `--help`: Show this message and exit.

### [​](http://docs.comfy.org#fix) `fix`

**Usage**:

```plaintext
$ fix [OPTIONS] ARGS...
```

**Arguments**:

- `ARGS...`: fix dependencies for specified custom nodes \[required]

**Options**:

- `--channel TEXT`: Specify the operation mode
- `--mode TEXT`: \[remote|local|cache]
- `--help`: Show this message and exit.

### [​](http://docs.comfy.org#install) `install`

**Usage**:

```plaintext
$ install [OPTIONS] ARGS...
```

**Arguments**:

- `ARGS...`: install custom nodes \[required]

**Options**:

- `--channel TEXT`: Specify the operation mode
- `--mode TEXT`: \[remote|local|cache]
- `--help`: Show this message and exit.

### [​](http://docs.comfy.org#install-deps) `install-deps`

**Usage**:

```plaintext
$ install-deps [OPTIONS]
```

**Options**:

- `--deps TEXT`: Dependency spec file (.json)
- `--workflow TEXT`: Workflow file (.json/.png)
- `--channel TEXT`: Specify the operation mode
- `--mode TEXT`: \[remote|local|cache]
- `--help`: Show this message and exit.

### [​](http://docs.comfy.org#reinstall) `reinstall`

**Usage**:

```plaintext
$ reinstall [OPTIONS] ARGS...
```

**Arguments**:

- `ARGS...`: reinstall custom nodes \[required]

**Options**:

- `--channel TEXT`: Specify the operation mode
- `--mode TEXT`: \[remote|local|cache]
- `--help`: Show this message and exit.

### [​](http://docs.comfy.org#restore-dependencies) `restore-dependencies`

**Usage**:

```plaintext
$ restore-dependencies [OPTIONS]
```

**Options**:

- `--help`: Show this message and exit.

### [​](http://docs.comfy.org#restore-snapshot) `restore-snapshot`

**Usage**:

```plaintext
$ restore-snapshot [OPTIONS] PATH
```

**Arguments**:

- `PATH`: \[required]

**Options**:

- `--help`: Show this message and exit.

### [​](http://docs.comfy.org#save-snapshot) `save-snapshot`

Save a snapshot of the current ComfyUI environment

**Usage**:

```plaintext
$ save-snapshot [OPTIONS]
```

**Options**:

- `--output TEXT`: Specify the output file path. (.json/.yaml)
- `--help`: Show this message and exit.

### [​](http://docs.comfy.org#show) `show`

**Usage**:

```plaintext
$ show [OPTIONS] ARGS...
```

**Arguments**:

- `ARGS...`: \[installed|enabled|not-installed|disabled|all|snapshot|snapshot-list] \[required]

**Options**:

- `--channel TEXT`: Specify the operation mode
- `--mode TEXT`: \[remote|local|cache]
- `--help`: Show this message and exit.

### [​](http://docs.comfy.org#simple-show) `simple-show`

**Usage**:

```plaintext
$ simple-show [OPTIONS] ARGS...
```

**Arguments**:

- `ARGS...`: \[installed|enabled|not-installed|disabled|all|snapshot|snapshot-list] \[required]

**Options**:

- `--channel TEXT`: Specify the operation mode
- `--mode TEXT`: \[remote|local|cache]
- `--help`: Show this message and exit.

### [​](http://docs.comfy.org#uninstall) `uninstall`

**Usage**:

```plaintext
$ uninstall [OPTIONS] ARGS...
```

**Arguments**:

- `ARGS...`: uninstall custom nodes \[required]

**Options**:

- `--channel TEXT`: Specify the operation mode
- `--mode TEXT`: \[remote|local|cache]
- `--help`: Show this message and exit.

### [​](http://docs.comfy.org#update) `update`

**Usage**:

```plaintext
$ update [OPTIONS] ARGS...
```

**Arguments**:

- `ARGS...`: update custom nodes \[required]

**Options**:

- `--channel TEXT`: Specify the operation mode
- `--mode TEXT`: \[remote|local|cache]
- `--help`: Show this message and exit.

## [​](http://docs.comfy.org#models) Models

**Usage**:

```plaintext
$ comfy model [OPTIONS] COMMAND [ARGS]...
```

**Options**:

- `--install-completion`: Install completion for the current shell.
- `--show-completion`: Show completion for the current shell, to copy it or customize the installation.
- `--help`: Show this message and exit.

**Commands**:

- `download`: Download a model to a specified relative…
- `list`: Display a list of all models currently…
- `remove`: Remove one or more downloaded models,…

### [​](http://docs.comfy.org#download) `download`

Download a model to a specified relative path if it is not already downloaded.

**Usage**:

```plaintext
$ download [OPTIONS]
```

**Options**:

- `--url TEXT`: The URL from which to download the model \[required]
- `--relative-path TEXT`: The relative path from the current workspace to install the model. \[default: models/checkpoints]
- `--help`: Show this message and exit.

### [​](http://docs.comfy.org#list) `list`

Display a list of all models currently downloaded in a table format.

**Usage**:

```plaintext
$ list [OPTIONS]
```

**Options**:

- `--relative-path TEXT`: The relative path from the current workspace where the models are stored. \[default: models/checkpoints]
- `--help`: Show this message and exit.

### [​](http://docs.comfy.org#remove) `remove`

Remove one or more downloaded models, either by specifying them directly or through an interactive selection.

**Usage**:

```plaintext
$ remove [OPTIONS]
```

**Options**:

- `--relative-path TEXT`: The relative path from the current workspace where the models are stored. \[default: models/checkpoints]
- `--model-names TEXT`: List of model filenames to delete, separated by spaces
- `--help`: Show this message and exit.

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/comfy-cli/reference.mdx)

[Previous](http://docs.comfy.org/comfy-cli/getting-started)

[Overview  
\
Next](http://docs.comfy.org/custom-nodes/overview)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [CLI](http://docs.comfy.org#cli)
- [Nodes](http://docs.comfy.org#nodes)
- [deps-in-workflow](http://docs.comfy.org#deps-in-workflow)
- [disable](http://docs.comfy.org#disable)
- [enable](http://docs.comfy.org#enable)
- [fix](http://docs.comfy.org#fix)
- [install](http://docs.comfy.org#install)
- [install-deps](http://docs.comfy.org#install-deps)
- [reinstall](http://docs.comfy.org#reinstall)
- [restore-dependencies](http://docs.comfy.org#restore-dependencies)
- [restore-snapshot](http://docs.comfy.org#restore-snapshot)
- [save-snapshot](http://docs.comfy.org#save-snapshot)
- [show](http://docs.comfy.org#show)
- [simple-show](http://docs.comfy.org#simple-show)
- [uninstall](http://docs.comfy.org#uninstall)
- [update](http://docs.comfy.org#update)
- [Models](http://docs.comfy.org#models)
- [download](http://docs.comfy.org#download)
- [list](http://docs.comfy.org#list)
- [remove](http://docs.comfy.org#remove)