# Taller 8.1 | AREP

# Building a Simple LLM Application with LangChain

## Overview

This guide provides a step-by-step tutorial on how to build a simple Language Model (LLM) application using LangChain. The application will translate text from English into another language. This is a great starting point for understanding the basics of LangChain, including how to use language models, create prompt templates, and debug your application.

By the end of this tutorial, you will have a high-level understanding of:

- **Using Language Models**: How to interact with different language models.
- **Using Prompt Templates**: How to create and use prompt templates to structure inputs for language models.
- **Debugging and Tracing**: How to debug and trace your application using LangSmith (though this part is not covered in detail here).

## Setup

### Jupyter Notebook

This tutorial is best followed in a Jupyter Notebook, which provides an interactive environment for running and experimenting with the code. If you don't have Jupyter installed, you can find installation instructions [here](https://jupyter.org/install).

### Installation

To install LangChain, you can use either `pip` or `conda`:

### Pip

```bash
pip install langchain

```

### Conda

```bash
conda install langchain

```

For more detailed installation instructions, refer to the [LangChain Installation Guide](https://langchain.com/installation).

## Using Language Models

### Selecting a Chat Model

First, let's learn how to use a language model by itself. LangChain supports many different language models that you can use interchangeably. To get started, you'll need to install the necessary dependencies and set up your API key.

```bash
pip install -qU "langchain[openai]"

```

Next, set up your OpenAI API key:

```python
import getpass
import os

if not os.environ.get("OPENAI_API_KEY"):
    os.environ["OPENAI_API_KEY"] = getpass.getpass("Enter API key for OpenAI: ")

```

Now, initialize the chat model:

```python
from langchain.chat_models import init_chat_model

model = init_chat_model("gpt-4o-mini", model_provider="openai")

```

### Interacting with the Model

Chat models in LangChain are instances of `Runnables`, which means they expose a standard interface for interaction. You can pass a list of messages to the `.invoke` method to get a response from the model.

```python
from langchain_core.messages import HumanMessage, SystemMessage

messages = [
    SystemMessage("Translate the following from English into Italian"),
    HumanMessage("hi!"),
]

response = model.invoke(messages)
print(response.content)

```

### Streaming Responses

LangChain also supports streaming responses from the model, allowing you to receive tokens as they are generated:

```python
for token in model.stream(messages):
    print(token.content, end="|")

```

## Prompt Templates

### Creating a Prompt Template

Prompt templates help you structure the input to the language model. They take raw user input and transform it into a format that the model can understand. Let's create a prompt template that takes two variables:

- `language`: The language to translate the text into.
- `text`: The text to translate.

```python
from langchain_core.prompts import ChatPromptTemplate

system_template = "Translate the following from English into {language}"
prompt_template = ChatPromptTemplate.from_messages(
    [("system", system_template), ("user", "{text}")]
)

```

### Using the Prompt Template

You can use the prompt template to format the input and then pass it to the model:

```python
prompt = prompt_template.invoke({"language": "Italian", "text": "hi!"})
response = model.invoke(prompt)
print(response.content)

```

### Inspecting the Prompt

You can inspect the formatted prompt to see how it structures the input:

```python
prompt.to_messages()

```

This will return a list of messages that the model will receive, including the system message and the user input.

## Conclusion

Congratulations! You've built a simple LLM application that translates text from English into another language. You've learned how to:

- Use language models in LangChain.
- Create and use prompt templates to structure inputs.
- Stream responses from the model.

This is just the beginning of what you can do with LangChain. To dive deeper, check out the [LangChain Conceptual Guides](https://langchain.com/concepts) and [How-To Guides](https://langchain.com/how-to) for more advanced topics and techniques.
