# ChatBot for Multiple Documentation Q&A

This repository contains Jupyter Notebooks to perform retrieval Q&A from multiple PDF documents. It supports multiple language models OpenAI and local Falcon. If you don't have an OpenAI key, by default, it selects local Falcon language model. Note: Local LLM will be slow if you have limited memory on your laptop (recommend RAM >= 16GB)

## How the project rag is structured?
Jupyter notebooks are in the rag directory. 

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

# Load your own PDF
1. Delete PDFs under ./source
2. Copy your PDFs to ./source
3. Run 'Jupyter Lab'
4. Open 'loaddb.ipynb'
5. Execute all cells in 'loaddb.ipynb'
6. In command line, run 'panel serve chatbot.ipynb'. Now, you can retrieve information from your own PDFs. 
   
# Troubleshooting
* If it is the first time running chatbot.ipynb, it will take awhile because the notebook is going to download the local language model, ~4.2GB.
* When you load the chatbot interface(http://localhost:5006/chatbot), it will take a couple of seconds because it is trying to load the ChromaDB and Local language model. 
