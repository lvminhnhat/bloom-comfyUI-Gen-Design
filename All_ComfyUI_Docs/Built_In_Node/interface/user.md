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

Account Management

# Account Management

In this document, we will introduce the account management features of ComfyUI, including account login, registration, and logout operations.

The account system was added to support `API Nodes`, which enable calls to closed-source model APIs, greatly expanding the possibilities of ComfyUI. Since these API calls consume tokens, we have added a corresponding user system.

Currently, we support the following login methods:

- Email login
- Google login
- Github login
- API Key login (for non-whitelisted site authorization)

We will provide relevant login requirements and explanations in this document.

## [​](http://docs.comfy.org#comfyui-version-requirements) ComfyUI Version Requirements

You may need to use at least [ComfyUI v0.3.0](https://github.com/comfyanonymous/ComfyUI/releases/tag/v0.3.30) to use the account system. Ensure that the corresponding frontend version is at least `1.17.11`. Sometimes the frontend may fail to install and revert to an older version, so please check if the frontend version is greater than `1.17.11` in `Settings` -&gt; `About`.

In some regions, network restrictions may prevent normal access to the login API, causing timeouts or failures. Before logging in, please **ensure that your network environment does not restrict access to the corresponding API**, and make sure you can access sites like Google or Github.

As we are still rapidly iterating and updating, related features may change. If there are no special circumstances, please try to update to the latest version to access the relevant features.

## [​](http://docs.comfy.org#network-requirements) Network Requirements

To login to ComfyUI account, you must be in a secure network environment:

- Only allow access from `127.0.0.1` or `localhost`.
- Do not support using the `--listen` parameter to access the API node through a local network.
- If you are using a non-SSL certificate or a site that does not start with `https`, you may not be able to successfully log in.
- You may not be able to log in on a site that is not in our whitelist (but you can log in using an API Key now).
- Ensure you can connect to our service normally (some regions may require a proxy).

## [​](http://docs.comfy.org#how-to-log-in) How to Log In

Log in via `Settings` -&gt; `User`:

## [​](http://docs.comfy.org#login-methods) Login Methods

If this is your first login, please create an account first.

## [​](http://docs.comfy.org#logging-in-with-an-api-key) Logging in with an API Key

Since not all ComfyUI deployments are on our domain authorization whitelist, we have provided API Key login in a recent update (2025-05-10) for logging in through non-whitelisted sites. Below are the steps for logging in with an API Key:

- Have an API Key
- No API Key, Apply for an API Key First

1

Select Comfy API Key Login on the Login Screen

Select `Comfy API Key` login in the login popup

2

Enter Your API Key

1. Enter your API Key and save it
2. If you don’t have an API Key, click the `Get one here` link to go to [https://platform.comfy.org/login](https://platform.comfy.org/login) and log in to obtain it.

3

Login Successful

After a successful login, you can see the corresponding API Key login information in the settings menu

1

Select Comfy API Key Login on the Login Screen

Select `Comfy API Key` login in the login popup

2

Enter Your API Key

1. Enter your API Key and save it
2. If you don’t have an API Key, click the `Get one here` link to go to [https://platform.comfy.org/login](https://platform.comfy.org/login) and log in to obtain it.

3

Login Successful

After a successful login, you can see the corresponding API Key login information in the settings menu

Please refer to the following steps to apply for and obtain an API Key:

1

Visit https://platform.comfy.org/login and Log In

Please visit [https://platform.comfy.org/login](https://platform.comfy.org/login) and log in with the corresponding account

2

Click \`+ New\` in API Keys to Create an API Key

Click `+ New` in API Keys to create an API Key

3

Enter API Key Name

1. (Required) Enter the API Key name,
2. Click `Generate` to create

4

Save the Obtained API Key

Since the API Key is only visible upon first creation, please save it immediately after creation. It cannot be viewed later, so please keep it safe.

5

API Key Management

For unused API Keys or those at risk of being leaked, you can click `Delete` to remove them to prevent unnecessary losses.

6

(Optional) Log Out

If you have obtained an API Key and are logged in on a public device, please log out promptly.

## [​](http://docs.comfy.org#post-login-status) Post-Login Status

After logging in, a login button is displayed in the top menu bar of the ComfyUI interface. You can open the corresponding login interface through this button and log out of the corresponding account in the settings menu.

## [​](http://docs.comfy.org#frequently-asked-questions) Frequently Asked Questions

Are there any login device restrictions?

We do not restrict login devices. You can log in to your account on any device, but please note that your account information may be accessed by other devices, so do not log in to your account on public devices.

Why can't I log in with a LAN IP?

We do not currently support logging in via LAN IP because the security of the LAN environment is uncontrollable. Therefore, the current version does not fully support LAN IP login. We may consider handling LAN situations in the future.

Why can't I log in on some websites?

Our login service has a whitelist, so you may not be able to log in to ComfyUI deployed on some servers.

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/interface/user.mdx)

[Previous](http://docs.comfy.org/interface/overview)

[Credits ManagementIn this article, we will introduce ComfyUI's credit management features, including how to obtain, use, and view credits.  
\
Next](http://docs.comfy.org/interface/credits)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [ComfyUI Version Requirements](http://docs.comfy.org#comfyui-version-requirements)
- [Network Requirements](http://docs.comfy.org#network-requirements)
- [How to Log In](http://docs.comfy.org#how-to-log-in)
- [Login Methods](http://docs.comfy.org#login-methods)
- [Logging in with an API Key](http://docs.comfy.org#logging-in-with-an-api-key)
- [Post-Login Status](http://docs.comfy.org#post-login-status)
- [Frequently Asked Questions](http://docs.comfy.org#frequently-asked-questions)