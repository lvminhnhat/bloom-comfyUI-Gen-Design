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
  
  - [Javascript Extensions](http://docs.comfy.org/custom-nodes/js/javascript_overview)
  - [Comfy Hooks](http://docs.comfy.org/custom-nodes/js/javascript_hooks)
  - [Comfy Objects](http://docs.comfy.org/custom-nodes/js/javascript_objects_and_hijacking)
  - [Settings](http://docs.comfy.org/custom-nodes/js/javascript_settings)
  - [Annotated Examples](http://docs.comfy.org/custom-nodes/js/javascript_examples)
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

Comfy Hooks

# Comfy Hooks

## [​](http://docs.comfy.org#extension-hooks) Extension hooks

At various points during Comfy execution, the application calls `#invokeExtensionsAsync` or `#invokeExtensions` with the name of a hook. These invoke, on all registered extensions, the appropriately named method (if present), such as `setup` in the example above.

Comfy provides a variety of hooks for custom extension code to use to modify client behavior.

These hooks are called during creation and modification of the Comfy client side elements.  
Events during workflow execution are handled by the `apiUpdateHandlers`

A few of the most significant hooks are described below. As Comfy is being actively developed, from time to time additional hooks are added, so search for `#invokeExtensions` in `app.js` to find all available hooks.

See also the [sequence](http://docs.comfy.org/_sites/docs.comfy.org/custom-nodes/js/javascript_hooks#call-sequences) in which hooks are invoked.

### [​](http://docs.comfy.org#commonly-used-hooks) Commonly used hooks

Start with `beforeRegisterNodeDef`, which is used by the majority of extensions, and is often the only one needed.

#### [​](http://docs.comfy.org#beforeregisternodedef) beforeRegisterNodeDef()

Called once for each node type (the list of nodes available in the `AddNode` menu), and is used to modify the bahaviour of the node.

```javascript
async beforeRegisterNodeDef(nodeType, nodeData, app) 
```

The object passed in the `nodeType` parameter essentially serves as a template for all nodes that will be created of this type, so modifications made to `nodeType.prototype` will apply to all nodes of this type. `nodeData` is an encapsulation of aspects of the node defined in the Python code, such as its category, inputs, and outputs. `app` is a reference to the main Comfy app object (which you have already imported anyway!)

This method is called, on each registered extension, for *every* node type, not just the ones added by that extension.

The usual idiom is to check `nodeType.ComfyClass`, which holds the Python class name corresponding to this node, to see if you need to modify the node. Often this means modifying the custom nodes that you have added, although you may sometimes need to modify the behavior of other nodes (or other custom nodes might modify yours!), in which case care should be taken to ensure interoperability.

Since other extensions may also modify nodes, aim to write code that makes as few assumptions as possible. And play nicely - isolate your changes wherever possible.

A very common idiom in `beforeRegisterNodeDef` is to ‘hijack’ an existing method:

```javascript
async beforeRegisterNodeDef(nodeType, nodeData, app) {
	if (nodeType.comfyClass=="MyNodeClass") { 
		const onConnectionsChange = nodeType.prototype.onConnectionsChange;
		nodeType.prototype.onConnectionsChange = function (side,slot,connect,link_info,output) {     
			const r = onConnectionsChange?.apply(this, arguments);   
			console.log("Someone changed my connection!");
			return r;
		}
	}
}
```

In this idiom the existing prototype method is stored, and then replaced. The replacement calls the original method (the `?.apply` ensures that if there wasn’t one this is still safe) and then performs additional operations. Depending on your code logic, you may need to place the `apply` elsewhere in your replacement code, or even make calling it conditional.

When hijacking a method in this way, you will want to look at the core comfy code (breakpoints are your friend) to check and conform with the method signature.

#### [​](http://docs.comfy.org#nodecreated) nodeCreated()

```javascript
async nodeCreated(node)
```

Called when a specific instance of a node gets created (right at the end of the `ComfyNode()` function on `nodeType` which serves as a constructor). In this hook you can make modifications to individual instances of your node.

Changes that apply to all instances are better added to the prototype in `beforeRegisterNodeDef` as described above.

#### [​](http://docs.comfy.org#init) init()

```javascript
async init()
```

Called when the Comfy webpage is loaded (or reloaded). The call is made after the graph object has been created, but before any nodes are registered or created. It can be used to modify core Comfy behavior by hijacking methods of the app, or of the graph (a `LiteGraph` object). This is discussed further in [Comfy Objects](http://docs.comfy.org/javascript_objects_and_hijacking).

With great power comes great responsibility. Hijacking core behavior makes it more likely your nodes will be incompatible with other custom nodes, or future Comfy updates

#### [​](http://docs.comfy.org#setup) setup()

```javascript
async setup()
```

Called at the end of the startup process. A good place to add event listeners (either for Comfy events, or DOM events), or adding to the global menus, both of which are discussed elsewhere.

To do something when a workflow has loaded, use `afterConfigureGraph`, not `setup`

### [​](http://docs.comfy.org#call-sequences) Call sequences

These sequences were obtained by insert logging code into the Comfy `app.js` file. You may find similar code helpful in understanding the execution flow.

```javascript
/* approx line 220 at time of writing: */
	#invokeExtensions(method, ...args) {
		console.log(`invokeExtensions      ${method}`) // this line added
		// ...
	}
/* approx line 250 at time of writing: */
	async #invokeExtensionsAsync(method, ...args) {
		console.log(`invokeExtensionsAsync ${method}`) // this line added
		// ...
	}
```

#### [​](http://docs.comfy.org#web-page-load) Web page load

```plaintext
invokeExtensionsAsync init
invokeExtensionsAsync addCustomNodeDefs
invokeExtensionsAsync getCustomWidgets
invokeExtensionsAsync beforeRegisterNodeDef    [repeated multiple times]
invokeExtensionsAsync registerCustomNodes
invokeExtensionsAsync beforeConfigureGraph
invokeExtensionsAsync nodeCreated
invokeExtensions      loadedGraphNode
invokeExtensionsAsync afterConfigureGraph
invokeExtensionsAsync setup
```

#### [​](http://docs.comfy.org#loading-workflow) Loading workflow

```plaintext
invokeExtensionsAsync beforeConfigureGraph
invokeExtensionsAsync beforeRegisterNodeDef   [zero, one, or multiple times]
invokeExtensionsAsync nodeCreated             [repeated multiple times]
invokeExtensions      loadedGraphNode         [repeated multiple times]
invokeExtensionsAsync afterConfigureGraph
```

#### [​](http://docs.comfy.org#adding-new-node) Adding new node

```plaintext
invokeExtensionsAsync nodeCreated
```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/custom-nodes/js/javascript_hooks.mdx)

[Previous](http://docs.comfy.org/custom-nodes/js/javascript_overview)

[Comfy Objects  
\
Next](http://docs.comfy.org/custom-nodes/js/javascript_objects_and_hijacking)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Extension hooks](http://docs.comfy.org#extension-hooks)
- [Commonly used hooks](http://docs.comfy.org#commonly-used-hooks)
- [beforeRegisterNodeDef()](http://docs.comfy.org#beforeregisternodedef)
- [nodeCreated()](http://docs.comfy.org#nodecreated)
- [init()](http://docs.comfy.org#init)
- [setup()](http://docs.comfy.org#setup)
- [Call sequences](http://docs.comfy.org#call-sequences)
- [Web page load](http://docs.comfy.org#web-page-load)
- [Loading workflow](http://docs.comfy.org#loading-workflow)
- [Adding new node](http://docs.comfy.org#adding-new-node)