
# Day 9 — How AI Images Are Generated: CLIP, Diffusion, and DALL-E 2

## Topics Covered

* CLIP — connecting text and images in a shared vector space
* Diffusion models and DDPM — generating images from noise
* Vector fields and the data manifold
* DDIM — making diffusion fast enough for real use
* DALL-E 2 — combining CLIP + diffusion into one pipeline
* Conditioning, Classifier-Free Guidance (CFG), and negative prompts

## Sources

* Guest video by Welch Labs — *But how do AI images and videos actually work?* (3Blue1Brown channel)

## Key Concept: CLIP (Contrastive Language-Image Pretraining)

Before a model can generate an image from a text prompt, it needs to "understand" how words relate to pictures. OpenAI's CLIP (Feb 2021) solves this using two neural networks working together: a **Text Encoder** (turns words into vectors) and an **Image Encoder** (turns images into vectors) — conceptually similar to the embeddings from Day 5, just across two different modalities instead of one.

**Training CLIP**
CLIP trains on millions of internet image-caption pairs. The goal: make the text vector for "a cute golden retriever" point in nearly the same direction as the image vector of an actual golden retriever. It uses a **Contrastive Loss** — calculating cosine similarity between image-text pairs, maximizing alignment (0° angle) for correct pairs while pushing mismatched pairs toward perpendicular/opposite directions.

## Key Concept: The Shared Embedding Space

CLIP's core idea is a **Shared Embedding Space** — a high-dimensional landscape where images and text are mapped together, and geometric closeness represents semantic similarity (directions carrying meaning — same idea introduced in Day 5's embeddings, but now spanning two modalities). Because it's a real vector space, you can do vector arithmetic: `(image of Man with Hat) − (image of Man) ≈ (text vector for "hat")`. CLIP acts as the bridge that turns a text prompt into a coordinate in this shared space, which the image generator then targets.

## Key Concept: Diffusion Models & DDPM

CLIP can translate meaning, but it can't generate pixels — that's diffusion's job, popularized by the 2020 **DDPM** (Denoising Diffusion Probabilistic Models) paper. Training happens in two phases:

- **Forward process (destruction)** — take a clean image and gradually add Gaussian noise over hundreds of steps until it's unrecognizable static.
- **Backward process (rebuilding)** — train a neural network to look at a noisy image and clean it up.

**The mathematical shortcut**
Rather than learning to denoise one tiny step at a time (inefficient), DDPM's key insight is a closed-form equation that computes any noisy step instantly. The network is trained to predict the *total* noise added to a clean image, so it can subtract that noise in one shot to reveal a cleaner version.

## Key Concept: Vector Fields & the Data Manifold

Picture the space of all possible pixel combinations as terrain: realistic images (faces, landscapes) sit in deep valleys — the **data manifold** — while pure noise sits on chaotic mountain peaks. Generation starts at a random peak (random noise). The model learns a **vector field** — like a map of wind currents — where every point in pixel space points toward the nearest realistic image. Following these currents (i.e., following probability gradients) blows the noise down into the valleys, gradually forming a coherent image.

## Key Concept: DDIM — The Deterministic Shortcut

Original DDPM denoising is stochastic — at each step it predicts noise, subtracts it, then adds a bit of new random noise back in (like a drunkard zigzagging downhill), requiring ~1,000 steps per image. **DDIM** (late 2020) reformulates this as a deterministic path — an Ordinary Differential Equation (smooth line) instead of a Stochastic Differential Equation (random walk). A smooth path allows larger steps via solver techniques, cutting generation from 1,000 steps down to just 20-50 — fast enough to run on consumer hardware in seconds.

## Key Concept: DALL-E 2 — Putting It All Together

DALL-E 2 chains these pieces into one pipeline:

1. **CLIP (the conductor)** — encodes your text prompt into a text embedding vector
2. **The Prior** — a separate network maps that text embedding to a corresponding CLIP *image* embedding
3. **The Decoder (Diffusion, using DDIM)** — takes that image embedding and turns it into actual high-resolution pixels, generating a new image out of pure noise

## Key Concept: Conditioning

A plain diffusion model just generates a random realistic image. To force it to generate *your* prompt, the model uses **conditioning** — feeding the CLIP text embedding directly into the diffusion network's layers (typically via cross-attention, a mechanism related to the attention block from Day 4-5). Geometrically, this tilts the vector field: instead of wind blowing toward any realistic image, it blows specifically toward images matching the prompt.

## Key Concept: Classifier-Free Guidance (CFG)

If conditioning alone is too weak, the model may ignore parts of the prompt. **CFG** fixes this by running two calculations at every step: a **conditioned step** (wind direction with the prompt) and an **unconditioned step** (wind direction with a blank prompt). The difference between these two vectors points directly toward the unique details of the prompt, and amplifying that difference strengthens prompt adherence.

## Key Concept: Negative Prompts

Negative prompts are a direct application of CFG. Instead of leaving the unconditioned branch blank, it's conditioned on the *negative* prompt (e.g., "ugly, blurry, low resolution"). The positive branch pulls the image toward what you want; the negative branch pulls toward what you don't want. Subtracting the negative branch's direction pushes the final image away from those bad qualities.

## Takeaway

This day connected embeddings (Day 5) and attention (Day 4-5) to a completely different modality — CLIP builds a shared space where text and images are geometrically comparable, and diffusion models learn to "walk" from noise toward realistic images guided by a probability-gradient vector field. DDIM makes that walk practical, and CFG/negative prompts are just clever uses of the conditioned-vs-unconditioned difference vector to steer generation more precisely.

## Questions I still have

* How is the Prior network in DALL-E 2 actually trained — what loss function maps a text embedding to a corresponding image embedding?

---

*Part of my **AI/ML learning journey** — Day 9*
