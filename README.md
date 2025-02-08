# Experimental Dynamic Research RAG

![image](book_image.jpeg)
<small>Generated from Image Playground</small>

This is a layer on top of preexisting models like LLama which helps with fuller and more accurate data through scraping the internet for related information. This is very much still in a development phase.

This can be run using any OpenAI compatible endpoint including hosts such as:
- OpenAI
- Ollama
- LMStudio

Both an embedding model and large language model will need to be served from that endpoint.

For a demo output see: ["How did the Romance Languages diverge over the years and what types of changes occurred in each of these offshoot languages?"](demo.md)

## Requirements
Developed on Python 3.11 with LMStudio as the backend
Uses the following libraries:
- beautifulsoup4
- googlesearch-python
- matplotlib
- openai
- pandas
- scipy

See [requirements.txt](requirements.txt) for a full list of dependencies and existing versions

## Default Configuration
|Key|Value|
|---|---|
|LLM|llama-3.2-3b-instruct|
|L Context Length|8192|
|Embedding|text-embedding-all-minilm-l6-v2-embedding|
|E Context Length|2048|
|Research Searches|10|
|Topic Depth|5|
|Chunk Size|100|
|Chunk Overlap|10|
|Retrieved|40|

## Understanding the architecture:
Input --> LLM (This creates more search engine queries) --> Retrieve results from the web and places into a data storage medium alongside chunking and embedding. Repeat this process until satisfied. Then use cosine similarity with the original query to retrieve the most relevant chunks. This is then passed to a "thought" pass to better digest the material. Then, a final pass over for the result that is meant to be used.

I'll have a post up on my blog pretty soon talking about how a RAG works.

## Limitations
I don't have a powerful GPU to run this on so it was designed with LLama3.2's 3b instruct model alongside being limited to a context length of 8192 tokens. This means that I cannot include as much information as I would have liked or use as logically aware models.

Furthermore, it is difficult esimating the number of tokens that I would be using. As far as I am aware, the OpenAI library does not have a way of stating how many tokens each prompt would be using until after it has been submitted so using cloud AI providers could be incredibly expensive if one is not careful.