# IIA4XAI — Interactive Installation Art for AI Explainability

**MSc thesis prototype** by Marise van Noordenne  
*IIA4XAI: Interactive Installation Art to increase Non-Expert User Engagement with AI Systems*

An interactive **webcam → machine perception → generative image** pipeline that makes how AI “sees” and imagines visible to non-expert audiences. Built as the technical core of a physical installation: visitors are captured on camera, their image is interpreted by vision-language models, and Stable Diffusion renders what the system “understands.”

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/vannoordenne/static./blob/main/webcam2interrogator2images.ipynb)

---

## What this demonstrates

| Area | Evidence in this repo |
|------|----------------------|
| **Generative AI prototyping** | End-to-end Stable Diffusion pipeline (latent diffusion, schedulers, batch generation) |
| **Python / ML experimentation** | PyTorch, Hugging Face Diffusers & Transformers, CLIP Interrogator |
| **Interactive AI installation design** | Live webcam input, iterative image output, HTML display layer for exhibition |
| **AI explainability & research-through-design** | Makes CLIP-based captioning and text-to-image generation tangible for non-experts |
| **Technical communication** | Documented setup, security hygiene, configurable paths for reproducibility |

---

## Pipeline

```
Webcam capture (webcam.png)
        ↓
CLIP Interrogator  →  natural-language prompt
        ↓
Stable Diffusion v1-4  →  sequence of generated images
        ↓
display.html  →  animated exhibition view
```

1. **`webcam2interrogator2images.ipynb`** — main notebook: model setup, prompt generation, image synthesis.
2. **`display.html`** — cycles through generated frames in `output/imgs/<folder>/` for a live-installation feel.

---

## Tech stack

- **Python** · **PyTorch** · **Jupyter / Google Colab**
- [CLIP Interrogator](https://github.com/pharmapsychotic/clip-interrogator) — image → text prompt
- [Stable Diffusion v1-4](https://huggingface.co/CompVis/stable-diffusion-v1-4) via Hugging Face Diffusers
- [Hugging Face Hub](https://huggingface.co/) — model authentication & downloads
- **HTML / JavaScript** — lightweight display layer

---

## Quick start (Google Colab — recommended)

1. Open the notebook: [**Open in Colab**](https://colab.research.google.com/github/vannoordenne/static./blob/main/webcam2interrogator2images.ipynb)
2. **Runtime → Change runtime type → GPU** (T4 or better)
3. Add a Colab **Secret** named `HF_TOKEN` with a [Hugging Face read token](https://huggingface.co/settings/tokens)  
   - Enable **Read access to gated repos** and accept the [SD v1-4 license](https://huggingface.co/CompVis/stable-diffusion-v1-4)
4. Run the **setup** and **prompt 2 img** cells
5. In **webcam 2 prompt**: click **📸 Capture webcam** when prompted (or set `input_source` to `upload` and pick a photo)

Optional Colab Secrets: `IIA4XAI_OUTPUT_DIR`, `IIA4XAI_PROMPT_FILE` (see `.env.example`).

### Local run

```bash
cp .env.example .env   # set HF_TOKEN locally — never commit .env
```

Then open `webcam2interrogator2images.ipynb` in Jupyter or VS Code. A CUDA GPU is strongly recommended.

### Exhibition display

After generation, open `display.html` in a browser (or serve the repo root locally). It reads frames from `output/imgs/0/image*.png` by default.

---

## Configuration

| Variable | Purpose |
|----------|---------|
| `HF_TOKEN` | Hugging Face token for gated model download |
| `IIA4XAI_OUTPUT_DIR` | Output folder for images and CSV (default: `./output/imgs`) |
| `IIA4XAI_PROMPT_FILE` | Latest prompt text file (default: `./output/prompt.txt`) |

See [`.env.example`](.env.example) and [`SECURITY.md`](SECURITY.md).

---

## Repository structure

```
.
├── webcam2interrogator2images.ipynb   # Main pipeline
├── display.html                       # Exhibition display layer
├── .env.example                       # Configuration template
├── SECURITY.md                        # Credential & sharing guidelines
└── README.md
```

---

## Credits & lineage

This prototype adapts and combines work from:

- [CLIP Interrogator](https://colab.research.google.com/github/pharmapsychotic/clip-interrogator/blob/main/clip_interrogator.ipynb) — pharmapsychotic
- [Stable Diffusion (Diffusers)](https://colab.research.google.com/github/huggingface/notebooks/blob/main/diffusers/stable_diffusion.ipynb) — Hugging Face
- [Diffusion display approach](https://colab.research.google.com/drive/1_kbRZPTjnFgViPrmGcUsaszEdYa8XTpq) — Edan Myer

Original thesis codebase: [vannoordenne/IIA4XAI](https://github.com/vannoordenne/IIA4XAI) (superseded by this cleaned portfolio version).

---

## Security

No API keys or tokens belong in source files. Before sharing, review [`SECURITY.md`](SECURITY.md).

---

## Author

**Marise van Noordenne**  
MSc thesis project · Interactive installation art × AI explainability

> **Note:** This README was drafted with AI assistance for clarity and structure. The thesis, installation concept, and technical prototype are my own work.
