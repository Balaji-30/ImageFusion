# ImageFusion

ImageFusion is a fullstack web application that combines multiple user-provided images (like people, backgrounds, and objects) into a single, coherent scene using AI. It uses OpenAI’s DALL·E for generation and CLIP for output evaluation.

<br>

<p align="center">
  <img src="./assets/ImageFusionCropped.PNG" alt="ImageFusion Banner">
</p>

<br>

## Project Overview and Motivation

**ImageFusion** is an AI-driven image composition tool that combines multiple user-provided images into a single cohesive scene.  
### 🔹 Users provide:
- One or more **person** images
- A **background** image
- A **prop** image
- An optional **instructional prompt**

### 🔹 The system then:
1. **Extracts visual descriptions** of each input using OpenAI’s vision-language model.
2. **Combines them into a single scene prompt** tailored for image generation.
3. **Generates a new image** using DALL·E 3 that realistically blends people, background, and props.
4. **Evaluates the result** using **CLIP-based similarity scoring**, comparing the final image with the inputs and prompt to assess semantic alignment and trustworthiness.

---

### Motivation: Why Trust Matters in ImageFusion

In many real-world applications—advertising, media generation, educational content—image generation systems must **faithfully represent** user inputs without introducing hallucinations, distortions, or bias.

**Potential trust issues:**
- Generated outputs ignoring key user inputs (e.g., missing people or wrong backgrounds).
- Inaccurate representation of original people or props.
- Unreliable or inconsistent output quality.

Because users trust the system to preserve the intent and structure of the input images, **trustworthiness** is essential for adoption and usability.

---

### Defining Trust Quantitatively
We establish a quantitative measure of trustworthiness by assessing:

- The degree to which the generated image semantically corresponds with both the input prompt and the provided images.
To evaluate this alignment, we utilize a CLIP-based similarity score, which compares the summarized prompt (describing the intended scene) with the generated image.
A higher score indicates stronger semantic alignment, suggesting greater trustworthiness of the output.
This metric, commonly referred to as the CLIP similarity score or Image-Text Relevance Retrieval Score (IRRS), measures how closely the generated image matches the provided text description.

---

## Implementation of Trust-Enhancing Modifications

### Original System (Baseline)
- Images and prompts were sent to OpenAI's API without structured summarization.
- Outputs were sometimes misaligned or hallucinated.
- Trust was compromised due to under-specified prompts.
<br>  

### Trust-Enhancing Changes in ImageFusion
<br>

| Area               | Modification Implemented                                                                 |
|--------------------|-------------------------------------------------------------------------------------------|
| **Prompt Design**  | Created a structured summarization strategy focusing on visible human attributes, backgrounds, and objects without inferring missing details. |
| **Prompt Engineering** | Strict instructions for "continuous single-scene generation with natural interactions" (no panels, no split layouts). |
| **Model Usage**    | Integrated OpenAI Vision APIs thoughtfully, crafting prompts that tightly bind all user elements together. |
| **Evaluation Metric** | Used CLIP (Contrastive Language–Image Pretraining) model to score the alignment between prompt and output. |
<br>

- With a more refined and carefully structured system prompt, the overall prompt quality significantly improved, leading to an even higher IRRS score. We were able to achieve an IRRS score of approximately 39, showcasing a substantial improvement in semantic alignment and image relevance. This indicates that thoughtful prompt engineering plays a critical role in enhancing the final output quality and model performance when generating images based on multi-image instructions.
<br>

```python
summarization_prompt = (
    "For each image: "
    "If it contains a person,you have to mention the ethnicity or skin tone, then describe the person's visible characteristics (e.g., hair color, gender, ethnicity) in about 30 words, ignoring the background. "
    "If it contains only a background, describe the scene. "
    "If it contains only an object, describe the object's visual details. "
    "Do not infer or imagine missing details. Only describe what is explicitly visible."

    "Then, combine the descriptions of all images into the following user instruction for the prompt: "
    f"\"{body.prompt.strip()}\" "
    "Create a summarized prompt that will be used as input to DALL-E 3, so prioritize clarity, key details, and visual faithfulness."
    "The combined prompt must create a single continuous scene, not separate sections. "
        )
prompt=merged_prompt + "Strictly avoid introducing extra characters, unrelated objects, or changing the original elements.Depict all individuals together naturally, interacting in the same scene, avoiding separate frames or isolated" "placement.Capture the scene in highly detailed photorealistic style, with natural human features, realistic lighting, and cinematic atmosphere, as if taken by a professional camera. "
```
---
## ⚙️ Tech Stack

- **Frontend**: React + Vite
- **Backend**: FastAPI (Python)
- **AI Services**: OpenAI (DALL·E 3 + CLIP)
- **Other**: Axios, Node.js, Python Venv


## 🛠️ Getting Started
### 🔹 Clone the Repository

```bash
git clone https://github.com/Balaji-30/ImageFusion.git
cd ImageFusion
```

### 🔹 Backend (FastAPI)

```bash
cd backend
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt
uvicorn main:app --reload
```
In the backend/ directory, create a .env file to store your OpenAI API key (OPENAI_API_KEY=YOUR_API_KEY).

### 🔹 Frontend (React + Vite)
```bash
cd frontend
npm install
npm run dev
```
---
### Qualitative Evaluation

**Before Improvements:**
- Random artifacts introduced.
- Backgrounds mismatched.
- People missing or distorted.
<br>

**After Improvements:**
- All key elements appear in the correct context.
- People accurately portrayed with background and prop.
- No split scenes or collage layouts—single continuous image achieved.
---
### Realistic Use Cases

| Use Case              | Why Trust is Critical                                                |
|------------------------|----------------------------------------------------------------------|
| Educational posters    | Students and teachers expect accurate representations.              |
| Personalized marketing | Clients expect that inputs (faces, products) are preserved accurately. |
| Creative media content | Trust in faithful visualization encourages user creativity.         |

