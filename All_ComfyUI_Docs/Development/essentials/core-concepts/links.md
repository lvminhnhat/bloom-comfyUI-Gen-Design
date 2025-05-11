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

Links

# Links

Understand connection links in ComfyUI

As ComfyUI is still in rapid iteration and development, we are continuously improving it every day. Therefore, some operations mentioned in this article may change or be omitted. Please refer to the actual interface. If you find changes in actual operations, it may be due to our iterative updates. You can also fork [this repo](https://github.com/Comfy-Org/docs) and help us improve this documentation.

## [​](http://docs.comfy.org#links-connect-nodes) Links connect nodes

In the terminology of ComfyUI, the lines or curves between nodes are called ***links***. They’re also known as ***connections*** or wires. Links can be displayed in several ways, such as curves, right angles, straight lines, or completely hidden.

You can modify the link style in **Setup Menu** —&gt; **Display (Lite Graph)** —&gt; **Graph** —&gt; **Link Render Mode**.

You can also temporarily hide links in the **Canvas Menu**.

Link display is crucial. Depending on the situation, it may be necessary to see all links. Especially when learning, sharing, or even just understanding workflows, the visibility of links enables users to follow the flow of data through the graph. For packaged workflows that aren’t intended to be altered, it might make sense to hide the links to reduce clutter.

### [​](http://docs.comfy.org#reroute-node) Reroute node

If legibility of the graph structure is important, then link wires can be manually routed in the 2D space of the graph with a tiny node called **Reroute**. Its purpose is to position the beginning and/or end points of link wires to ensure visibility. We can design a workflow so that link wires don’t pass behind nodes, don’t cross other link wires, and so on.

We are also continuously improving the native reroute functionality in litegraph. We recommend using this feature in the future to reorganize connections.

## [​](http://docs.comfy.org#color-coding) Color-coding

The data type of node properties is indicated by color coding of input/output ports and link connection wires. We can always tell which inputs and outputs can be connected to one another by their color. Ports can only be connected to other ports of the same color to ensure matching data types.

Common data types:

Data typeColordiffusion modellavenderCLIP modelyellowVAE modelroseconditioningorangelatent imagepinkpixel imagebluemaskgreennumber (integer or float)light greenmeshbright green

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/essentials/core-concepts/links.mdx)

[Previous](http://docs.comfy.org/essentials/core-concepts/properties)

[Mask EditorLearn how to use the Mask Editor in ComfyUI, including settings and usage instructions  
\
Next](http://docs.comfy.org/interface/maskeditor)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Links connect nodes](http://docs.comfy.org#links-connect-nodes)
- [Reroute node](http://docs.comfy.org#reroute-node)
- [Color-coding](http://docs.comfy.org#color-coding)