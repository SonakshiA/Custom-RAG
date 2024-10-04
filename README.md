# Custom-RAG
In this notebook, I created a custom RAG (Retrieval Augmented Generator) using HuggingFace dataset (databricks/databricks-dolly-15k), HuggingFace model (distilbert/distilbert-base-cased-distilled-squad) and LangChain.

# About RAG
RAG stands for Retrieval Augmented Generator; to further demystify the term — ‘Augment’ means an addition or an increase, ‘Retrieval’ means to fetch, and ‘Generator’ is a tool that creates something. So to speak intuitively, a RAG is an addition to an LLM that aids in retrieving relevant documents and generating responses.

RAGs are instrumental in keeping LLMs updated without having to retrain them regularly. RAGs also play an important role in supplying private datasets such as enterprise data to the LLM which it may not be trained on. AI applications need to support custom data to provide its users a seamless experience — consider an AI chatbot for an e-commerce platform. The chatbot must be aware about the products and their attributes to answer item-specific customer queries accurately. One more example could be that of an internal Q&A chatbot used by employees to answer how many sick or caregiver leaves they are entitled to; which uses the organization’s HR data to respond to the employee. RAGs are baked into chatbots and enterprise knowledge engines to provide domain-specific responses at cheaper costs. Thus, RAGs play an architecturally indispensable role in the world of LLMs.

# Working of a RAG
![image](https://github.com/user-attachments/assets/69062948-fc31-44c1-9893-0c3a37b1b5ac)

Here is how a RAG works:

1. The custom documents first undergo cracking wherein the text is extracted from the documents supplied.
   
2. Next, the extracted text undergoes chunking which involves breaking the text into smaller digestible segments so that they do not exceed the LLM’s window size.
   
3. The chunked text is converted into mathematical representations called embeddings. Embeddings are vectors having weights and directions associated with them. To better understand embeddings, consider that you’re in a library with many books. An embedding is a special bookmark for the book that contains all important information about it like its genre, author, theme, and its relationship with other books. Similar to how books of the same genre might be positioned close to each other, embeddings representing similar words point toward the same direction
   
4. These embeddings are then stored in a vector database (such as Redis Cache, Pinecone, Azure AI Search, etc.). When a user gives a prompt to the LLM — the prompt undergoes chunking and is converted into embeddings. It is then sent to the vector database and the similarity measure is calculated for the prompt embedding and those stored in the database. The top ‘k’ (the value of ‘k’ depends on the implementation) embeddings having the highest similarity scores with the prompt are returned to the LLM. Similarity measures vary based on the implementation but include either finding out the Euclidean Distance between the embeddings or using cosine similarity to measure the angles between the embeddings.
   
5. Since the top ‘k’ elements have the least distance with the user’s prompt, they are the responses to the user’s queries. The LLM then generates an answer for the prompt using the embeddings retrieved.

[Read my article on RAG](https://medium.com/@sonakshi.arora02/unlocking-the-power-of-rags-a-deep-dive-into-retrieval-augmented-generation-cce8aa30eaa7)
