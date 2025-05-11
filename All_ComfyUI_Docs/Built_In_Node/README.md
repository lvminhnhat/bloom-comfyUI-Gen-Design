# Built-In Node – Full Documentation Catalog  

> Read this file first if you are an LLM, plugin, or human reader that needs a **complete,
> machine-parsable overview** of everything inside `Built_In_Node/`.

---

## 0.  Purpose & Usage

1. Quick-scan the **Directory Tree** to know where to jump.
2. Use the **File Catalog** tables for a per-file summary (path + purpose).
3. Follow cross-references (`→`) if you need related concepts or prerequisite reading.

---

## 1. Directory Tree (high-level) 
```
Built_In_Node/
├── README.md                  ← Human-friendly landing page (high-level)
├── README_DIRECTORY.md        ← ***THIS FILE*** – exhaustive catalogue
├── essentials/
│   ├── core-concepts/
│   │   ├── workflow.md           ← How to create and manage workflows
│   │   ├── nodes.md             ← Understanding node types and usage
│   │   ├── properties.md        ← Configuring node properties
│   │   ├── links.md            ← Connecting nodes together
│   │   ├── models.md           ← Working with AI models
│   │   ├── dependencies.md     ← Managing node dependencies
│   │   ├── graph-engine.md     ← How the node graph system works
│   │   └── troubleshooting.md  ← Common issues and solutions
├── get-started/
│   ├── installation.md
│   ├── first-generation.md
│   ├── faq.md
├── interface/
│   ├── navigation.md
│   ├── settings.md
│   └── workspace.md
├── tutorials/
│   ├── basic-workflows.md
│   ├── advanced-workflows.md
│   └── custom-nodes.md
└── built-in-nodes/
    └── api-node/
        ├── image/
        │   ├── bfl/
        │   │   └── flux-pro-ultra-image.md
        │   ├── ideogram/
        │   │   ├── ideogram-v1.md
        │   │   ├── ideogram-v2.md
        │   │   └── ideogram-v3.md
        │   ├── luma/
        │   │   ├── luma-text-to-image.md
        │   │   ├── luma-image-to-image.md
        │   │   └── luma-reference.md
        │   └── recraft/
        │       ├── recraft-text-to-image.md
        │       ├── recraft-image-to-image.md
        │       ├── recraft-image-inpainting.md
        │       ├── recraft-text-to-vector.md
        │       ├── recraft-vectorize-image.md
        │       ├── recraft-color-rgb.md
        │       ├── recraft-controls.md
        │       ├── recraft-creative-upscale.md
        │       ├── recraft-crisp-upscale.md
        │       ├── recraft-remove-background.md
        │       ├── recraft-replace-background.md
        │       ├── recraft-style-realistic-image.md
        │       ├── recraft-style-digital-illustration.md
        │       ├── recraft-style-logo-raster.md
        │       └── save-svg.md
        └── video/
            ├── google/
            │   └── google-veo2-video.md
            └── kwai_vgi/
                └── kling-camera-control-i2v.md
```

---

## 2. File Catalog – Essentials

| File | Purpose / Key topics |
|------|---------------------|
| `essentials/core-concepts.md` | Comprehensive guide to ComfyUI's fundamental data-types, socket connection system, and execution order. Essential reading before working with API nodes. Includes detailed explanations of tensor types, image formats, and conditioning concepts. |
| `essentials/graph-engine.md` | In-depth technical exploration of ComfyUI's internal scheduler, batching mechanisms, and memory management. Contains performance optimization tips, GPU utilization strategies, and advanced execution flow control techniques. |
| `essentials/troubleshooting.md` | Complete error reference guide with detailed explanations of common error codes, log file interpretation, and hardware-specific troubleshooting for both NVIDIA and AMD GPUs. Includes solutions for CUDA out-of-memory errors and CPU fallback options. |

---

## 3. File Catalog – Getting Started

| File | Purpose |
|------|---------|
| `get-started/installation.md` | Comprehensive installation instructions for all major platforms: Windows (with and without CUDA), macOS (Intel/Apple Silicon), and Linux distributions. Includes portable installation options, Docker setup, and virtual environment configuration. Contains hardware requirement specifications and optimization settings. |
| `get-started/first-generation.md` | Beginner-friendly tutorial for creating your first image generation workflow. Covers prompt engineering basics, sampler selection and configuration, and image output options. Includes step-by-step screenshots and example prompts with explanations of each node's function. |
| `get-started/faq.md` | Extensive collection of frequently asked questions addressing common issues like blank outputs, node connection errors, and model loading problems. Includes troubleshooting decision trees and solutions for version compatibility issues. Contains sections on performance optimization and memory management. |

---

## 4. File Catalog – Interface Guides

