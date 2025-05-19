# ImageFusion

ImageFusion is a fullstack web application that combines multiple user-provided images (like people, backgrounds, and objects) into a single, coherent scene using AI. It uses OpenAI’s DALL·E for generation and CLIP for output evaluation.

---

<p align="center">
  <img src="./assets/ImageFusionCropped.PNG" alt="ImageFusion Banner">
</p>

---

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

## ⚙️ Tech Stack

- **Frontend**: React + Vite
- **Backend**: FastAPI (Python)
- **AI Services**: OpenAI (DALL·E 3 + CLIP)
- **Other**: Axios, Node.js, Python Venv

---

## 🚀 Features

- Upload multiple images (people, background, props)
- Extract visual details using prompt engineering
- Generate a fused image based on a user prompt
- Evaluate semantic similarity using CLIP
- Lightweight and fast client-server setup

## 🛠️ Getting Started

### 🔹 Backend (FastAPI)

```bash
cd backend
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt
uvicorn main:app --reload
```
### 🔹 Frontend (React + Vite)
```bash
cd frontend
npm install
npm run dev
```
