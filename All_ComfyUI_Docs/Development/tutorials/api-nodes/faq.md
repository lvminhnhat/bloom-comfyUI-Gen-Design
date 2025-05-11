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

FAQs about API Nodes

# FAQs about API Nodes

Some FAQs you may encounter when using API Nodes.

This article addresses common questions regarding the use of API nodes.

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

[Suggest edits](https://github.com/comfy-org/docs/edit/main/tutorials/api-nodes/faq.mdx)

[Previous](http://docs.comfy.org/tutorials/api-nodes/overview)

[PricingThis article lists the pricing of the current API Nodes.  
\
Next](http://docs.comfy.org/tutorials/api-nodes/pricing)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)