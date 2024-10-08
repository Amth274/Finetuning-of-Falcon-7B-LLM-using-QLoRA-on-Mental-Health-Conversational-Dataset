# Chatbot using QLoRA on Falcon 7B with Gradio Interface


## Introduction:
Mental health issues are often misunderstood or not fully grasped by the general public.
Mental health directly impacts an individual's overall well-being, quality of life, and ability to function effectively in daily life. Good mental health is essential for experiencing happiness, fulfilment, and a sense of purpose. Mental health and physical health are closely intertwined. Untreated mental health issues can lead to or worsen physical health problems, such as cardiovascular diseases, weakened immune systems, and chronic conditions.
This project involves fine-tunin  g a large language model (Falcon 7B) using Quantized Low-Rank Adaptation (QLoRA) for efficient memory use, and deploying the model through a Gradio-based web interface for interactive conversations.



## Core Rationale:
Chatbots offer a readily available and accessible platform for individuals seeking support. They can be accessed anytime and anywhere, providing immediate assistance to those in need. Chatbots can offer empathetic and non-judgmental responses, providing emotional support to users. While they cannot replace human interaction entirely, they can be a helpful supplement, especially in moments of distress.<br><br>
NOTE: _It is important to note that while mental health chatbots can be helpful, they are not a replacement for professional mental health care. They can complement existing mental health services by providing additional support and resources._

## Dataset:
The dataset was curated from online FAQs related to mental health, popular healthcare blogs like WebMD, Mayo Clinic and Healthline, and other wiki articles related to mental health. The dataset was pre-processed in a conversational format such that both questions asked by the patient and responses given by the doctor are in the same text. The dataset for this mental health conversation can be found here: [heliosbrahma/mental_health_chatbot_dataset](https://huggingface.co/datasets/heliosbrahma/mental_health_chatbot_dataset).<br><br>
NOTE: _All questions and answers have been anonymized to remove any PII data and preprocessed to remove any unwanted characters._

## Model Finetuning:
This is the major step in the entire project. I have used sharded Falcon-7B pre-trained model and finetuned it to using the QLoRA technique on my custom mental health dataset. The entire finetuning process took less than an hour and it was finetuned entirely on Nvidia A100 from Google Colab Pro. But, it could also be trained on free-tier GPU using Nvidia T4 provided by Colab. In that case,  ensure to use max_steps less than 150.<br>
**Model**: Fine-tuned Falcon 7B using QLoRA and PEFT.<br>
**Efficiency:** 4-bit quantization for reduced memory usage.<br>
**Interface:** Deployed using a Gradio web-based interface.<br>
**Customization**: Easily adaptable for other models or datasets.<br>
NOTE: _Try changing hyperparameters in TrainingArguments and LoraConfig based on your requirements. With the settings mentioned in notebook, I achieved 0.031 training loss after 320 steps._

## Requirements 
python 3.8 or higher<br>
Required libraries:<br>
`gradio==3.31.0`<br>
`transformers==4.32.0`<br>
`trl==0.6.0`<br>
`langchain==0.0.273`<br>
`peft==0.5.0`<br>
`datasets==2.13.1`<br>
`einops==0.7.0`<br>

##  Install Dependencies
Make sure all the necessary Python libraries are installed. You can install them using the following command:<br>
```python
pip install gradio==3.41.0 transformers==4.32.0 langchain==0.0.273 accelerate==0.12.0 bitsandbytes==0.41.1 peft==0.5.0 trl==0.6.0 datasets==2.13.1 einops==0.7.0 wandb==0.15.8
```

## Model Inference:
Run `gradio_chatbot_app.ipynb` notebook to get a chatbot like interface using Gradio as frontend for demo. Play around with different hyperparameter config settings for answer generation and run multiple queries to check for the quality of generated response. 


It takes less than 3 minutes to generate the model response. Compare the PEFT model response with the original model response in `funetuned_qlora_falcon7b.ipynb` notebook.

## Conclusion:
Here is a detailed technical blog explaining key concepts of QLoRA and PEFT fine-tuning method: [Fine-tuning of Falcon-7B Large Language Model using QLoRA on Mental Health Dataset](https://medium.com/@iamarunbrahma/fine-tuning-of-falcon-7b-large-language-model-using-qlora-on-mental-health-dataset-aa290eb6ec85). If you still have any queries, you can open an issue on this repo or comment on my blog.

_If you like this project, please :star: this repository_.
