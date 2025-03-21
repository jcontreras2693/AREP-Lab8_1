# Taller 8.1 | AREP

# Building a Simple LLM Application with LangChain

## Overview

This repository contains a simple Language Model (LLM) application built using **LangChain**. The application translates text from English into another language using a chat model and prompt templates. This project serves as an introduction to LangChain, demonstrating how to use language models, create prompt templates, and structure inputs for LLMs.

By following this guide, you will learn:

- How to use **language models** in LangChain.
- How to create and use **prompt templates** to structure inputs.
- How to interact with chat models and **stream responses**.

---

## Project Architecture and Components

The application consists of the following components:

1. **Language Model**: The core component that performs the translation. In this example, we use OpenAI's GPT model.
2. **Prompt Templates**: Structures the input for the language model by combining user input with predefined instructions.
3. **Streaming Interface**: Allows for real-time token streaming from the model.
4. **Environment Setup**: Includes installation instructions and API key configuration.

---

## Installation

### Prerequisites

- Python 3.7 or higher.
- A valid OpenAI API key.

### Step-by-Step Instructions

1. **Install LangChain**:
You can install LangChain using `pip` or `conda`.
    
    ### Using Pip:
    
    ```bash
    pip install langchain
    
    ```
    
    ### Using Conda:
    
    ```bash
    conda install langchain
    
    ```
    
2. **Install Additional Dependencies**:
To use the OpenAI chat model, install the required dependencies:
    
    ```bash
    pip install -qU "langchain[openai]"
    
    ```
    
3. **Set Up Your OpenAI API Key**:
Set your OpenAI API key as an environment variable. You can do this in your terminal or within a Jupyter Notebook.
    
    ### In Terminal:
    
    ```bash
    export OPENAI_API_KEY="your-api-key-here"
    
    ```
    
    ### In a Jupyter Notebook:
    
    ```python
    import getpass
    import os
    
    if not os.environ.get("OPENAI_API_KEY"):
        os.environ["OPENAI_API_KEY"] = getpass.getpass("Enter API key for OpenAI: ")
    
    ```
    

---

## Running the Code

### Step 1: Initialize the Chat Model

First, initialize the chat model using LangChain:

```python
from langchain.chat_models import init_chat_model

model = init_chat_model("gpt-4o-mini", model_provider="openai")

```

### Step 2: Interact with the Model

You can interact with the model by passing a list of messages. Here’s an example of translating "hi!" from English to Italian:

```python
from langchain_core.messages import HumanMessage, SystemMessage

messages = [
    SystemMessage("Translate the following from English into Italian"),
    HumanMessage("hi!"),
]

response = model.invoke(messages)
print(response.content)  # Output: Ciao!

```

### Step 3: Stream Responses

LangChain supports streaming responses, allowing you to receive tokens as they are generated:

```python
for token in model.stream(messages):
    print(token.content, end="|")

```

Output:

```
|C|iao|!|

```

---

## Using Prompt Templates

### Step 1: Create a Prompt Template

Prompt templates help structure the input for the language model. Here’s how to create a template that takes two variables:

- `language`: The target language for translation.
- `text`: The text to translate.

```python
from langchain_core.prompts import ChatPromptTemplate

system_template = "Translate the following from English into {language}"
prompt_template = ChatPromptTemplate.from_messages(
    [("system", system_template), ("user", "{text}")]
)

```

### Step 2: Format and Use the Prompt

You can format the prompt with user input and pass it to the model:

```python
prompt = prompt_template.invoke({"language": "Italian", "text": "hi!"})
response = model.invoke(prompt)
print(response.content)  # Output: Ciao!

```

### Step 3: Inspect the Prompt

You can inspect the formatted prompt to see how it structures the input:

```python
prompt.to_messages()

```

Output:

```python
[
    SystemMessage(content='Translate the following from English into Italian'),
    HumanMessage(content='hi!')
]

```

---

## Example Output

Here’s an example of the application in action:

### Input:

```python
prompt = prompt_template.invoke({"language": "French", "text": "Hello!"})
response = model.invoke(prompt)
print(response.content)

```

### Output:

```
Bonjour!

```

---

## Screenshots

![image](https://github.com/user-attachments/assets/13a6c009-9088-47d9-9e81-cc49404c06c0)

---

## Conclusion

This project demonstrates how to build a simple LLM application using LangChain. You’ve learned how to:

- Use language models for translation.
- Create and use prompt templates.
- Stream responses from the model.

This is just the beginning! LangChain offers many more features for building complex AI applications. For further learning, check out the [LangChain Documentation](https://langchain.com/docs).

---

## Acknowledgement

* [LangChain Tutorial](https://python.langchain.com/docs/tutorials/llm_chain/)

## Authors

* **Juan David Contreras Becerra** - *Taller 8.1 | AREP* - [AREP-Lab8.1](https://github.com/jcontreras2693/AREP-Lab8_1.git)
