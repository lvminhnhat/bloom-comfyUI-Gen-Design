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

API Nodes

# API Nodes

In this article, we will introduce ComfyUI’s API Nodes and related information.

API Nodes are ComfyUI’s new way of calling closed-source models through API requests, providing ComfyUI users with access to external state-of-the-art AI models without complex API key setup.

## [​](http://docs.comfy.org#what-are-api-nodes%3F) What are API Nodes?

API Nodes are a set of special nodes that connect to external API services, allowing you to use closed-source or third-party hosted AI models directly in your ComfyUI workflows. These nodes are designed to seamlessly integrate the capabilities of external models while maintaining the open-source nature of ComfyUI’s core.

Currently supported models include:

- Black Forest Labs Flux 1.1\[pro] Ultra, Flux .1\[pro]
- Kling 2.0, 1.6, 1.5 &amp; Various Effects
- Luma Photon, Ray2, Ray1.6
- MiniMax Text-to-Video, Image-to-Video
- PixVerse V4 &amp; Effects
- Recraft V3, V2 &amp; Various Tools
- Stability AI Stable Image Ultra, Stable Diffusion 3.5 Large
- Google Veo2
- Ideogram V3, V2, V1
- OpenAI GPT4o image
- Pika 2.2

## [​](http://docs.comfy.org#prerequisites-for-using-api-nodes) Prerequisites for Using API Nodes

To use API Nodes, the following requirements must be met:

### [​](http://docs.comfy.org#1-comfyui-version-requirements) 1. ComfyUI Version Requirements

Please update your ComfyUI to the latest version, as we may add more API support in the future, and corresponding nodes will be updated, so please keep your ComfyUI up to date.

Please note the distinction between nightly and release versions. We recommend using the `nightly` version (which is the latest code commit), as the release version may not be updated in a timely manner. This refers to the development version and the stable version, and since we are still rapidly iterating, this document may not be updated promptly, so please pay attention to the version differences.

### [​](http://docs.comfy.org#2-network-environment-requirements) 2. Network Environment Requirements

API access requires that your current requests are based on a secure network environment. The current requirements for API access are as follows:

- Local networks only allow access from `127.0.0.1`. We do not support accessing via LAN IPs without `https` as it is insecure. This may mean that you cannot use API Nodes in a ComfyUI service launched with the `--listen` parameter in a LAN environment.
- You must be able to access our API services normally (in some regions, you may need to use a proxy service).

Accessing in an insecure context poses significant risks, which may result in the following consequences:

1. Authentication may be stolen, leading to the leakage of your account information.
2. Your account may be maliciously used, resulting in financial losses.

Even if we open this restriction in the future, we strongly advise against accessing API services through insecure network requests due to the high risks involved.

### [​](http://docs.comfy.org#3-account-and-credits-requirements) 3. Account and Credits Requirements

You need to be logged into your ComfyUI with a [Comfy account](http://docs.comfy.org/zh-CN/interface/user) and have a credit balance of [credits](http://docs.comfy.org/zh-CN/interface/credits) greater than 0.

Please refer to the corresponding documentation for account and credits to ensure this requirement:

- [Comfy account](http://docs.comfy.org/zh-CN/interface/user): Find the `User` section in the settings menu to log in.
- [Credits](http://docs.comfy.org/zh-CN/interface/credits): After logging in, the settings interface will show a credits menu where you can purchase credits. We use a prepaid system, so there will be no unexpected charges.

### [​](http://docs.comfy.org#4-using-the-corresponding-nodes) 4. Using the Corresponding Nodes

**Add to Workflow**: Add the API node to your workflow just like you would with other nodes. **Run**: Set the parameters and then run the workflow.

## [​](http://docs.comfy.org#log-in-with-api-key-on-non-whitelisted-websites) Log in with API Key on non-whitelisted websites

Currently, we have set up a whitelist to restrict the websites where you can log in to your ComfyUI account. If you need to log in to your ComfyUI account on some non-whitelisted websites, please refer to the account management section to learn how to log in using an API Key. In this case, the corresponding website does not need to be on our whitelist.

[**Account Management**  
\
Learn how to log in with ComfyUI API Key](http://docs.comfy.org/interface/user#logging-in-with-an-api-key)

## [​](http://docs.comfy.org#advantages-of-api-nodes) Advantages of API Nodes

API Nodes provide several important advantages for ComfyUI users:

- **Access to closed-source models**: Use state-of-the-art AI models without having to deploy them yourself
- **Seamless integration**: API nodes are fully compatible with other ComfyUI nodes and can be combined to create complex workflows
- **Simplified experience**: No need to manage API keys or handle complex API requests
- **Controlled costs**: The prepaid system ensures you have complete control over your spending with no unexpected charges

## [​](http://docs.comfy.org#pricing) Pricing

[**API Node Pricing**  
\
Please refer to the pricing page for the corresponding API pricing](http://docs.comfy.org/tutorials/api-nodes/pricing)

## [​](http://docs.comfy.org#about-open-source-and-opt-in) About Open Source and Opt-in

It’s important to note that **API Nodes are completely optional**. ComfyUI will always remain fully open-source and free for local users. API nodes are designed as an “opt-in” feature, providing convenience for those who want access to external SOTA (state-of-the-art) models.

## [​](http://docs.comfy.org#use-cases) Use Cases

A powerful application of API Nodes is combining the output of external models with local nodes. For example:

- Using GPT-Image-1 to generate a base image, then transforming it into video with a local `wan` node
- Combining externally generated images with local upscaling or style transfer nodes
- Creating hybrid workflows that leverage the advantages of both closed-source and open-source models

This flexibility makes ComfyUI a truly universal generative AI interface, integrating various AI capabilities into a unified workflow, opening up more possibilities

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

[Suggest edits](https://github.com/comfy-org/docs/edit/main/tutorials/api-nodes/overview.mdx)

[Previous](http://docs.comfy.org/tutorials/audio/ace-step/ace-step-v1)

[FAQsSome FAQs you may encounter when using API Nodes.  
\
Next](http://docs.comfy.org/tutorials/api-nodes/faq)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [What are API Nodes?](http://docs.comfy.org#what-are-api-nodes%3F)
- [Prerequisites for Using API Nodes](http://docs.comfy.org#prerequisites-for-using-api-nodes)
- [1. ComfyUI Version Requirements](http://docs.comfy.org#1-comfyui-version-requirements)
- [2. Network Environment Requirements](http://docs.comfy.org#2-network-environment-requirements)
- [3. Account and Credits Requirements](http://docs.comfy.org#3-account-and-credits-requirements)
- [4. Using the Corresponding Nodes](http://docs.comfy.org#4-using-the-corresponding-nodes)
- [Log in with API Key on non-whitelisted websites](http://docs.comfy.org#log-in-with-api-key-on-non-whitelisted-websites)
- [Advantages of API Nodes](http://docs.comfy.org#advantages-of-api-nodes)
- [Pricing](http://docs.comfy.org#pricing)
- [About Open Source and Opt-in](http://docs.comfy.org#about-open-source-and-opt-in)
- [Use Cases](http://docs.comfy.org#use-cases)
- [FAQs](http://docs.comfy.org#faqs)