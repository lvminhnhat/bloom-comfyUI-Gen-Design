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

Settings

# Settings

You can provide a settings object to ComfyUI that will show up when the user opens the ComfyUI settings panel.

## [​](http://docs.comfy.org#basic-operation) Basic operation

### [​](http://docs.comfy.org#add-a-setting) Add a setting

```javascript
import { app } from "../../scripts/app.js";

app.registerExtension({
    name: "My Extension",
    settings: [
        {
            id: "example.boolean",
            name: "Example boolean setting",
            type: "boolean",
            defaultValue: false,
        },
    ],
});
```

The `id` must be unique across all extensions and will be used to fetch values.

If you do not [provide a category](http://docs.comfy.org/_sites/docs.comfy.org/custom-nodes/js/javascript_settings#categories), then the `id` will be split by `.` to determine where it appears in the settings panel.

- If your `id` doesn’t contain any `.` then it will appear in the “Other” category and your `id` will be used as the section heading.
- If your `id` contains at least one `.` then the leftmost part will be used as the setting category and the second part will be used as the section heading. Any further parts are ignored.

### [​](http://docs.comfy.org#read-a-setting) Read a setting

```javascript
import { app } from "../../scripts/app.js";

if (app.extensionManager.setting.get('example.boolean')) {
    console.log("Setting is enabled.");
} else {
    console.log("Setting is disabled.");
}
```

### [​](http://docs.comfy.org#react-to-changes) React to changes

The `onChange()` event handler will be called as soon as the user changes the setting in the settings panel.

This will also be called when the extension is registered, on every page load.

```javascript
{
    id: "example.boolean",
    name: "Example boolean setting",
    type: "boolean",
    defaultValue: false,
    onChange: (newVal, oldVal) => {
        console.log(`Setting was changed from ${oldVal} to ${newVal}`);
    },
}
```

### [​](http://docs.comfy.org#write-a-setting) Write a setting

```javascript
import { app } from "../../scripts/app.js";

try {
    await app.extensionManager.setting.set("example.boolean", true);
} catch (error) {
    console.error(`Error changing setting: ${error}`);
}
```

### [​](http://docs.comfy.org#extra-configuration) Extra configuration

The setting types are based on [PrimeVue](https://primevue.org/) components. Props described in the PrimeVue documentation can be defined for ComfyUI settings by adding them in an `attrs` field.

For instance, this adds increment/decrement buttons to a number input:

```javascript
{
    id: "example.number",
    name: "Example number setting",
    type: "number",
    defaultValue: 0,
    attrs: {
        showButtons: true,
    },
    onChange: (newVal, oldVal) => {
        console.log(`Setting was changed from ${oldVal} to ${newVal}`);
    },
}
```

## [​](http://docs.comfy.org#types) Types

### [​](http://docs.comfy.org#boolean) Boolean

This shows an on/off toggle.

Based on the [ToggleSwitch PrimeVue component](https://primevue.org/toggleswitch/).

```javascript
{
    id: "example.boolean",
    name: "Example boolean setting",
    type: "boolean",
    defaultValue: false,
    onChange: (newVal, oldVal) => {
        console.log(`Setting was changed from ${oldVal} to ${newVal}`);
    },
}
```

### [​](http://docs.comfy.org#text) Text

This is freeform text.

Based on the [InputText PrimeVue component](https://primevue.org/inputtext/).

```javascript
{
    id: "example.text",
    name: "Example text setting",
    type: "text",
    defaultValue: "Foo",
    onChange: (newVal, oldVal) => {
        console.log(`Setting was changed from ${oldVal} to ${newVal}`);
    },
}
```

### [​](http://docs.comfy.org#number) Number

This for entering numbers.

To allow decimal places, set the `maxFractionDigits` attribute to a number greater than zero.

Based on the [InputNumber PrimeVue component](https://primevue.org/inputnumber/).

```javascript
{
    id: "example.number",
    name: "Example number setting",
    type: "number",
    defaultValue: 42,
    attrs: {
        showButtons: true,
        maxFractionDigits: 1,
    },
    onChange: (newVal, oldVal) => {
        console.log(`Setting was changed from ${oldVal} to ${newVal}`);
    },
}
```

### [​](http://docs.comfy.org#slider) Slider

This lets the user enter a number directly or via a slider.

Based on the [Slider PrimeVue component](https://primevue.org/slider/). Ranges are not supported.

```javascript
{
    id: "example.slider",
    name: "Example slider setting",
    type: "slider",
    attrs: {
        min: -10,
        max: 10,
        step: 0.5,
    },
    defaultValue: 0,
    onChange: (newVal, oldVal) => {
        console.log(`Setting was changed from ${oldVal} to ${newVal}`);
    },
}
```

### [​](http://docs.comfy.org#combo) Combo

This lets the user pick from a drop-down list of values.

You can provide options either as a plain string or as an object with `text` and `value` fields. If you only provide a plain string, then it will be used for both.

You can let the user enter freeform text by supplying the `editable: true` attribute, or search by supplying the `filter: true` attribute.

Based on the [Select PrimeVue component](https://primevue.org/select/). Groups are not supported.

```javascript
{
    id: "example.combo",
    name: "Example combo setting",
    type: "combo",
    defaultValue: "first",
    options: [
        { text: "My first option", value: "first" },
        "My second option",
    ],
    attrs: {
        editable: true,
        filter: true,
    },
    onChange: (newVal, oldVal) => {
        console.log(`Setting was changed from ${oldVal} to ${newVal}`);
    },
}
```

### [​](http://docs.comfy.org#color) Color

This lets the user select a color from a color picker or type in a hex reference.

Note that the format requires six full hex digits - three digit shorthand does not work.

Based on the [ColorPicker PrimeVue component](https://primevue.org/colorpicker/).

```javascript
{
    id: "example.color",
    name: "Example color setting",
    type: "color",
    defaultValue: "ff0000",
    onChange: (newVal, oldVal) => {
        console.log(`Setting was changed from ${oldVal} to ${newVal}`);
    },
}
```

### [​](http://docs.comfy.org#image) Image

This lets the user upload an image.

The setting will be saved as a [data URL](https://developer.mozilla.org/en-US/docs/Web/URI/Schemes/data).

Based on the [FileUpload PrimeVue component](https://primevue.org/fileupload/).

```javascript
{
    id: "example.image",
    name: "Example image setting",
    type: "image",
    onChange: (newVal, oldVal) => {
        console.log(`Setting was changed from ${oldVal} to ${newVal}`);
    },
}
```

### [​](http://docs.comfy.org#hidden) Hidden

Hidden settings aren’t displayed in the settings panel, but you can read and write to them from your code.

```javascript
{
    id: "example.hidden",
    name: "Example hidden setting",
    type: "hidden",
}
```

## [​](http://docs.comfy.org#other) Other

### [​](http://docs.comfy.org#categories) Categories

You can specify the categorisation of your setting separately to the `id`. This means you can change the categorisation and naming without changing the `id` and losing the values that have already been set by users.

```javascript
{
    id: "example.boolean",
    name: "Example boolean setting",
    type: "boolean",
    defaultValue: false,
    category: ["Category name", "Section heading", "Setting label"],
}
```

### [​](http://docs.comfy.org#tooltips) Tooltips

You can add extra contextual help with the `tooltip` field. This adds a small ℹ︎ icon after the field name that will show the help text when the user hovers over it.

```javascript
{
    id: "example.boolean",
    name: "Example boolean setting",
    type: "boolean",
    defaultValue: false,
    tooltip: "This is some helpful information",
}
```

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/custom-nodes/js/javascript_settings.mdx)

[Previous](http://docs.comfy.org/custom-nodes/js/javascript_objects_and_hijacking)

[Annotated Examples  
\
Next](http://docs.comfy.org/custom-nodes/js/javascript_examples)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [Basic operation](http://docs.comfy.org#basic-operation)
- [Add a setting](http://docs.comfy.org#add-a-setting)
- [Read a setting](http://docs.comfy.org#read-a-setting)
- [React to changes](http://docs.comfy.org#react-to-changes)
- [Write a setting](http://docs.comfy.org#write-a-setting)
- [Extra configuration](http://docs.comfy.org#extra-configuration)
- [Types](http://docs.comfy.org#types)
- [Boolean](http://docs.comfy.org#boolean)
- [Text](http://docs.comfy.org#text)
- [Number](http://docs.comfy.org#number)
- [Slider](http://docs.comfy.org#slider)
- [Combo](http://docs.comfy.org#combo)
- [Color](http://docs.comfy.org#color)
- [Image](http://docs.comfy.org#image)
- [Hidden](http://docs.comfy.org#hidden)
- [Other](http://docs.comfy.org#other)
- [Categories](http://docs.comfy.org#categories)
- [Tooltips](http://docs.comfy.org#tooltips)