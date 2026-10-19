# ComfyUI Workflow Skill

> Create ComfyUI workflow JSON files from natural language requests.

**No API fees or backend required. Describe what you want, generate workflow JSON, then load it in ComfyUI.**

[![Linux.do](https://img.shields.io/badge/Linux.do-Discussion-blue)](https://linux.do/t/topic/1896794)

## Examples

### Install the skill
![Skill installation](images/%E5%AE%89%E8%A3%85skills.png)

### Generate a workflow, load it in ComfyUI, and create media
![Image-to-video workflow generation](images/%E7%94%9F%E5%9B%BE%E8%BD%AC%E8%A7%86%E9%A2%91workflow.png)
![Image-to-video workflow](images/%E5%9B%BE%E7%94%9F%E8%A7%86%E9%A2%91%E6%B5%81%E7%A8%8B.png)

### Generated images and video
![Generated image](images/%E7%94%9F%E6%88%90%E7%9A%84%E5%9B%BE%E7%89%87.jpg)
![Generated result](images/%E8%BF%90%E8%A1%8C%E7%BB%93%E6%9E%9C.png)

https://github.com/user-attachments/assets/831e8453-d3fa-41ad-99f6-39b13ce498d0

### Combine and update workflows
![Combined workflows](images/%E5%A4%9A%E4%B8%AAworkflow%E5%90%88%E5%B9%B6%E6%9B%B4%E6%96%B0.png)

### Motion transfer

Source video:

https://github.com/user-attachments/assets/8a0affa3-ff07-449e-9ec5-c6ca8c37ba0f

Result (rendered at lower resolution due to VRAM limits):

https://github.com/user-attachments/assets/5420d74e-18eb-4a72-8819-3138d7353edf

![Motion transfer workflow](images/%E5%8A%A8%E4%BD%9C%E8%BF%81%E7%A7%BBworkflow.png)
![Motion transfer pipeline](images/%E5%8A%A8%E4%BD%9C%E8%BF%81%E7%A7%BB%E6%B5%81%E7%A8%8B.png)
![Motion transfer fix](images/%E5%8A%A8%E4%BD%9C%E8%BF%81%E7%A7%BB%E4%BF%AE%E5%A4%8D.png)
![Restore source audio](images/%E5%8A%A8%E4%BD%9C%E8%BF%81%E7%A7%BB%E9%9F%B3%E9%A2%91%E8%BF%98%E5%8E%9F.png)

## What it does

This Claude Code skill creates ComfyUI workflow JSON through conversation. Describe the result you want, and the skill selects and customizes a workflow template. You do not need to connect nodes manually in the ComfyUI editor.

The skill **generates workflow files; it does not connect to or run a ComfyUI server**. Load the generated JSON in ComfyUI and start the workflow there.

## Features

- **34 workflow templates** for popular models and tasks
- **360+ node definitions** extracted from ComfyUI source, including input types and value ranges
- **Model download metadata** in the native `models` field so ComfyUI can offer missing models when a workflow is imported
- **Optional LLM integration** through comfyui_LLM_party (OpenAI, Claude, Gemini, Ollama, DeepSeek, and compatible APIs)
- **On-demand node references** organized into 42 category files

## Installation

### Requirements

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code)
- Git

### Recommended: clone this fork into the Claude Code skills directory

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/remiehneppo/comfyui-workflow-skill.git ~/.claude/skills/comfyui-workflow
```

### Alternative: clone and symlink

Use this option to keep a working copy in `~/codes` and update it with Git:

```bash
git clone https://github.com/remiehneppo/comfyui-workflow-skill.git ~/codes/comfyui-workflow-skill
mkdir -p ~/.claude/skills
ln -s ~/codes/comfyui-workflow-skill ~/.claude/skills/comfyui-workflow
```

### Verify the installation

```bash
ls ~/.claude/skills/comfyui-workflow/SKILL.md
```

If the command prints the file path, Claude Code can read the skill from that location.

### Update

For a direct clone:

```bash
cd ~/.claude/skills/comfyui-workflow
git pull
```

For a symlink installation:

```bash
cd ~/codes/comfyui-workflow-skill
git pull
```

### Uninstall

Remove the installed directory or symlink:

```bash
rm -r ~/.claude/skills/comfyui-workflow
```

If you also want to remove the cloned working copy, delete `~/codes/comfyui-workflow-skill`.

## Usage

Describe the workflow you need in Claude Code. For example:

```text
Create a FLUX text-to-image workflow.
Make a Wan 2.2 image-to-video workflow with camera movement.
Create an SDXL inpainting workflow.
Use an LLM to write a script, then create character images and a video.
```

You can also invoke the skill with its slash command:

```text
/comfyui-workflow Create an SD3 text-to-image workflow
```

### Run a generated workflow

1. Save the generated workflow JSON in the current directory when requested.
2. In ComfyUI, click **Load** or drag the JSON file into the interface.
3. If models are missing, use ComfyUI download prompt or install the required files.
4. Click **Queue** to run the workflow.

## Example workflows

- [FLUX text-to-image to Wan 2.2 image-to-video](flux-txt2img-wan22-img2vid.json)
- [Wan 2.2 motion transfer](wan22-motion-transfer.json)

## Optional: install LLM integration

Workflows that use LLM nodes for script writing, character descriptions, or prompt enhancement require the [comfyui_LLM_party custom node package](https://github.com/heshengtao/comfyui_LLM_party).

In your ComfyUI installation:

```bash
cd ComfyUI/custom_nodes
git clone https://github.com/heshengtao/comfyui_LLM_party.git
pip install -r comfyui_LLM_party/requirements.txt
```

Supported providers include OpenAI, Claude, Gemini, DeepSeek, Ollama, and OpenAI-compatible APIs.

## Included templates

### Image generation and editing

| Template | File | Description |
|---|---|---|
| SD 1.5 text-to-image | `sd15-txt2img.json` | Basic SD 1.5 image generation |
| SD 1.5 image-to-image | `sd15-img2img.json` | Transform an input image |
| SD 1.5 + LoRA | `sd15-lora.json` | Load a LoRA with SD 1.5 |
| SD 1.5 + ControlNet | `sd15-controlnet.json` | Guide generation with ControlNet |
| SD 1.5 inpainting | `sd15-inpaint.json` | Edit a selected image region |
| SDXL text-to-image | `sdxl-txt2img.json` | Basic SDXL image generation |
| SDXL image-to-image | `sdxl-img2img.json` | Transform an input image |
| SDXL + LoRA | `sdxl-lora.json` | Load a LoRA with SDXL |
| SDXL + ControlNet | `sdxl-controlnet.json` | Guide generation with ControlNet |
| SDXL inpainting | `sdxl-inpaint.json` | Edit a selected image region |
| SD3 text-to-image | `sd3-txt2img.json` | SD3 with TripleCLIPLoader |
| FLUX text-to-image | `flux-txt2img.json` | FLUX.1 image generation |
| FLUX image-to-image | `flux-img2img.json` | Transform an input image |
| FLUX + LoRA | `flux-lora.json` | Load a LoRA with FLUX.1 |

### Video generation

| Template | File | Description |
|---|---|---|
| Wan 2.2 text-to-video | `wan22-txt2vid.json` | 832x480, 81 frames |
| Wan 2.2 image-to-video | `wan22-img2vid.json` | Image-conditioned video |
| Wan 2.2 first/last frame | `wan22-first-last.json` | Generate video between two frames |
| Wan 2.2 Fun Control | `wan22-fun-control.json` | Control video with a reference image |
| Wan 2.2 camera control | `wan22-camera.json` | Apply camera motion |
| HunyuanVideo text-to-video | `hunyuan-video.json` | HunyuanVideo generation |
| HunyuanVideo image-to-video | `hunyuan-video-i2v.json` | Image-conditioned HunyuanVideo |
| LTXV text-to-video | `ltxv-txt2vid.json` | 768x512, 97 frames |
| LTXV image-to-video | `ltxv-img2vid.json` | Image-conditioned LTXV |
| Mochi text-to-video | `mochi-txt2vid.json` | 848x480 video |
| Cosmos text-to-video | `cosmos-txt2vid.json` | 1280x704 video |
| Cosmos image-to-video | `cosmos-img2vid.json` | Image-conditioned Cosmos |

### Audio, 3D, and other

| Template | File | Description |
|---|---|---|
| Image upscaling | `upscale-model.json` | RealESRGAN and similar models |
| Stable Audio | `stable-audio.json` | Audio generation (47 seconds) |
| Hunyuan3D v2 | `hunyuan3d-v2.json` | Create a 3D model from an image |
| Stable Cascade | `stable-cascade.json` | Two-stage image generation |

### LLM workflows

| Template | File | Description |
|---|---|---|
| LLM chat (API) | `comfyui_LLM_party/llm-chat-api.json` | Chat through an API provider |
| LLM chat (Ollama) | `comfyui_LLM_party/llm-chat-ollama.json` | Chat with a local Ollama model |
| LLM prompt enhancement | `comfyui_LLM_party/llm-prompt-enhance.json` | Expand a prompt for FLUX |
| LLM script-to-video pipeline | `comfyui_LLM_party/llm-script-to-video.json` | Script, character descriptions, and storyboard |

## Model downloads

Templates include ComfyUI native `models` metadata. When you load a workflow, ComfyUI can detect missing models and offer download options.

A model entry looks like this:

```json
{
  "models": [
    {
      "name": "flux1-dev.safetensors",
      "url": "https://huggingface.co/black-forest-labs/FLUX.1-dev/resolve/main/flux1-dev.safetensors",
      "directory": "diffusion_models"
    }
  ]
}
```

Model downloads use Hugging Face or CivitAI sources where available.

## Repository layout

```text
comfyui-workflow-skill/
├── SKILL.md
├── README.md
├── flux-txt2img-wan22-img2vid.json
├── wan22-motion-transfer.json
├── images/
├── references/
│   ├── nodes/
│   ├── node-registry-additions.md
│   ├── workflow-format.md
│   └── common-workflows.md
└── templates/
    └── comfyui_LLM_party/
```

## Troubleshooting

### Missing nodes after loading a workflow

Some workflows use custom nodes such as LLM Party. Install the matching custom node package in ComfyUI, restart ComfyUI, then load the workflow again.

### Missing models

ComfyUI may offer to download missing models when you load a workflow. If no prompt appears, follow the model link and place the file in the matching subdirectory under `ComfyUI/models/`.

### `widgets_values` errors

A `Value not in list` error usually means a widget value has the wrong type or falls outside the allowed range. Check that:

- COMBO values match an allowed option exactly.
- Seed fields use the expected value, including `randomize` when required.
- FLOAT and INT values are within their minimum and maximum limits.

## Contributing

Contributions to this fork are welcome. Open issues or pull requests at:

https://github.com/remiehneppo/comfyui-workflow-skill

Useful contributions include workflow templates, support for more custom nodes, fixes for generated workflow JSON, and documentation improvements.

## License

MIT