| File | Purpose |
|------|---------|
| `interface/navigation.md` | Detailed guide to ComfyUI's canvas navigation system, including keyboard shortcuts for panning and zooming, quick-search functionality for finding nodes, and mini-map usage for complex workflows. Includes node organization techniques and workspace navigation best practices. |
| `interface/settings.md` | Complete reference for ComfyUI's configuration options, including model directory paths, cache size management, and performance settings. Covers theme customization, auto-save preferences, and advanced GPU memory allocation options. Includes instructions for editing the configuration file directly. |
| `interface/workspace.md` | Advanced guide to workspace management, including techniques for layering multiple workflows, creating node groups for better organization, and customizing workspace backgrounds. Covers workflow versioning, template creation, and export/import functionality for sharing complex graphs. |

---

## 5. File Catalog – Tutorials

| File | Level | What you build |
|------|-------|----------------|
| `tutorials/basic-workflows.md` | Beginner | Step-by-step tutorials for essential workflows: text-to-image generation with different models, ControlNet implementation with pose/depth/canny edge detection, and batch rendering for multiple variations. Includes detailed explanations of each node's parameters and how they affect the final output. |
| `tutorials/advanced-workflows.md` | Intermediate–advanced | Complex workflow tutorials covering LoRA model mixing techniques, conditional branching based on image analysis, and chaining multiple API nodes for sophisticated generation pipelines. Includes optimization strategies for complex workflows and techniques for dynamic parameter adjustment. |
| `tutorials/custom-nodes.md` | Developer | Comprehensive developer guide for creating custom ComfyUI nodes. Includes Python boilerplate code, node registration process, input/output socket configuration, and UI element creation. Covers best practices for error handling, performance optimization, and compatibility with the core ComfyUI system. |

---

## 6. API Reference – Image Nodes

### 6.1 BFL (Flux-Pro Ultra)

| Path | Description |
|------|-------------|
| `built-in-nodes/api-node/image/bfl/flux-pro-ultra-image.md` | Complete documentation for the Flux-Pro Ultra image generation API. Includes detailed installation instructions for the BFL client, comprehensive parameter tables with value ranges and defaults, example workflow graphs with annotations, and troubleshooting guide for latency and connection issues. Contains API key setup instructions and usage quota information. |

### 6.2 Ideogram

| Version file | Highlights |
|--------------|------------|
| `ideogram-v1.md` | Documentation for Ideogram's legacy model with simple prompt interface. Covers basic text-to-image functionality, parameter limitations, and example prompts. Includes historical context and comparison with newer versions. |
| `ideogram-v2.md` | Detailed guide to Ideogram V2, which introduces aspect ratio controls and magic-prompt enhancement features. Includes parameter tables, example workflows, and techniques for optimizing prompt results with the enhanced model. |
| `ideogram-v3.md` | Comprehensive documentation for Ideogram V3, covering both text-to-image and in-painting capabilities. Details seed control mechanisms, multi-image generation (up to 10 per API call), and advanced prompt engineering techniques specific to V3. Includes performance benchmarks and quality comparison examples. |

### 6.3 Luma AI

| Path | Node type | Notes |
|------|-----------|-------|
| `luma-text-to-image.md` | Text → Image | Detailed guide to Luma's text-to-image generation capabilities. Covers reference image integration, concept prompt techniques, and style control parameters. Includes examples of effective prompt structures and parameter combinations for different artistic styles. |
| `luma-image-to-image.md` | Image → Image | Comprehensive documentation of Luma's image-to-image transformation node. Explains the `image_weight` slider functionality for balancing between source image preservation and creative reinterpretation. Includes examples of different weight settings and their effects. |
| `luma-reference.md` | Helper node | Detailed explanation of the Luma Reference helper node, which encapsulates an image and weight parameter into a reusable "Luma Ref" object. Covers integration with other Luma nodes, parameter inheritance, and techniques for using multiple reference images in complex workflows. |

### 6.4 Recraft V3 Suite

