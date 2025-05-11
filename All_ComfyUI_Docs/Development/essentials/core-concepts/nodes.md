[ComfyUI home page![logo](https://mintlify.s3.us-west-1.amazonaws.com/dripart/logo.png)](http://docs.comfy.org/)

Search or ask...

Get Started

##### Get Started

- [Introduction](http://docs.comfy.org/get_started/introduction)
- Installation
- [First Image Generation](http://docs.comfy.org/get_started/first_generation)

##### Interface

- [Interface Overview](http://docs.comfy.org/interface/overview)
- [Account Management](http://docs.comfy.org/interface/user)
- [Credits Management](http://docs.comfy.org/interface/credits)
- [Workflow](http://docs.comfy.org/essentials/core-concepts/workflow)
- [Nodes](http://docs.comfy.org/essentials/core-concepts/nodes)
- [Properties](http://docs.comfy.org/essentials/core-concepts/properties)
- [Links](http://docs.comfy.org/essentials/core-concepts/links)
- [Mask Editor](http://docs.comfy.org/interface/maskeditor)
- [Models](http://docs.comfy.org/essentials/core-concepts/models)
- [Dependencies](http://docs.comfy.org/essentials/core-concepts/dependencies)
- [Shortcuts](http://docs.comfy.org/interface/shortcuts)

##### Tutorials

- Basic Examples
- ControlNet
- Flux
- Image
- 3D
- Video
- Audio
- API Nodes

##### Community

- [Contributing](http://docs.comfy.org/community/contributing)

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

Nodes

# Nodes

Understand the concept of a node in ComfyUI.

In ComfyUI, nodes are the fundamental building blocks for executing tasks. Each node is an independently built module, whether it’s a **Comfy Core** node or a **Custom Node**, with its own unique functionality. Nodes connect to each other through links, allowing us to build complex functionality like assembling LEGO blocks. The combinations of different nodes create the unlimited possibilities of ComfyUI.

For example, in the K-Sampler node, you can see it has multiple inputs and outputs, and also includes multiple parameter settings. These parameters determine the logic of node execution. Behind each node is well-written Python logic, allowing you to achieve corresponding functionality without having to write code yourself.

As ComfyUI is still in rapid iteration and development, we are continuously improving it every day. Therefore, some operations mentioned in this article may change or be omitted. Please refer to the actual interface. If you find changes in actual operations, it may be due to our iterative updates. You can also fork [this repo](https://github.com/Comfy-Org/docs) and help us improve this documentation.

## [​](http://docs.comfy.org#nodes-perform-operations) Nodes perform operations

In computer science, a ***node*** is a container for information, usually including programmed instructions to perform some task. Nodes almost never exist in isolation, they’re almost always connected to other nodes in a networked graph. In ComfyUI, nodes take the visual form of boxes that are connected to each other.

ComfyUI nodes are usually ***function operators***. This means that they operate on some data to perform a function. A function is a process that accepts input data, performs some operation on it, and produces output data. In other words, nodes do some work, contributing to the completion of a task such as generating an image. So ComfyUI nodes almost always have at least one input or output, and usually have multiple inputs and outputs.

## [​](http://docs.comfy.org#different-node-states) Different Node States

In ComfyUI, nodes have multiple states. Here are some common node states:

1. **Normal State**: The default state
2. **Running State**: The running state, typically displayed when a node is executing after you start running the workflow
3. **Error State**: Node error, typically displayed after running the workflow if there’s a problem with the node’s input, indicated by red marking of the erroneous input node. You need to fix the problematic input to ensure the workflow runs correctly
4. **Missing State**: This state usually appears after importing workflows, with two possibilities:
   
   - Comfy Core native node missing: This usually happens because ComfyUI has been updated, but you’re using an older version of ComfyUI. You need to update ComfyUI to resolve this issue
   - Custom node missing: The workflow uses custom nodes developed by third-party authors, but your local ComfyUI version doesn’t have these custom nodes installed. You can use [ComfyUI-Manager](https://github.com/Comfy-Org/ComfyUI-Manager) to find and install the missing custom nodes

## [​](http://docs.comfy.org#connections-between-nodes) Connections Between Nodes

In ComfyUI, nodes are connected through [links](http://docs.comfy.org/essentials/core-concepts/links), allowing data of the same type to flow between different processing units to achieve the final result.

Each node receives some input, processes it through its module, and converts it to corresponding output. Connections between different nodes must conform to the data type requirements. In ComfyUI, we use different colors to distinguish node data types. Below are some basic data types:

Data typeColordiffusion modellavenderCLIP modelyellowVAE modelroseconditioningorangelatent imagepinkpixel imagebluemaskgreennumber (integer or float)light greenmeshbright green

As ComfyUI evolves, we may expand to more data types to meet the needs of more scenarios.

### [​](http://docs.comfy.org#connecting-and-disconnecting-nodes) Connecting and Disconnecting Nodes

**Connecting**: Drag from the output point of one node to the input of the same color on another node to connect them **Disconnecting**: Click on the input endpoint and drag the mouse left button to disconnect, or cancel the connection through the midpoint menu of the link

## [​](http://docs.comfy.org#node-appearance) Node Appearance

We provide various style settings for you to customize the appearance of nodes:

- Modify styles
- Double-click the node title to modify the node name
- Switch node inputs between input sockets and widgets through the context menu
- Resize the node using the bottom right corner

### [​](http://docs.comfy.org#node-badges) Node Badges

We provide multiple node badge display features, such as:

- Node ID
- Node source

Currently, **Comfy Core nodes** use a fox icon for display, while custom nodes use their names. This way you can quickly understand which node package a node comes from.

You can set the corresponding display in the menu:

## [​](http://docs.comfy.org#node-context-menus) Node Context Menus

Node context menus are mainly divided into two types:

- Context menu for the node itself
- Context menu for inputs/outputs

### [​](http://docs.comfy.org#node-context-menu) Node Context Menu

By right-clicking on a node, you can expand the corresponding node context menu:

In the node’s right-click context menu, you can:

- Adjust the node’s color style
- Modify the title
- Clone, copy, or delete the node
- Set the node’s mode

In this menu, besides appearance-related settings, the following menu operations are important:

- **Mode**: Set the node’s mode: Always, Never, Bypass
- **Toggle between Widget and Input mode for node inputs**: Switch between widget and input mode for node inputs

#### [​](http://docs.comfy.org#mode) Mode

For modes, you may notice that we currently provide: Always, Never, On Event, On Trigger - four modes, but actually only **Always** and **Never** are effective. **On Event** and **On Trigger** are currently ineffective as we haven’t fully implemented this feature. Additionally, you can understand **Bypass** as a mode. Below is an explanation of the available modes:

- **Always**: The default node mode. The node will execute whenever it runs for the first time or when any of its inputs change since the last execution
- **Never**: The node will never execute under any circumstances, as if it’s been deleted. Subsequent nodes cannot read or receive any data from it
- **Bypass**: The node will never execute under any circumstances, but subsequent nodes can still try to obtain data that hasn’t been processed by this node

Below is a comparison of the `Never` and `Bypass` modes:

In this comparison example, you can see that both workflows apply two LoRA models simultaneously, with the difference being that one `Load LoRA` node is set to `Never` mode while the other is set to `Bypass` mode.

- The node set to `Never` mode causes subsequent nodes to show errors because they don’t receive any input data
- The node set to `Bypass` mode still allows subsequent nodes to receive unprocessed data, so they load the output data from the first `Load LoRA` node, allowing the subsequent workflow to continue running normally

#### [​](http://docs.comfy.org#switching-between-widget-and-input-mode-for-node-inputs) Switching Between Widget and Input Mode for Node Inputs

In some cases, we need to use output results from other nodes as input. In this case, we can switch between widget and input mode for node inputs.

Here’s a very simple example:

By switching the K-Sampler’s Seed from widget to input mode, multiple nodes can share the same seed, achieving variable uniformity across multiple samplers. Comparing the first node with the subsequent two nodes, you can see that the seed in the latter two nodes is in input mode. You can also convert it back to widget mode:

After frontend version v1.16.0, we improved this feature. Now you only need to directly connect the input line to the corresponding widget to complete this process

> Say goodbye to annoying widget &lt;&gt; socket conversion starting from frontend version v1.16.0! Now each widget just always have an associated input socket by default [#ComfyUI](https://twitter.com/hashtag/ComfyUI?src=hash&ref_src=twsrc%5Etfw) [pic.twitter.com/sP9HHKyGYW](https://t.co/sP9HHKyGYW)
> 
> — Chenlei Hu (@HclHno3) [April 7, 2025](https://twitter.com/HclHno3/status/1909059259536375961?ref_src=twsrc%5Etfw)

### [​](http://docs.comfy.org#input%2Foutput-context-menu) Input/Output Context Menu

This context menu is mainly related to the data type of the corresponding input/output:

When dragging the input/output of a node, if a connection appears but you haven’t connected to another node’s input or output, releasing the mouse will pop up a context menu for the input/output, used to quickly add related types of nodes. You can adjust the number of node suggestions in the settings:

## [​](http://docs.comfy.org#node-selection-toolbox) Node Selection Toolbox

The **Node Selection Toolbox** is a floating tool that provides quick operations for nodes. When you select a node, it hovers above the selected node. Through this toolbox, you can:

- Change the node’s color
- Quickly set the node to Bypass mode (not execute during runtime)
- Lock the node
- Delete the node

Of course, these functions can also be found in the right-click menu of the corresponding node. The node selection toolbox just provides a shortcut operation. If you want to disable this feature, you can turn it off in the settings.

## [​](http://docs.comfy.org#node-groups) Node Groups

In ComfyUI, you can select multiple parts of a workflow simultaneously, then use the right-click menu to merge them into a node group, making that part a reusable module that can be repeatedly called in your ComfyUI.

## [​](http://docs.comfy.org#custom-nodes) Custom Nodes

ComfyUI includes many powerful nodes in the base installation package. These are known as **Comfy Core** nodes. Additionally, the ComfyUI community has created an amazing array of [***custom nodes***](https://registry.comfy.org) to perform a wide variety of functions.

## [​](http://docs.comfy.org#comfyui-manager) ComfyUI Manager

The **ComfyUI Manager** window makes it easy to perform custom node management tasks such as search, install, update, disable, and uninstall. The Manager is included in the ComfyUI desktop application, but not in the ComfyUI server application.

### [​](http://docs.comfy.org#installing-the-comfyui-manager) Installing the ComfyUI Manager

If you’re running the ComfyUI server application, you need to install the Manager. If ComfyUI is running, shut it down before proceeding.

The first step is to install Git, a command-line application for software version control. Git will download the ComfyUI Manager from [github.com](https://github.com). Download Git from [git-scm.com](https://git-scm.com/) and install it.

Once Git is installed, navigate to the ComfyUI server program directory, to the folder labeled **custom\_nodes**. Open up a command window or terminal. Make sure that the command line displays the current directory path as **custom\_nodes**. Enter the following command. This will download the Manager. Technically, this is known as *cloning a Git repository*.

```bash
git clone https://github.com/ltdrdata/ComfyUI-Manager.git
```

For details or special cases, see [ComfyUI Manager Install](https://github.com/ltdrdata/ComfyUI-Manager?tab=readme-ov-file#installation).

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/essentials/core-concepts/nodes.mdx)

[Previous](http://docs.comfy.org/essentials/core-concepts/workflow)

[Properties  
\
Next](http://docs.comfy.org/essentials/core-concepts/properties)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Nodes perform operations](http://docs.comfy.org#nodes-perform-operations)
- [Different Node States](http://docs.comfy.org#different-node-states)
- [Connections Between Nodes](http://docs.comfy.org#connections-between-nodes)
- [Connecting and Disconnecting Nodes](http://docs.comfy.org#connecting-and-disconnecting-nodes)
- [Node Appearance](http://docs.comfy.org#node-appearance)
- [Node Badges](http://docs.comfy.org#node-badges)
- [Node Context Menus](http://docs.comfy.org#node-context-menus)
- [Node Context Menu](http://docs.comfy.org#node-context-menu)
- [Mode](http://docs.comfy.org#mode)
- [Switching Between Widget and Input Mode for Node Inputs](http://docs.comfy.org#switching-between-widget-and-input-mode-for-node-inputs)
- [Input/Output Context Menu](http://docs.comfy.org#input%2Foutput-context-menu)
- [Node Selection Toolbox](http://docs.comfy.org#node-selection-toolbox)
- [Node Groups](http://docs.comfy.org#node-groups)
- [Custom Nodes](http://docs.comfy.org#custom-nodes)
- [ComfyUI Manager](http://docs.comfy.org#comfyui-manager)
- [Installing the ComfyUI Manager](http://docs.comfy.org#installing-the-comfyui-manager)