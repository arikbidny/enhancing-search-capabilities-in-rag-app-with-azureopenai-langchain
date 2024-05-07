# RAG - Query Transformation with Azure OpenAI and LangChain

Retrieval-Augmented Generation (RAG) techniques significantly enhance search functionalities in vector stores by addressing a key challenge: retrieving highly relevant answers from a vector stores. Traditional search methods often struggle with understanding the complex and nuanced nature of user queries, leading to results that might be accurate but not contextually relevant. RAG tackles this issue by merging the robust retrieval capabilities of neural networks with the nuanced understanding of language models.

## Query Translation

The concept is pretty simple, we want to take an input user question and translate it in some way in order to improve retrieval. 
The problem statement is pretty intuitive: 
Semantic search on embeddings is hard to get right. Embedding long documents is a challenge. User queries are a challenge, if a user provides an ambiguous query they'll get ambiguous matches.
LLMs just follow what was in the context and hallucinate answers as a result

## General Approaches to transform input questions

The approaches are:

- Re-Written ( RAG-Fusion & Multi-Query )
- Sub-questions ( Least-to-Most )
- Step-back question ( Step-back prompting )

For my various approaches, I will be using the same document index that was shared in my GitHub Copilot thread. 
Here is the link: https://medium.com/@arikbidny/mastering-github-copilot-essential-tips-tricks-and-prompt-engineering-for-optimal-coding-efd420864c3d

### Packeges used:

```
pip install langchain_community tiktoken langchain-openai langchainhub chromadb langchain
```

Configure .env file with the following parameters:

```
OPENAI_API_KEY=<KEY>
AZURE_OPENAI_ENDPOINT=<ENDPOINT>
```

### The Approaches

#### Multi Query

Multi Query is an advanced technique that allows us to broaden our search score by using a LLM to generate multiple queries from a single input query.

#### RAG Fusion

RAG-Fusion takes search technology a step further by employing multiple query generation and Reciprocal Rank Fusion (RRF) to re-rank search results, Its pretty similar to the previous method we saw besides the ranking step added here.

#### Decomposition

RAG decomposition is a strategy used in question-answering systems to improve the handling of complex queries, decompose problem into sub-problems, solve sequentially

#### Step-back prompting

- Step-Back Prompting (STP) is a prompt engineering technique that interfaces with a single LLM in an iterative process.
- It involves distilling the original question into a stepback question, which represents a more abstract or higher-level version of the original question.
- The answer to the stepback question serves as a prerequisite for arriving at the final answer to the original question.

#### Hyde (Hypothetical Document Embeddings)

At a high level, HyDE is an embedding technique that takes queries, generates a hypothetical answer, and then embeds that generated document and uses that as the final example.
