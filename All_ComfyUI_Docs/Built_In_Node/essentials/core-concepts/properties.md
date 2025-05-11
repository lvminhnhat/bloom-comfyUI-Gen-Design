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

Properties

# Properties

## [​](http://docs.comfy.org#nodes-are-containers-for-properties) Nodes are containers for properties

Nodes usually have ***properties***. Also known as ***parameters*** or ***attributes***, node properties are variables that can be changed. Some properties can be adjusted manually by the user, using a data entry field called a ***widget***. Other properties can be driven automatically by other nodes connected to the property ***input slot*** or port. Usually, a property can be converted from widget to input and vice versa, allowing users to control property values manually or automatically.

Properties can take many forms and hold many different types of information. For example, a **Load Checkpoint** node has a single property:  the file path to the generative model checkpoint file. A **KSampler** node has multiple properties such as the number of sampling **steps**, **CFG** scale, **sampler\_name**, etc.

## [​](http://docs.comfy.org#data-types) Data types

Information can come in many different forms, called ***data types***. For example, alphanumeric text is known as a ***string***, a whole number is an ***integer***, and a number with a decimal point is known as a ***floating point*** number or ***float***. New data types are always being added to ComfyUI.

ComfyUI is written in the Python scripting language, which is very forgiving about data types. By contrast, the ComfyUI environment is very ***strongly typed***. This means that different data types can’t be mixed up. For example, we can’t connect an image output to an integer input. This is a huge benefit to users, guiding them to proper workflow construction and preventing program errors.

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/essentials/core-concepts/properties.mdx)

[Previous](http://docs.comfy.org/essentials/core-concepts/nodes)

[LinksUnderstand connection links in ComfyUI  
\
Next](http://docs.comfy.org/essentials/core-concepts/links)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Nodes are containers for properties](http://docs.comfy.org#nodes-are-containers-for-properties)
- [Data types](http://docs.comfy.org#data-types)