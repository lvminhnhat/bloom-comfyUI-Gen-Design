# Development Directory Documentation

This directory contains documentation for **work-in-progress** (alpha/experimental) nodes that are not yet part of the public-stable documentation. Each Markdown file documents a Built-in ComfyUI Node under active development.

> ⚠️ API and file names may change without notice - please report any outdated information via issues/PRs.

## Directory Structure

Development/
├── README.md                  ← Main development documentation
├── api-node/
│   ├── image/
│   │   ├── bfl/
│   │   │   └── flux-pro-ultra-image.md
│   │   ├── ideogram/
│   │   │   ├── ideogram-v1.md
│   │   │   ├── ideogram-v2.md
│   │   │   └── ideogram-v3.md
│   │   ├── luma/
│   │   │   ├── luma-text-to-image.md
│   │   │   ├── luma-image-to-image.md
│   │   │   └── luma-reference.md
│   │   ├── openai/
│   │   │   ├── openai-dalle2.md
│   │   │   ├── openai-dalle3.md
│   │   │   └── openai-gpt-image1.md
│   │   └── recraft/
│   │       ├── recraft-text-to-image.md
│   │       ├── recraft-image-to-image.md
│   │       ├── recraft-image-inpainting.md
│   │       ├── recraft-text-to-vector.md
│   │       ├── recraft-vectorize-image.md
│   │       ├── recraft-color-rgb.md
│   │       ├── recraft-controls.md
│   │       ├── recraft-creative-upscale.md
│   │       ├── recraft-crisp-upscale.md
│   │       ├── recraft-remove-background.md
│   │       ├── recraft-replace-background.md
│   │       ├── recraft-style-realistic-image.md
│   │       ├── recraft-style-digital-illustration.md
│   │       ├── recraft-style-logo-raster.md
│   │       └── save-svg.md
│   └── video/
│       ├── minimax/
│       │   └── minimax-video.md
│       └── future/
│           └── README.md
├── core/
│   ├── concepts/
│   │   ├── node-theory.md
│   │   ├── execution-graphs.md
│   │   └── io-types.md
│   ├── get-started/
│   │   ├── installation.md
│   │   ├── first-steps.md
│   │   └── faq.md
│   ├── installation/
│   │   ├── windows.md
│   │   ├── macos.md
│   │   └── linux.md
│   ├── interface/
│   │   ├── toolbar.md
│   │   ├── inspector.md
│   │   └── node-search.md
│   └── tutorials/
│       ├── bfl-tutorial.md
│       ├── ideogram-tutorial.md
│       ├── luma-tutorial.md
│       ├── openai-tutorial.md
│       └── recraft-tutorial.md
└── guidelines/
    ├── documentation-standards.md
    ├── version-control.md
    └── local-development.md

# Development Documentation Overview

This section provides a comprehensive guide to all documentation files in the Development directory, organized by category and purpose.

## Guidelines Documentation
The guidelines section contains essential policy and procedure documents:

- **documentation-standards.md**: A detailed style guide covering formatting rules, documentation structure, and writing conventions for all project documentation. Includes examples of proper formatting for code blocks, tables, and API references.

- **version-control.md**: Comprehensive guide to Git workflow practices, including branching strategies, commit message formatting, and code review procedures. Explains how to maintain clean commit history and handle merge conflicts.

- **local-development.md**: Step-by-step instructions for setting up a development environment, including required dependencies, configuration settings, and testing procedures. Covers environment variables and local debugging tools.

## API Node Documentation

### Image Generation Nodes

#### BFL Integration
- **flux-pro-ultra-image.md**: Complete documentation for the BFL API image generator node, including API authentication, parameter configuration, and example workflows. Details error handling and rate limiting considerations.

#### Ideogram Integration
- **ideogram-v1.md**: Documentation for the original Ideogram text-to-image endpoint, covering basic prompt engineering and parameter settings.
- **ideogram-v2.md**: Enhanced documentation for V2, focusing on new features like aspect ratio control and resolution options.
- **ideogram-v3.md**: Comprehensive guide to V3's capabilities, including in-painting workflows and advanced generation techniques.

#### Luma AI Integration
- **luma-text-to-image.md**: Guide to text-to-image generation using Luma AI models, including model selection and prompt optimization.
- **luma-image-to-image.md**: Documentation for image transformation workflows, explaining the image weight parameter and its effects.
- **luma-reference.md**: Technical reference for the Luma reference object system, used in complex image manipulation workflows.

#### OpenAI Integration
- **openai-dalle2.md**: Complete guide to DALL·E 2 integration, covering both generation and editing capabilities.
- **openai-dalle3.md**: Updated documentation for DALL·E 3, including new features and improved quality settings.
- **openai-gpt-image1.md**: Experimental documentation for the GPT-4 Vision API integration.

#### Recraft Integration
The Recraft section contains extensive documentation for various image manipulation tools:

- **recraft-text-to-image.md**: Main documentation for text-to-image generation with style and control options.
- **recraft-image-to-image.md**: Guide to image transformation workflows with strength control.
- **recraft-image-inpainting.md**: Documentation for mask-based in-painting operations.
- **recraft-text-to-vector.md**: Guide to generating SVG vectors from text prompts.
- **recraft-vectorize-image.md**: Documentation for converting raster images to vector format.
- **recraft-color-rgb.md**: Reference for color object creation and manipulation.
- **recraft-controls.md**: Guide to combining multiple control parameters for complex operations.
- **recraft-creative-upscale.md**: Documentation for AI-powered image upscaling with creative modifications.
- **recraft-crisp-upscale.md**: Guide to high-quality image upscaling without creative changes.
- **recraft-remove-background.md**: Documentation for automatic background removal.
- **recraft-replace-background.md**: Guide to background replacement with AI-generated content.
- **recraft-style-*.md**: Individual documentation for different style presets (realistic, digital illustration, logo raster).

## Interface Documentation
- **toolbar.md**: Detailed explanation of the main toolbar interface, including all buttons and quick actions.
- **inspector.md**: Comprehensive guide to the node inspector panel and its configuration options.
- **node-search.md**: Documentation for the node search functionality, including filtering and keyboard shortcuts.

## Tutorial Documentation
- **bfl-tutorial.md**: Step-by-step guide to creating image generation workflows using BFL.
- **ideogram-tutorial.md**: Practical examples of Ideogram node implementation.
- **luma-tutorial.md**: Complete tutorial covering both text-to-image and image-to-image workflows.
- **openai-tutorial.md**: Guide to building complex generation and editing chains with DALL·E.
- **recraft-tutorial.md**: Comprehensive tutorial for image and vector creation workflows.

Note: This documentation is continuously updated. New files should be added following the established hierarchy and formatting standards.
