# PromptFlow_str_for_TVGPT

## Overview 
This repository contains a **Prompt Flow** structure designed to automate and optimize complex workflows involving multi-step prompts for various use cases. It allows users to orchestrate a series of prompts, perform pre-processing and post-processing, and integrate multiple components to achieve desired outcomes.
As a use-case example, we will create an AI assistant that recommends movies or series on TV from digital and satellite channels.
This is graph structure of my prompt flow : 

![image](https://github.com/user-attachments/assets/4f97e5e0-cc36-4356-b50e-2902dc654045)

## Get Started 

### Prerequisites

- Azure subscription

  
Azure Account - If you're new to Azure, get an Azure account for [free](https://azure.microsoft.com/en-us/free/?wt.mc_id=online-social-sicotin)
 and you'll get some free Azure credits to get started.

- [Azure Open AI](https://azure.microsoft.com/tr-tr/products/ai-services/openai-service)


  
Azure subscription with access enabled for the Azure OpenAI Service - For more details, see the [Azure OpenAI Service documentation on how to get access](https://learn.microsoft.com/en-us/azure/ai-services/openai/overview#how-do-i-get-access-to-azure-openai).
Azure OpenAI resource - For these samples, you'll need to deploy models like GPT-3.5 Turbo, GPT 4, DALL-E, and Whisper. See the Azure OpenAI Service documentation for more details on [deploying models](https://learn.microsoft.com/en-us/azure/ai-services/openai/how-to/create-resource?pivots=web-portal) and [model availability](https://learn.microsoft.com/en-us/azure/ai-services/openai/concepts/models)

- [Azure Machine Learning workspace](https://azure.microsoft.com/en-us/products/machine-learning)
  
![image](https://github.com/user-attachments/assets/13d78b66-b84d-459a-930c-9365fddb13fc)

### Define Inputs & Outputs 

Define your Prompt Flow input and outputs like this :


![image](https://github.com/user-attachments/assets/d3be0207-32c2-40fb-b755-e390fac78e6c)

### Extract Query

To get a more accurate answer, you need to extract intent from the question you want to ask in a way that AI can understand. 
To do this:
1. Create LLM in Azure Machine Learning Studio.
![image](https://github.com/user-attachments/assets/e8d33897-c09a-4410-a26c-1336b5775601)

2. Name the LLM you added. 
![image](https://github.com/user-attachments/assets/ee8bc42e-0651-4083-b765-2a4e9c41a6d1)

3. Give Connection, Api, deployment_name and response_format to the input section, chat_history and question.

![image](https://github.com/user-attachments/assets/7f3b71bc-b393-42a2-af6f-7f421ad4bbf2)

4. Take the extract_query.txt content in this repo and paste it into the LLM.
Note: This shows it how to extract intent. You can also make this LLM work by binding it to a condition using the Activate Config feature.
![image](https://github.com/user-attachments/assets/0c82027f-a94e-42e4-8ec9-aedcf776e603)

### Get Data from API

According to the intent we extracted, we will send a series movie query from public APIs. I used tvmaze and rapid API sites here. If desired, another site can be used.

Accordingly:
1. Add Python code and give it a name.
![image](https://github.com/user-attachments/assets/abf8713e-7b0a-412f-8e1f-0cfabd7e4fd0)
2. For country_code as input, give 'TR' and the output that was just returned from extract_query.txt.
![image](https://github.com/user-attachments/assets/a64ea030-d013-492d-9185-6c0b79cee075)

3.Take the get_data.py code from this repo and paste it.

### EPG data

We will manually get the EPG data and put it into the blob. Then we will read it from there.

For this:
1. Add Python code and give it a name. We will give the Connection string, container name and blob names of Azure blob Storage as input. Since we defined these in the input section at the beginning, there is no need to rewrite them in the code.
![image](https://github.com/user-attachments/assets/2759224a-191a-4fff-a315-d4f6c340a058)

2. Get and paste the get_EPG_blob.py from this repo.

### Chat 

We will send the data we created and the data received as a result of the query to the LLM, which we call chat, and we will write a prompt here that includes the prompt's capabilities, instructions, and how it should respond.

1. Enter the connection, APi and deployment_name and response_format.
![image](https://github.com/user-attachments/assets/4d72d74c-9098-43d6-8532-ac28743835d8)

2.Give chat_history, contexts, question and user_info as input
![image](https://github.com/user-attachments/assets/2c51cf69-6c6c-45b5-96de-189d4cbf2929)


3. Paste the content of chat_prompt.txt from this repo.

## TEST TIME 
After starting the start compute session in the upper right corner of the page, you can start testing from the chat button.