| Path | What it does |
|------|--------------|
| `recraft-text-to-image.md` | Comprehensive guide to Recraft's text-to-image generation with multiple style options. Includes detailed parameter explanations, prompt engineering techniques specific to Recraft, and examples of different style presets and their results. |
| `recraft-image-to-image.md` | Detailed documentation of Recraft's image transformation capabilities, focusing on the strength slider for controlling the balance between input preservation and stylistic changes. Includes examples of different strength settings and their effects on various input images. |
| `recraft-image-inpainting.md` | Complete guide to Recraft's mask-based region repair and regeneration. Covers mask creation techniques, parameter adjustments for seamless integration, and strategies for effective inpainting across different image types. |
| `recraft-text-to-vector.md` | Detailed explanation of Recraft's text-to-SVG vector generation. Includes prompt optimization for vector output, connection instructions for the `save-svg` node, and techniques for creating clean, scalable vector graphics from text descriptions. |
| `recraft-vectorize-image.md` | Comprehensive documentation of Recraft's raster-to-SVG tracing capabilities. Covers detail level adjustment, color quantization options, and optimization techniques for different types of input images. |
| `recraft-color-rgb.md` | Detailed guide to creating and manipulating Recraft Color objects from raw RGB values. Includes color theory considerations, parameter ranges, and integration techniques with other Recraft nodes. |
| `recraft-controls.md` | Complete documentation for bundling colors and background options into a unified "controls" object. Covers parameter inheritance, reusability across multiple nodes, and techniques for creating consistent style settings. |
| `recraft-creative-upscale.md` | Comprehensive guide to Recraft's artistic upscaling capabilities. Explains the creative reinterpretation process, resolution limits, and techniques for enhancing details while maintaining artistic coherence. |
| `recraft-crisp-upscale.md` | Detailed documentation of Recraft's detail-preserving upscaling. Covers resolution parameters, artifact reduction techniques, and comparison with creative upscaling for different image types. |
| `recraft-remove-background.md` | Complete guide to Recraft's automatic matting and background removal. Explains the output format (mask + transparent image), edge refinement options, and techniques for handling complex foregrounds. |
| `recraft-replace-background.md` | Comprehensive documentation of Recraft's background replacement functionality. Covers prompt engineering for background generation, foreground integration parameters, and lighting consistency techniques. |
| `recraft-style-realistic-image.md` | Detailed guide to Recraft's realistic image style preset. Includes parameter modifications specific to realistic rendering, example prompts, and techniques for achieving photorealistic results. |
| `recraft-style-digital-illustration.md` | Complete documentation of Recraft's digital illustration style preset. Covers illustration-specific parameters, color palette considerations, and techniques for achieving different illustration styles. |
| `recraft-style-logo-raster.md` | Comprehensive guide to Recraft's logo raster style preset. Explains parameters for creating effective logo designs, considerations for brand identity, and techniques for generating commercially viable logo concepts. |
| `save-svg.md` | Detailed utility documentation for writing SVG data to disk. Covers file naming conventions, output directory structure (`output/svg/`), and integration with Recraft's vector-generating nodes. Includes SVG post-processing options and viewer recommendations. |

---

## 7. API Reference – Video Nodes

| Path | Provider | Function |
|------|----------|----------|
| `google-veo2-video.md` | Google Veo 2 | Comprehensive documentation of Google's Veo 2 text-to-video generation API. Covers prompt engineering for video content, duration options (4-16 seconds), output format specifications, and the polling status endpoint for monitoring generation progress. Includes examples of effective video prompts and parameter combinations. |
| `kling-camera-control-i2v.md` | Kwai VGI / Kling | Detailed guide to Kwai's Kling image-to-video conversion system (kling-v1-5). Focuses on camera path control parameters for creating dynamic 5-second videos from static images. Includes documentation of camera movement types, transition smoothness settings, and techniques for creating cinematic effects from still images. |
| `runway-gen2-video.md` | Runway | Complete documentation of Runway's Gen-2 video generation system. Covers text-to-video and image-to-video capabilities, motion strength controls, and style transfer options. Includes examples of different motion types and techniques for achieving smooth transitions. |
| `pika-labs-video.md` | Pika Labs | Detailed guide to Pika Labs' video generation API. Explains the different model versions (v1.0, v1.1), prompt engineering for video content, and advanced parameters for controlling motion and style. Includes examples of effective prompts and parameter combinations. |
| `stability-video.md` | Stability AI | Comprehensive documentation of Stability AI's video generation system. Covers both text-to-video and image-to-video capabilities, motion controls, and style transfer options. Includes examples of different motion types and techniques for achieving smooth transitions. |


---

## 8. Cross-Reference Shortcuts

• Most **API nodes** rely on concepts from `essentials/core-concepts.md` → read this document first for a thorough understanding of the underlying principles.  
• The **Recraft** colour and control helper nodes are extensively used in every Recraft generation tutorial found in `tutorials/advanced-workflows.md`. These helper nodes are essential for creating consistent and reusable parameter sets.  
• For saving SVG vector graphics, connect the output of either `recraft-text-to-vector.md` or `recraft-vectorize-image.md` to the input of `save-svg.md`. This workflow is documented in detail in the respective node documentation.

---

## 9. Version & Compatibility

* Documentation set version 1.0 — generated 2025-05-10  
* Compatible with **ComfyUI 1.3.x** and API-Node bundle 2025-05-01.
* All node documentation reflects the latest API endpoints and parameter sets as of the generation date.

---

### Need Help?

If you encounter any issues or have questions about the documentation, please open an issue in the official documentation repository or join the **#support** channel on the ComfyUI Discord server for community assistance.  
Happy noodling with ComfyUI! 🖇️

