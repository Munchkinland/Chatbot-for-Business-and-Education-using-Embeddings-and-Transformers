# Chatbot-for-Business-and-Education-using-Embeddings-and-Transformers
A powerful chatbot for business and education that uses embeddings and transformers to provide accurate and personalized responses, enhancing user experiences. Customizable and adaptable, it leverages NLP techniques to automate tasks, offer guidance, and streamline processes.
 The project is a conversational chatbot specifically developed for business and educational purposes. It leverages the power of embeddings and transformers to deliver highly accurate and contextually relevant responses to user queries. By incorporating advanced natural language processing techniques, the chatbot enables seamless interaction with users, providing them with real-time information and assistance.

With a focus on enhancing the user experience, the chatbot offers prompt and precise answers to frequently asked questions, as well as tailored responses to specific inquiries. It serves as a virtual assistant, capable of understanding and addressing a wide range of topics related to the business or educational domain.

One of the key advantages of this project is its ability to be customized and trained using domain-specific data. This allows businesses and educational institutions to fine-tune the chatbot according to their specific needs and requirements. By incorporating their own data, they can create a more personalized and effective conversational experience for their users.

The chatbot's underlying technology utilizes embeddings, which capture the semantic representation of text, enabling a deeper understanding of user queries. This, combined with transformers, enables the chatbot to generate contextually appropriate responses with a high degree of accuracy. The model continuously learns and adapts from user interactions, improving its performance over time.

In a business context, the chatbot can serve as an efficient customer support tool, providing instant responses to common inquiries and guiding users through various processes. It can also act as a virtual assistant, assisting with tasks such as appointment scheduling, order tracking, and product recommendations.

In the education sector, the chatbot can support students by answering their questions, providing study materials, and offering guidance on educational pathways. It can assist educators by automating administrative tasks, delivering relevant educational resources, and facilitating online learning experiences.

Guide explaining the code step by step:

Importing the libraries:

python
Copy code
import os
import openai
from llama_index import GPTVectorStoreIndex, SimpleDirectoryReader, LLMPredictor, ServiceContext
from langchain.chat_models import ChatOpenAI
import textwrap
In this section, the necessary libraries for the code are imported. These libraries include os for operating system manipulation, openai for interacting with the OpenAI API, llama_index for text indexing and searching, langchain for chat models, and textwrap for text formatting.

Installing packages:

python
Copy code
!pip install PyPDF2
!pip install openai
!pip install langchain
!pip install llama-index
In this section, some required packages are installed. The !pip install commands are used to install the specified packages. In this case, PyPDF2, openai, langchain, and llama-index are being installed.

Setting up the OpenAI API key:

python
Copy code
os.environ["OPENAI_API_KEY"] = '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'
Here, the OpenAI API key is configured by assigning the key to the environment variable "OPENAI_API_KEY". Make sure to replace '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' with your own OpenAI API key.

Reading the PDF files:

python
Copy code
pdf = SimpleDirectoryReader('datos').load_data()
In this line of code, the SimpleDirectoryReader from llama_index is used to read data from a folder named "datos" that contains PDF files. The load_data() function loads the data and stores it in the variable pdf.

Defining and instantiating the chat model:

python
Copy code
modelo = LLMPredictor(llm=ChatOpenAI(temperature=0, model_name='gpt-3.5-turbo'))
Here, the chat model is defined and instantiated using LLMPredictor from llama_index. The chat model used is ChatOpenAI with a temperature of 0 and the model name 'gpt-3.5-turbo'. The chat model is assigned to the variable modelo.

Indexing the content of the PDFs:

python
Copy code
service_context = ServiceContext.from_defaults(llm_predictor=modelo)
index = GPTVectorStoreIndex.from_documents(pdf, service_context=service_context)
In these lines of code, a service context is created using ServiceContext and the chat model (modelo) is passed as an argument. Then, GPTVectorStoreIndex from llama_index is used to create an index from the loaded PDF documents (pdf). The index is assigned to the variable index.

Saving the index to disk (optional):

python
Copy code
#index.save_to_disk('index.json')
If you want to save the index to disk to avoid repeating the entire process each time, you can uncomment this line of code to save the index to a JSON file named 'index.json'. However, this line is currently commented out.

Loading the index from disk (optional):

python
Copy code
#index = GPTVectorStoreIndex.load_from_disk('index.json')
If you previously saved the index to disk and want to load it again, you can uncomment this line of code to load the index from the JSON file 'index.json'. However, this line is also currently commented out.

Main loop:

python
Copy code
while True:
    question = input('Type your answer   \n') + "Reply"
     reply= index.as_query_engine().query(question)
  for sentence in textwrap.wrap(reply.response, width=100):
    print(sentence)
