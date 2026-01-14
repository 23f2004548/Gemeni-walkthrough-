Image to Text Generator with Google Gemini
This project demonstrates how to leverage the Google Gemini API for powerful text and image understanding capabilities, specifically focusing on generating descriptive text from images and engaging with text prompts.

Table of Contents
Features
Setup
Usage
API Key Configuration
Text Generation
Image to Text Generation
Interactive Streamlit Application
Models Used
Features
Gemini API Integration: Seamlessly connect to and utilize Google's Generative AI models.
Text-to-Text Generation: Generate creative or informative text based on textual prompts.
Image-to-Text Generation: Understand and describe images, or extract information from them using multimodal prompts.
Streamlit Web Application: An interactive web interface for uploading images and getting real-time responses from the Gemini model.
Setup
To run this project, you'll need a Google API Key and the necessary Python libraries.

Google API Key:

Obtain a Gemini API key from Google AI Studio.
In Google Colab, add your API key to the Secrets panel (🔑 icon on the left sidebar) and name it GOOGLE_API_KEY.
Install Dependencies: Run the following cells in your Colab notebook to install the required libraries:

!pip install -q U google-generativeai streamlit
Import Libraries and Configure API: Ensure the following cells are present and executed to import necessary libraries and configure the API key:

import google.generativeai as genai
import pathlib
import textwrap
from IPython.display import display, Markdown
from google.colab import userdata

# Setup API Key
GOOGLE_API_KEY = userdata.get('GOOGLE_API_KEY')
genai.configure(api_key=GOOGLE_API_KEY)
Usage
API Key Configuration
The notebook already includes cells to set up your API key from Colab secrets. Ensure GOOGLE_API_KEY is configured.

Text Generation
Initialize a generative model and use it to generate text:

model = genai.GenerativeModel('gemini-2.5-flash') # Or 'gemini-pro-latest' or any other suitable model
response = model.generate_content("What is the meaning of life?")
print(response.text)
Image to Text Generation
First, download an image (or use your own PIL.Image object):

!curl -o image.jpg https://images.unsplash.com/photo-1761839259488-2bdeeae794f5?w=1000&auto=format&fit=crop&q=60&ixlib=rb-4.1.0&ixid=M3wxMjA3fDF8MHxmZWF0dXJlZC1waG90b3MtZmVlZHwxfHx8ZW58MHx8fHx8
import PIL.Image
img = PIL.Image.open('image.jpg')
Then, generate content based on the image:

response = model.generate_content(img) # Generate a description based on the image
print(response.text)

# Or with a specific text prompt:
response = model.generate_content(["Write a short, engaging blog post based on this picture. It should include a description of it", img])
print(response.text)
