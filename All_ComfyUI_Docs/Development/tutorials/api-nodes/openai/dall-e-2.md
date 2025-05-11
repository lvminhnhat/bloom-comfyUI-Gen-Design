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
  
  - [Overview](http://docs.comfy.org/tutorials/api-nodes/overview)
  - [FAQs](http://docs.comfy.org/tutorials/api-nodes/faq)
  - [Pricing](http://docs.comfy.org/tutorials/api-nodes/pricing)
  - Black Forest Labs
  - Stability AI
  - Ideogram
  - Luma
  - OpenAI
    
    - [GPT-Image-1](http://docs.comfy.org/tutorials/api-nodes/openai/gpt-image-1)
    - [DALL·E 2](http://docs.comfy.org/tutorials/api-nodes/openai/dall-e-2)
    - [DALL·E 3](http://docs.comfy.org/tutorials/api-nodes/openai/dall-e-3)
  - Recraft

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

OpenAI DALL·E 2 Node

# OpenAI DALL·E 2 Node

Learn how to use the OpenAI DALL·E 2 API node to generate images in ComfyUI

OpenAI DALL·E 2 is part of the ComfyUI API Nodes series, allowing users to generate images through OpenAI’s **DALL·E 2** model.

This node supports:

- Text-to-image generation
- Image editing functionality (inpainting through masks)

## [​](http://docs.comfy.org#node-overview) Node Overview

The **OpenAI DALL·E 2** node generates images synchronously through OpenAI’s image generation API. It receives text prompts and returns images that match the description.

To use the API nodes, you need to ensure that you are logged in properly and using a permitted network environment. Please refer to the [API Nodes Overview](http://docs.comfy.org/tutorials/api-nodes/overview) section of the documentation to understand the specific requirements for using the API nodes.

## [​](http://docs.comfy.org#parameter-description) Parameter Description

### [​](http://docs.comfy.org#required-parameters) Required Parameters

ParameterDescription`prompt`Text prompt describing the image content you want to generate

### [​](http://docs.comfy.org#widget-parameters) Widget Parameters

ParameterDescriptionOptions/RangeDefault Value`seed`Seed value for image generation (currently not implemented in the backend)0 to 2^31-10`size`Output image dimensions”256x256”, “512x512”, “1024x1024""1024x1024”`n`Number of images to generate1 to 81

### [​](http://docs.comfy.org#optional-parameters) Optional Parameters

ParameterDescriptionOptions/RangeDefault Value`image`Optional reference image for image editingAny image inputNone`mask`Optional mask for local inpaintingMask inputNone

## [​](http://docs.comfy.org#usage-method) Usage Method

## [​](http://docs.comfy.org#workflow-examples) Workflow Examples

This API node currently supports two workflows:

- Text to Image
- Inpainting

Image to Image workflow is not supported

### [​](http://docs.comfy.org#text-to-image-example) Text to Image Example

The image below contains a simple text-to-image workflow. Please download the corresponding image and drag it into ComfyUI to load the workflow.

The corresponding example is very simple

You only need to load the `OpenAI DALL·E 2` node, input the description of the image you want to generate in the `prompt` node, connect a `Save Image` node, and then run the workflow.

### [​](http://docs.comfy.org#inpainting-workflow) Inpainting Workflow

DALL·E 2 supports image editing functionality, allowing you to use a mask to specify the area to be replaced. Below is a simple inpainting workflow example:

#### [​](http://docs.comfy.org#1-workflow-file-download) 1. Workflow File Download

Download the image below and drag it into ComfyUI to load the corresponding workflow.

We will use the image below as input:

#### [​](http://docs.comfy.org#2-workflow-file-usage-instructions) 2. Workflow File Usage Instructions

Since this workflow is relatively simple, if you want to manually implement the corresponding workflow yourself, you can follow the steps below:

1. Use the `Load Image` node to load the image
2. Right-click on the load image node and select `MaskEditor`
3. In the mask editor, use the brush to draw the area you want to redraw
4. Connect the loaded image to the `image` input of the **OpenAI DALL·E 2** node
5. Connect the mask to the `mask` input of the **OpenAI DALL·E 2** node
6. Edit the prompt in the `prompt` node
7. Run the workflow

**Notes**

- If you want to use the image editing functionality, you must provide both an image and a mask (both are required)
- The mask and image must be the same size
- When inputting large images, the node will automatically resize the image to an appropriate size
- The URLs returned by the API are valid for a short period, please save the results promptly
- Each generation consumes credits, charged according to image size and quantity

## [​](http://docs.comfy.org#faqs) FAQs

Why can't I find the API nodes?

Please update your ComfyUI to the latest version (the latest commit or the latest [desktop version](https://www.comfy.org/download)). We may add more API support in the future, and the corresponding nodes will be updated, so please keep your ComfyUI up to date.

Please note that you need to distinguish between the nightly version and the release version. In some cases, the latest `release` version may not be updated in time compared to the `nightly` version. Since we are still iterating quickly, please ensure you are using the latest version when you cannot find the corresponding node.

Why can't I use / log in to the API Nodes?

API access requires that your current request is based on a secure network environment. The current requirements for API access are as follows:

- The local network only allows access from `127.0.0.1` or `localhost`, which may mean that you cannot use the API Nodes in a ComfyUI service started with the `--listen` parameter in a LAN environment.
- Able to access our API service normally (a proxy service may be required in some regions).
- Your account does not have enough [credits](http://docs.comfy.org/interface/credits).

Why can't I use API node even after logging in, or why does it keep asking me to log in while using?

- Currently, only `127.0.0.1` or `localhost` access is supported.
- Ensure your account has enough credits.

Can API Nodes be used for free?

API Nodes require credits for API calls to closed-source models, so they do not support free usage.

How to purchase credits?

Please refer to the following documentation:

1. [Comfy Account](http://docs.comfy.org/interface/user): Find the `User` section in the settings menu to log in.
2. [Credits](http://docs.comfy.org/interface/credits): After logging in, the settings interface will show the credits menu. You can purchase credits in `Settings` → `Credits`. We use a prepaid system, so there will be no unexpected charges.
3. Complete the payment through Stripe.
4. Check if the credits have been updated. If not, try restarting or refreshing the page.

Are unused credits refundable?

Currently, we do not support refunds for credits. If you believe there is an error resulting in unused balance due to technical issues, please [contact support](mailto:support@comfy.org).

Can credits go negative?

Credits cannot go negative, so please ensure you have enough credits before making the corresponding API calls.

Where can I check usage and expenses?

Please visit the [Credits](http://docs.comfy.org/interface/credits) menu after logging in to check the corresponding credits.

Is it possible to use my own API Key?

Currently, the API Nodes are still in the testing phase and do not support this feature yet, but we have considered adding it.

Do credits expire?

No, your credits do not expire.

Can credits be transferred or shared?

No, your credits cannot be transferred to other users and are limited to the currently logged-in account, but we do not restrict the number of devices that can log in.

Can I use the same account on different devices?

We do not limit the number of devices that can log in; you can use your account anywhere you want.

How can I request for my account or information to be deleted??

Email a request to [support@comfy.org](mailto:support@comfy.org) and we will delete your information

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/tutorials/api-nodes/openai/dall-e-2.mdx)

[Previous](http://docs.comfy.org/tutorials/api-nodes/openai/gpt-image-1)

[DALL·E 3Learn how to use the OpenAI DALL·E 3 API node to generate images in ComfyUI  
\
Next](http://docs.comfy.org/tutorials/api-nodes/openai/dall-e-3)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Node Overview](http://docs.comfy.org#node-overview)
- [Parameter Description](http://docs.comfy.org#parameter-description)
- [Required Parameters](http://docs.comfy.org#required-parameters)
- [Widget Parameters](http://docs.comfy.org#widget-parameters)
- [Optional Parameters](http://docs.comfy.org#optional-parameters)
- [Usage Method](http://docs.comfy.org#usage-method)
- [Workflow Examples](http://docs.comfy.org#workflow-examples)
- [Text to Image Example](http://docs.comfy.org#text-to-image-example)
- [Inpainting Workflow](http://docs.comfy.org#inpainting-workflow)
- [1. Workflow File Download](http://docs.comfy.org#1-workflow-file-download)
- [2. Workflow File Usage Instructions](http://docs.comfy.org#2-workflow-file-usage-instructions)
- [FAQs](http://docs.comfy.org#faqs)