# AI-Powered Job Application Toolkit

## Overview
This project consists of three independent AI-powered applications designed to optimize the job application process. Each tool serves a distinct purpose:

1. **Resume Enhancer:** Polishes resumes to align with job descriptions.
2. **Cover Letter Generator:** Creates personalized cover letters.
3. **Career Advisor:** Provides strategic job search insights.

Each application is built using **IBM Watsonx.ai** and **Gradio**, offering an interactive user-friendly experience.

---

# 1. Resume Enhancer

## Introduction
The Resume Enhancer improves the clarity, relevance, and impact of a user's resume to better align with job requirements. It allows users to specify a job position and optional polishing instructions.

## Technologies Used
- Python
- IBM Watsonx.ai
- Gradio

## Code
```python
from ibm_watsonx_ai import Credentials
from ibm_watsonx_ai.foundation_models import ModelInference
from ibm_watsonx_ai.foundation_models.schema import TextChatParameters
import gradio as gr

credentials = Credentials(url="https://us-south.ml.cloud.ibm.com")
params = TextChatParameters(temperature=0.7, max_tokens=512)
model = ModelInference(model_id="meta-llama/llama-3-2-11b-vision-instruct", credentials=credentials, params=params)

def polish_resume(position_name, resume_content, polish_prompt=""):
    prompt = f"Enhance this resume for a {position_name} position. {polish_prompt} Resume: {resume_content}"
    messages = [{"role": "user", "content": [{"type": "text", "text": prompt}]}]
    response = model.chat(messages=messages)
    return response['choices'][0]['message']['content']

resume_polish_app = gr.Interface(
    fn=polish_resume,
    inputs=[
        gr.Textbox(label="Position Name"),
        gr.Textbox(label="Resume Content", lines=20),
        gr.Textbox(label="Polish Instructions (Optional)", lines=2)
    ],
    outputs=gr.Textbox(label="Polished Resume"),
    title="Resume Enhancer"
)
resume_polish_app.launch()
```

---

# 2. Cover Letter Generator

## Introduction
This application generates a customized cover letter based on a given job description and resume. It ensures alignment between the applicant's qualifications and the job requirements.

## Technologies Used
- Python
- IBM Watsonx.ai
- Gradio

## Code
```python
from ibm_watsonx_ai import Credentials
from ibm_watsonx_ai.foundation_models import ModelInference
from ibm_watsonx_ai.foundation_models.schema import TextChatParameters
import gradio as gr

credentials = Credentials(url="https://us-south.ml.cloud.ibm.com")
params = TextChatParameters(temperature=0.7, max_tokens=512)
model = ModelInference(model_id="meta-llama/llama-3-2-11b-vision-instruct", credentials=credentials, params=params)

def generate_cover_letter(company_name, position_name, job_description, resume_content):
    prompt = f"Write a cover letter for {company_name} applying for {position_name}. Job: {job_description}. Resume: {resume_content}"
    messages = [{"role": "user", "content": [{"type": "text", "text": prompt}]}]
    response = model.chat(messages=messages)
    return response['choices'][0]['message']['content']

cover_letter_app = gr.Interface(
    fn=generate_cover_letter,
    inputs=[
        gr.Textbox(label="Company Name"),
        gr.Textbox(label="Position Name"),
        gr.Textbox(label="Job Description", lines=10),
        gr.Textbox(label="Resume Content", lines=10)
    ],
    outputs=gr.Textbox(label="Generated Cover Letter"),
    title="Cover Letter Generator"
)
cover_letter_app.launch()
```

---

# 3. Career Advisor

## Introduction
The Career Advisor evaluates a job posting and an applicant's resume to provide strategic guidance on improving their chances of securing the position.

## Technologies Used
- Python
- IBM Watsonx.ai
- Gradio

## Code
```python
from ibm_watsonx_ai import Credentials
from ibm_watsonx_ai.foundation_models import ModelInference
from ibm_watsonx_ai.foundation_models.schema import TextChatParameters
import gradio as gr

credentials = Credentials(url="https://us-south.ml.cloud.ibm.com")
params = TextChatParameters(temperature=0.7, max_tokens=1024)
model = ModelInference(model_id="meta-llama/llama-3-2-11b-vision-instruct", credentials=credentials, params=params)

def generate_career_advice(position_applied, job_description, resume_content):
    prompt = f"Analyze this resume against the job description for {position_applied}. {job_description}. Resume: {resume_content}"
    messages = [{"role": "user", "content": [{"type": "text", "text": prompt}]}]
    response = model.chat(messages=messages)
    return response['choices'][0]['message']['content']

career_advice_app = gr.Interface(
    fn=generate_career_advice,
    inputs=[
        gr.Textbox(label="Position Applied For"),
        gr.Textbox(label="Job Description", lines=10),
        gr.Textbox(label="Resume Content", lines=10)
    ],
    outputs=gr.Textbox(label="Career Advice"),
    title="Career Advisor"
)
career_advice_app.launch()
```

---


###  Run Each Application
```bash
python resume_enhancer.py
python cover_letter_generator.py
python career_advisor.py
```

---

## Conclusion
These three independent applications provide job seekers with powerful AI-driven tools to enhance their applications. By leveraging IBM Watsonx.ai and NLP, they help users craft stronger resumes, cover letters, and job strategies, ultimately improving their chances of career success.


