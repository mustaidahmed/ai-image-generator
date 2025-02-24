Stable Diffusion 2.1 Deployment in Google Colab

Overview

This project runs Stable Diffusion 2.1 in Google Colab and deploys it as a web app using Gradio. Users can generate AI-powered images by entering text prompts.

Features

🚀 Text-to-Image Generation using Stable Diffusion 2.1

🎨 Gradio Web UI for easy interaction

☁️ Colab Deployment with Public URL

🔥 GPU Acceleration for Faster Image Processing

Installation

Before running the script, install the required dependencies:

!pip install --upgrade diffusers transformers accelerate torch bitsandbytes scipy safetensors xformers torchvision gradio

Running in Google Colab

Open Google Colab and create a new notebook.

Copy and paste the script below into a code cell:

import torch
from diffusers import StableDiffusionPipeline, DPMSolverMultistepScheduler
import gradio as gr

# Load Model
model_id = "stabilityai/stable-diffusion-2-1"
pipe = StableDiffusionPipeline.from_pretrained(model_id, torch_dtype=torch.float16)
pipe.scheduler = DPMSolverMultistepScheduler.from_config(pipe.scheduler.config)
pipe = pipe.to("cuda")

# Function to generate image
def generate_image(prompt):
    image = pipe(prompt, guidance_scale=7.5).images[0]
    return image

# Gradio UI
interface = gr.Interface(
    fn=generate_image,
    inputs=gr.Textbox(label="Enter your prompt"),
    outputs=gr.Image(),
    title="Stable Diffusion 2.1 Generator",
    description="Generate AI-powered images with Stable Diffusion 2.1"
)

# Launch UI
interface.launch(share=True)

Run the notebook and wait for the model to load.

Click the public Gradio link to use the web app.

Deployment Options

Hugging Face Spaces: Upload app.py with the script and a requirements.txt file.

Google Cloud Run / AWS: Use FastAPI for API-based deployment.

Example Usage

Prompt: "A dragon breathing fire over a medieval village, cinematic lighting, ultra-detailed, fantasy art"
Result: [Generated AI Image]

License

This project is licensed under the MIT License.

