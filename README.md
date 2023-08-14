# RAG-PINECONE-RAY

## Build enterprise-grade Q&A at scale with Open LLMs on AWS using Pinecone and Anyscale
An example on how to use Anyscale and Pinecone on AWS to build an LLM application using Retrieval Augmented Generation (RAG).

[LlamaIndex](https://gpt-index.readthedocs.io/en/latest/) is a data framework for building LLM applications. It provides abstractions for ingesting data from various sources, data structures for storing and indexing data, and a retrieval and query interface.

[Ray](https://docs.ray.io/en/latest/) is A general-purpose, open source, distributed compute framework for scaling AI applications in native-Python.

[Pinecone](http://pinecone.io) is the long-term memory for AI

By using Ray and Pinecone with LlamaIndex, we can easily build production-quality LLM applications that can scale out to large amounts of data. 


## Example

In this example, we build a Q&A system from 2 datasources: the [Ray documentation](https://docs.ray.io/en/master/), and the [Ray/Anyscale blog posts](https://www.anyscale.com/blog). 

In particular, we create a pipeline to load the data and we retrieve the most relevant context to be included in a prompt and inferred against LLama2 70b model hosted on Anyscale Endpoint.

## Pre-requisites
Run the following commands to download the ray doc and the Anyscale website
wget -e robots=off --recursive --no-clobber --page-requisites --html-extension --convert-links --restrict-file-names=windows --domains docs.ray.io --no-parent https://docs.ray.io/en/master/
wget -e robots=off --recursive --no-clobber --page-requisites --html-extension --convert-links --restrict-file-names=windows --domains anyscale.com --no-parent https://www.anyscale.com/blog

Follow the Ray or Anyscale documentation to start a cluster. In the current example, we use a cluster with one GPU but this can be run on CPU as well.

### Step 1: Scalable Data Indexing

The first step is to load our data sources and create our data ingestion pipeline. This involves parsing the source data and embedding the data using GPUs. The embeddings are then persisted in Pinecone, a vector store.

LlamaIndex provides the abstraction for reading and loading the data, while [Ray Datasets](https://docs.ray.io/en/master/data/data.html) is used to scale out the processing/embedding across multiple GPUs.

Run `python create_pinecone_index.py` to create embeddings and load the data into Pinecone.

### Step 2: Ask the question, retrieve the contenxt, build the prompt and get answer from llama2

Run through the query.ipynb to perform the following:
- Embedd the query
- Retrieve the relevant context
- Build the prompt
- Get the answer from llama2 hosted on Anyscale Endpoint


