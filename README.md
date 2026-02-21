# cat-scene-clarity

A scalar function that evaluates the scene clarity surrounding a cat in a photograph — the degree to which the background and environment yield to the cat, allowing it to stand as the unambiguous subject of the image.

## Overview

Not every photograph of a cat is a clear photograph of a cat. The world around the animal matters: a cluttered background competes for attention, camouflaging colors dissolve the cat into its setting, and obstructing objects fragment its form. **cat-scene-clarity** measures whether the scene has done its job — whether it has receded, contrasted, and cleared the way for the cat to be seen.

The function returns a single scalar score between **0** and **1**:

| Score Range | Interpretation |
|---|---|
| **0.8 – 1.0** | The scene fully cooperates. The background is clean, the cat is visually striking against its surroundings, and its body is completely visible. |
| **0.5 – 0.8** | The scene is moderately cooperative. Some clutter, partial blending, or minor obstructions are present, but the cat remains reasonably clear. |
| **0.2 – 0.5** | The scene competes with the cat. Noticeable clutter, visual similarity between the cat and background, or partial occlusion weaken the cat's dominance. |
| **0.0 – 0.2** | The scene fails the cat. Heavy clutter, strong camouflage, or significant obstruction make the cat difficult to distinguish as the subject. |

## Input

The function accepts a single input:

| Field | Type | Required | Description |
|---|---|---|---|
| `image` | `image` | Yes | A photograph containing a cat. The function evaluates the relationship between the cat and everything else in the frame. |

The image is the totality of what the function considers. No metadata, captions, or additional context are used — the image must speak for itself.

## What It Evaluates

The score is derived from three independent evaluations, each targeting a fundamental quality of scene clarity:

### 1. Background Simplicity

Assesses whether the space behind and around the cat is clean, calm, and visually restrained — or cluttered with competing elements.

- **High score:** A solid-colored wall, an expanse of grass, a smooth surface, or an intentionally blurred backdrop. The environment recedes, serving as a quiet canvas.
- **Low score:** Piles of objects, tangled items, busy wallpaper, other animals, bright signage, or chaotic surroundings that fracture the viewer's gaze and force the cat to share attention.

### 2. Subject Distinction

Assesses the visual contrast between the cat and its surroundings — whether the cat is perceptually separable from its environment through differences in color, brightness, or texture.

- **High score:** A white cat on a dark sofa, an orange tabby against green grass, or any scene where strong contrast creates a clear boundary between the cat and the background.
- **Low score:** A gray cat on a gray couch, a tabby in autumn leaves, or a black cat in a dark room — scenes where the cat is absorbed into its setting through similar colors, matching patterns, or low contrast.

### 3. Freedom from Obstruction

Assesses whether the cat's body is fully visible and openly presented to the viewer — or partially hidden behind objects, surfaces, or other elements in the scene.

- **High score:** The cat's entire body is revealed with nothing blocking the view. The scene commits to showing the cat completely.
- **Low score:** The cat is photographed through a fence, peeking from behind furniture, partially buried in blankets, or otherwise obscured by elements that break the line of sight between the viewer and the subject.

## Use-Cases

### Dataset Curation
Filter cat image datasets by scene clarity to select images where the cat is visually unambiguous — useful for training object detection models, building editorial image libraries, or curating online galleries.

### Content Ranking
Prioritize cat photographs for social media feeds, thumbnails, or hero images by surfacing those with the highest scene clarity — ensuring the cat reads instantly at any size.

### Photography Feedback
Evaluate a portfolio of cat photographs to identify patterns in environmental composition. The score reflects not the quality of the cat, but the quality of the choices made around it — helping photographers recognize whether they tend toward clean, cooperative backgrounds or cluttered, competing ones.

### Quality Filtering
Establish minimum scene clarity thresholds for automated pipelines that process cat imagery at scale — rejecting images where clutter, camouflage, or obstruction make the cat ambiguous as the subject.

## Important Notes

- This function evaluates the **scene**, not the cat. It does not measure whether the cat is beautiful, centered, well-lit, or in focus. It measures whether the environment has made room for the cat to be seen.
- The function is designed for images that **contain a cat**. Results on images without a cat are undefined.
- The score reflects three independent dimensions (simplicity, distinction, obstruction) aggregated into a single value. An image could score well on one dimension and poorly on another.