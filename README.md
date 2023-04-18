# Email_Reply_Transformers_Project

## Overview	(25)	
Two-minute overview providing context, stating the problem the project is addressing, characterising the approach, and giving a brief account of how the problem was addressed.

## Presentation materials	(25)	
Interactive Huggingface Spaces site using guidance text and graphics

Experiement:[(Conversation with ChatGPT on Poe.html)](https://poe.com/s/dx8Nep1p8GQviwy8S7rZ)

## Model card/dataset card	(10)	
LangChain is a tool that allows answering questions over specific documents by only utilizing the information in those documents to construct an answer. The following steps are involved in the process:

1. Load the document into memory.
2. Split the document into smaller chunks of text using the "CharacterTextSplitter" class from the "text_splitter" module.
3. Compute embeddings (i.e., vector representations) of the text chunks using the "HuggingFaceEmbeddings" class from the "embeddings" module.
4. Build an index of the embeddings using the "FAISS" class from the "vectorstores" module, allowing for efficient similarity search.
5. Find the most similar text chunks to a given query using the index and print the content of the top-ranked chunk.

## Critical Analysis	(10)	
Answer one or more of the following questions: <br>
 - What is the impact of this project? 
 - What does it reveal or suggest? 
 - What is the next step?

## Resource links	(10)	
Prepare links of where to go to get more information (other papers, models, blog posts (e.g. papers with code))

## Code demonstration	(15)	
Make a Jupyter notebook demonstrating using the model

## Repo	(20)	
Prepare a repo with a readme, notebook, links to video, resources

## Video Recording	(10)	
Record a short video recording of the overview
