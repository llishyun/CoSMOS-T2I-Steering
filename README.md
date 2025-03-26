# 🧠 Improving Text-to-Image Alignment Using Image Captioning

This project proposes a pipeline to enhance text-to-image (TTI) alignment by comparing user prompts and image captions, then selectively regenerating or editing images to better reflect user intent.

✨ Without retraining any diffusion model, we improve semantic alignment and reduce visual artifacts in generated images.

## 📌 Overview

Most TTI models struggle with complex prompts, multi-object interactions, or fine-grained attributes, leading to:
- ❌ Incomplete object rendering
- ❌ Misalignment between prompt and image
- ❌ Unintended artifacts

We propose an automatic framework that:
1.	Generates an image from a user prompt
2.	Captions the image using BLIP-2
3.	Computes similarity between the prompt and the caption (STS)
4.	Based on similarity score:
    - Regenerates the image entirely (Case 1)
    - Or edits specific regions via inpainting (Case 2)

## 🛠️ Pipeline
<img width="1259" alt="TTI_Alignment_pipeline" src="https://github.com/user-attachments/assets/e26da768-7097-4782-b5c0-4b5c61e551c2" />


## 🧪 Model Components

| Module                     | Model Used                          |
|----------------------------|--------------------------------------|
| Image Generation           | Stable Diffusion XL (with fixed seed) |
| Captioning                 | BLIP-2                               |
| Semantic Similarity        | SentenceTransformer STS model        |
| Image Regeneration (Case 1)| InstructPix2Pix                      |
| Object Masking (Case 2)    | SAM (Segment Anything Model)         |
| Inpainting (Case 2)        | Stable Diffusion Inpainting          |

## 🔍 Case Handling Logic
### Case 1
- Prompt and caption differ significantly (low STS score)	Regenerate image with prompt engineering
- Example Prompt Engineering
  ```
  Prompt:
  "The user prompt was: 'a red sports car on a highway', 
  but the generated image was captioned as: 'a red car in a city street'. 
  Considering the difference, regenerate the image to better reflect the user's intent."
  ```
### Case 2
- Minor mismatches (e.g., incorrect object or attribute) -> identify and inpaint target objects
- Approach1: Attribute-Based Dictionary
  - POS tagging + synonym filtering to extract modified nouns
- Approach2: Relationship-Based Graph
  - Graph-based semantic parsing using tokenization + NER (inspired by SHINE)


## 📈 Evaluation
To measure improvement over baseline generations, we use:
`CLIP Score: Semantic similarity between prompt and image`


## 📦 Dataset
`User Prompts: PartiPrompts`
→ A rich set of prompts for diverse and challenging image generation


# 📁 Project Structure (updating..)
```
│
├── captioning/         # BLIP-2-based captioning module
├── generation/         # SDXL & InstructPix2Pix generation pipeline
├── similarity/         # STS scoring logic
├── masking/            # Object detection & SAM masking
├── inpainting/         # Stable Diffusion inpainting handler
├── evaluation/         # CLIP & FID evaluation scripts
└── README.md
```


# 🔧 Setup Instructions (Colab)
```
!pip install diffusers transformers accelerate safetensors invisible_watermark
!pip install sentence-transformers torchvision
```
