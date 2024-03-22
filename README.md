
# Groq API Chat Assistant

The Groq API Chat Assistant is a tool that utilizes the Groq API to create a chat assistant capable of generating responses to user queries or prompts. It leverages large language models (LLMs) to provide informative and contextually relevant answers, making it suitable for a variety of applications such as customer support, information retrieval, and conversational interfaces.


## Installation

To run this project, you need to install the necessary dependencies. Run the following command in your Colab notebook:

   ```bash
   !pip install -q -U langchain langchain_core langchain_groq gradio
   ```



## Getting Started:

To use this notebook, you will need to have the following:

- Python 3.6+
- Google Colab account
- Groq API key (you can sign up for a free account at groq.ai)
## Usage


### 1. Initialize the Model:

```python
from google.colab import userdata
groq_api_key = userdata.get('GROQ_API_KEY')

from langchain_groq import ChatGroq

chat = ChatGroq(
    api_key = groq_api_key,
    model_name = "mixtral-8x7b-32768"
)
```

### 2. Create a Chain:

```python
from langchain_core.output_parsers import StrOutputParser

chain = prompt | chat | StrOutputParser()

response = chain.invoke({"text":"Why is the sky blue?"})
print(response)
```

### 3. Build an App:

```python
import gradio as gr

def fetch_response(user_input):
    chat = ChatGroq(
        api_key = groq_api_key,
        model_name = "mixtral-8x7b-32768"
    )
    system = "You are a helpful assistant."
    human = "{text}"

    prompt = ChatPromptTemplate.from_messages(
        [
            ("system", system), ("human", human)
        ]
    )
    chain = prompt | chat | StrOutputParser()
    output = chain.invoke({"text": user_input})
    return output

user_input = "Why is the sky blue?"

fetch_response(user_input)
```

### 4. Create an Interface:

```python
iface = gr.Interface(
    fn = fetch_response,
    inputs = "text",
    outputs = "text",
    title = "Groq Chatbot",
    description="Ask a question and get a response."
)

iface.launch()
```



## API Reference


- **ChatGroq:** This class initializes the Groq API for chat functionality. It requires an API key and a model name as parameters.
- **ChatPromptTemplate:** This class creates a chat prompt template for interacting with the Groq API.
- **StrOutputParser:** This class parses the output response from the Groq API into a string format.


## Additional Notes

- The code is divided into several sections, including installation instructions, imports, model initialization, and the main function.
- The ``groq_api_key`` variable is used to store your Groq API key. You can find your API key on the Groq website.
- The ``gradio`` library is used to create an interface for the chatbot.
## Acknowledgements

- [Groq API documentation](https://console.groq.com/docs/quickstart)
- [LangChain documentation](https://python.langchain.com/docs/get_started/introduction)
- [Gradio documentation](https://www.gradio.app/docs/interface)
## Authors


- [@Shubham Bhatia](https://www.linkedin.com/in/shubhambhatia2103/)


## Feedback

If you have any feedback, please reach out to me at Shubhambhatia2103@gmail.com

