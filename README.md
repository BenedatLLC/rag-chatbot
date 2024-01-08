# ChatBot for Multiple Documentation Q&A

This repository contains Jupyter Notebooks to perform retrieval Q&A from multiple PDF documents. It supports multiple language models OpenAI and local Falcon. If you don't have an OpenAI key, by default, it selects local Falcon language model. Note: Local LLM will be slow if you have limited memory on your laptop (recommend RAM >= 16GB)

## How the project rag-chatbot is structured?
Jupyter notebooks are in the rag-chatbot directory. 

* ./source (store your PDF files here. By default, Kubernetes PDFs are stored here. Kubernetes PDFs are from https://github.com/dohsimpson/kubernetes-doc-pdf/. Refer to this repo for the latest k8s PDFs.)
* ./image (Your chat website logo)
* ./db (Your ChromaDB output directory)

# How to run the code
1. `$ git clone https://github.com/BenedatLLC/rag-chatbot.git`
2. `$ cd rag-chatbot`
3. `$ conda env create -f environment.yml`
4. `$ conda activate rag-chatbot`
5. Import the sample PDF files into the Chroma DB (vector database):  
   * `$ jupyter lab`
   * Open 'loaddb.ipynb'
   * Execute all cells in 'loaddb.ipynb'   
6. `$ panel serve chatbot.ipynb # back on the command line`
7. Open your browser, enter http://localhost:5006/chatbot in your browser. Note: if you are running this the first time, it will be really slow to show the chatbot interface because it is downloading the local LLM, Falcon, loading ChromaDB, and loading local LLM. After the first time, when you run the chatbot in your browser, it only needs to load ChromaDB and Local LLM before showing the chat interface. 
8. By default, "Local LLM" is selected. If you have an OpenAI API key, see the "Configure your OpenAI key" section below. If you use the local LLM option, depending on your computer's memory (>=16 GB is recommended), you might experience slow response from the chatbot. 

# Configure your OpenAI key
There are two ways to setup OpenAI key in MacOS:
Option 1: Set up your OpenAI key in your OS environment
1. Run the following in your commandline window
   * `$ echo "export OPENAI_API_KEY='yourkey'" >> ~/.zshrc`
   * `$ source ~/.zshrc`
2. Select "OS Env OpenAI"
3. Enter your questions from the main chat interface.

   
Option 2: Enter you OpenAI key in your Chatbot interface
1. Select "Enter OpenAI" option from Sidebar "Select LLM" option
2. Enter your OpenAI API key in the entry field below the above option
3. Enter your questions from the main chat interface
Note: ChatBot will take the UI OpenAI API key when the "Enter OpenAI" is selected. 

# Load your own PDFs
1. Delete PDFs under ./source
2. Copy your PDFs to ./source
3. Run 'Jupyter Lab'
4. Open 'loaddb.ipynb'
5. Execute all cells in 'loaddb.ipynb'
6. In command line, run 'panel serve chatbot.ipynb'. Now, you can retrieve information from your own PDFs. 
   
# Troubleshooting
* If it is the first time running chatbot.ipynb, it will take awhile because the notebook is going to download the local language model, ~4.2GB.
* When you load the chatbot interface(http://localhost:5006/chatbot), it will take a couple of seconds because it is trying to load the ChromaDB and Local language model. 
