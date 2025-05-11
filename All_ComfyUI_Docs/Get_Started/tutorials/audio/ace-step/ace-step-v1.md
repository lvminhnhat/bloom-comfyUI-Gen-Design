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
  
  - [ACE-Step Music Generation](http://docs.comfy.org/tutorials/audio/ace-step/ace-step-v1)
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

ComfyUI ACE-Step Native Example

# ComfyUI ACE-Step Native Example

This guide will help you create dynamic music using the ACE-Step model in ComfyUI

ACE-Step is an open-source foundational music generation model jointly developed by Chinese team StepFun and ACE Studio, aimed at providing music creators with efficient, flexible and high-quality music generation and editing tools.

The model is released under the [Apache-2.0](https://github.com/ace-step/ACE-Step?tab=readme-ov-file#-license) license and is free for commercial use.

As a powerful music generation foundation, ACE-Step provides rich extensibility. Through fine-tuning techniques like LoRA and ControlNet, developers can customize the model according to their actual needs. Whether it’s audio editing, vocal synthesis, accompaniment production, voice cloning or style transfer applications, ACE-Step provides stable and reliable technical support. This flexible architecture greatly simplifies the development process of music AI applications, allowing more creators to quickly apply AI technology to music creation.

Currently, ACE-Step has released related training code, including LoRA model training, and the corresponding ControlNet training code will be released in the future. You can visit their [Github](https://github.com/ace-step/ACE-Step?tab=readme-ov-file#-roadmap) to learn more details.

## [​](http://docs.comfy.org#ace-step-comfyui-text-to-audio-generation-workflow-example) ACE-Step ComfyUI Text-to-Audio Generation Workflow Example

### [​](http://docs.comfy.org#1-download-workflow-and-related-models) 1. Download Workflow and Related Models

Click the button below to download the corresponding workflow file. Drag it into ComfyUI to load the workflow information. The workflow includes model download information.

Click the button below to download the corresponding workflow file. Drag it into ComfyUI to load the workflow information. The workflow includes model download information.

[Download Json Format Workflow File](https://raw.githubusercontent.com/Comfy-Org/example_workflows/main/audio/ace-step/ace_step_1_t2m.json)

You can also manually download [ace\_step\_v1\_3.5b.safetensors](https://huggingface.co/Comfy-Org/ACE-Step_ComfyUI_repackaged/blob/main/all_in_one/ace_step_v1_3.5b.safetensors) and save it to the `ComfyUI/models/checkpoints` folder

### [​](http://docs.comfy.org#2-complete-the-workflow-step-by-step) 2. Complete the Workflow Step by Step

1. Ensure the `Load Checkpoints` node has loaded the `ace_step_v1_3.5b.safetensors` model
2. Input corresponding music styles etc. in the `tags` field of `TextEncodeAceStepAudio`
3. Input corresponding lyrics in the `lyrics` field of `TextEncodeAceStepAudio`
4. Click the `Run` button, or use the shortcut `Ctrl(cmd) + Enter` to execute the generation
5. After the generation is complete, you can view the generated audio in the `Save Audio` node. You can click to play and preview. The audio will also be saved to `ComfyUI/output/audio` (subdirectory determined by the `Save Audio` node).

## [​](http://docs.comfy.org#ace-step-comfyui-audio-to-audio-workflow) ACE-Step ComfyUI Audio-to-Audio Workflow

Similar to image-to-image workflows, you can input a piece of music and use the workflow below to resample and generate music. You can also adjust the difference from the original audio by controlling the `denoise` parameter in the `Ksampler`.

### [​](http://docs.comfy.org#1-download-workflow-file) 1. Download Workflow File

Click the button below to download the corresponding workflow file. Drag it into ComfyUI to load the workflow information.

[Download Json Format Workflow File](https://raw.githubusercontent.com/Comfy-Org/example_workflows/main/audio/ace-stepace_step_1_m2m_editing.json)

### [​](http://docs.comfy.org#2-complete-the-workflow-step-by-step-2) 2. Complete the Workflow Step by Step

1. Ensure the `Load Checkpoints` node has loaded the `ace_step_v1_3.5b.safetensors` model
2. Upload the music you want to edit in the `LoadAudio` node (you can use the results generated from the text-to-audio workflow in this article)
3. Input corresponding music styles etc. in the `tags` field of `TextEncodeAceStepAudio`
4. Input corresponding lyrics in the `lyrics` field of `TextEncodeAceStepAudio`, you can refer to the prompt guide part (still updating) or the lyrics examples on the ACE-Step project page
5. Modify the `denoise` parameter in the `Ksampler` node to adjust the amount of noise added during sampling, which controls the similarity to the original audio (smaller values result in greater similarity to the original audio; if set to `1.00`, it can be considered as if there is no audio input)
6. Click the `Run` button, or use the shortcut `Ctrl(cmd) + Enter` to execute the audio generation
7. After the generation is complete, you can view the generated audio in the `Save Audio` node. You can click to play and preview. The audio will also be saved to `ComfyUI/output/audio` (subdirectory determined by the `Save Audio` node).

You can also implement the lyrics modification and editing functionality from the ACE-Step project page, modifying the original lyrics to change the audio effect.

### [​](http://docs.comfy.org#3-lyrics-modification-and-editing-example) 3. Lyrics Modification and Editing Example

\[To be updated]

## [​](http://docs.comfy.org#ace-step-prompt-guide) ACE-Step Prompt Guide

ACE currently uses two types of prompts: `tags` and `lyrics`.

- `tags`: Mainly used to describe music styles, scenes, etc. Similar to prompts we use for other generations, they primarily describe the overall style and requirements of the audio, separated by English commas
- `lyrics`: Mainly used to describe lyrics, supporting lyric structure tags such as \[verse], \[chorus], and \[bridge] to distinguish different parts of the lyrics. You can also input instrument names for purely instrumental music

You can find rich examples of `tags` and `lyrics` on the [ACE-Step model homepage](https://ace-step.github.io/). You can refer to these examples to try corresponding prompts. This document’s prompt guide is organized based on the project to help you quickly try combinations to achieve your desired effect.

### [​](http://docs.comfy.org#tags-prompt) Tags (prompt)

#### [​](http://docs.comfy.org#mainstream-music-styles) Mainstream Music Styles

Use short tag combinations to generate specific music styles

- electronic
- rock
- pop
- funk
- soul
- cyberpunk
- Acid jazz
- electro
- em (electronic music)
- soft electric drums
- melodic

#### [​](http://docs.comfy.org#scene-types) Scene Types

Combine specific usage scenarios and atmospheres to generate music that matches the corresponding mood

- background music for parties
- radio broadcasts
- workout playlists

#### [​](http://docs.comfy.org#instrumental-elements) Instrumental Elements

- saxophone
- jazz
- piano, violin

#### [​](http://docs.comfy.org#vocal-types) Vocal Types

- female voice
- male voice
- clean vocals

#### [​](http://docs.comfy.org#professional-terms) Professional Terms

Use some professional terms commonly used in music to precisely control music effects

- 110 bpm (beats per minute is 110)
- fast tempo
- slow tempo
- loops
- fills
- acoustic guitar
- electric bass

### [​](http://docs.comfy.org#lyrics) Lyrics

#### [​](http://docs.comfy.org#lyric-structure-tags) Lyric Structure Tags

- \[outro]
- \[verse]
- \[chorus]
- \[bridge]

#### [​](http://docs.comfy.org#multilingual-support) Multilingual Support

- ACE-Step V1 supports multiple languages. When used, ACE-Step converts different languages into English letters and then generates music.
- In ComfyUI, we haven’t fully implemented the conversion of all languages to English letters. Currently, only [Japanese hiragana and katakana characters](https://github.com/comfyanonymous/ComfyUI/commit/5d3cc85e13833aeb6ef9242cdae243083e30c6fc) are implemented. So if you need to use multiple languages for music generation, you need to first convert the corresponding language to English letters, and then input the language code abbreviation at the beginning of the `lyrics`, such as Chinese `[zh]`, Korean `[ko]`, etc.

For example:

```plaintext
[zh]ni hao
[ko]an nyeong
```

Currently, ACE-Step supports 19 languages, but the following ten languages have better support:

- English
- Chinese: \[zh]
- Russian: \[ru]
- Spanish: \[es]
- Japanese: \[ja]
- German: \[de]
- French: \[fr]
- Portuguese: \[pt]
- Italian: \[it]
- Korean: \[ko]

The language tags above have not been fully tested at the time of writing this documentation. If any language tag is incorrect, please [submit an issue to our documentation repository](https://github.com/Comfy-Org/docs/issues) and we will make timely corrections.

## [​](http://docs.comfy.org#ace-step-related-resources) ACE-Step Related Resources

- [Project Page](https://ace-step.github.io/)
- [Hugging Face](https://huggingface.co/ACE-Step/ACE-Step-v1-3.5B)
- [GitHub](https://github.com/ace-step/ACE-Step)
- [Training Scripts](https://github.com/ace-step/ACE-Step?tab=readme-ov-file#-train)

Was this page helpful?

YesNo

[Suggest edits](https://github.com/comfy-org/docs/edit/main/tutorials/audio/ace-step/ace-step-v1.mdx)

[Previous](http://docs.comfy.org/tutorials/video/wan/wan-flf)

[OverviewIn this article, we will introduce ComfyUI's API Nodes and related information.  
\
Next](http://docs.comfy.org/tutorials/api-nodes/overview)

[github](https://github.com/comfyanonymous/ComfyUI/)

[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=referral&utm_source=docs.comfy.org)

On this page

- [ACE-Step ComfyUI Text-to-Audio Generation Workflow Example](http://docs.comfy.org#ace-step-comfyui-text-to-audio-generation-workflow-example)
- [1. Download Workflow and Related Models](http://docs.comfy.org#1-download-workflow-and-related-models)
- [2. Complete the Workflow Step by Step](http://docs.comfy.org#2-complete-the-workflow-step-by-step)
- [ACE-Step ComfyUI Audio-to-Audio Workflow](http://docs.comfy.org#ace-step-comfyui-audio-to-audio-workflow)
- [1. Download Workflow File](http://docs.comfy.org#1-download-workflow-file)
- [2. Complete the Workflow Step by Step](http://docs.comfy.org#2-complete-the-workflow-step-by-step-2)
- [3. Lyrics Modification and Editing Example](http://docs.comfy.org#3-lyrics-modification-and-editing-example)
- [ACE-Step Prompt Guide](http://docs.comfy.org#ace-step-prompt-guide)
- [Tags (prompt)](http://docs.comfy.org#tags-prompt)
- [Mainstream Music Styles](http://docs.comfy.org#mainstream-music-styles)
- [Scene Types](http://docs.comfy.org#scene-types)
- [Instrumental Elements](http://docs.comfy.org#instrumental-elements)
- [Vocal Types](http://docs.comfy.org#vocal-types)
- [Professional Terms](http://docs.comfy.org#professional-terms)
- [Lyrics](http://docs.comfy.org#lyrics)
- [Lyric Structure Tags](http://docs.comfy.org#lyric-structure-tags)
- [Multilingual Support](http://docs.comfy.org#multilingual-support)
- [ACE-Step Related Resources](http://docs.comfy.org#ace-step-related-resources)