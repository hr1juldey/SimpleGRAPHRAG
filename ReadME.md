# GraphRAG: Graph-based Retrieval Augmented Generation

GraphRAG is a Python implementation that combines graph theory with Retrieval Augmented Generation (RAG) to improve information retrieval and generation for large language models.

## Table of Contents

1. [Introduction](#introduction)
2. [Installation](#installation)
3. [Usage](#usage)
4. [File Structure](#file-structure)
5. [Dependencies](#dependencies)
6. [Core Components](#core-components)
7. [Detailed Function Explanations](#detailed-function-explanations)
8. [Example Usage](#example-usage)
9. [Visualization](#visualization)
10. [Limitations and Future Work](#limitations-and-future-work)

## Introduction

GraphRAG enhances traditional RAG by using graph structures to represent relationships between text chunks, enabling more contextually relevant retrieval for language model queries.

## Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/hr1juldey/SimpleGRAPHRAG.git
   cd graphrag
   ```

2. Install the required dependencies:

```bash
   pip install -r requirements.txt
   ```

## Usage

1. Prepare your text data (Markdown or PDF format).
2. Run the GraphRAG creation script:

   ```python
   python create_graph.py --input_file path/to/your/file.md --output_file path/to/save/graph.gpickle
   ```

3. Use the graph for querying:

   ```python
   python query_graph.py --graph_file path/to/graph.gpickle --query "Your question here"
   ```

## File Structure

```markdown

graphrag/
├── Example.ipynb
├── data/
│   ├── st5.md
│   └── other_text_files.md
├── graphs/
│   └── st5.gpickle
├──requirements.txt
└── README.md
```

## Dependencies

- networkx
- numpy
- matplotlib
- PyPDF2
- nltk
- rake_nltk
- ollama

## Core Components

1. **Text Processing**: Converts input text into a hierarchical structure.
2. **Graph Creation**: Builds a NetworkX graph from the processed text.
3. **Embedding Generation**: Uses Ollama to generate embeddings for text chunks.
4. **Retrieval**: Finds relevant chunks based on query similarity.
5. **Answer Generation**: Uses a language model to generate answers based on retrieved context.

## Detailed Function Explanations

### `read_file(file_path)`

Reads content from Markdown or PDF files.

Parameters:

- `file_path`: Path to the input file

Returns:

- String containing the file content

### `detect_table_of_contents(text)`

Attempts to detect a table of contents in the input text.

Parameters:

- `text`: Input text

Returns:

- List of detected table of contents entries

### `split_text_into_sections(text)`

Splits the input text into a hierarchical structure and creates a graph.

Parameters:

- `text`: Input text

Returns:

- NetworkX graph representing the text structure

### `save_graph(graph, filepath)` and `load_graph(filepath)`

Save and load graph structures to/from disk using pickle.

Parameters:

- `graph`: NetworkX graph object

- `filepath`: Path to save/load the graph

### `get_embedding(text, model="mxbai-embed-large")`

Generates embeddings for given text using Ollama API.

Parameters:

- `text`: Input text

- `model`: Embedding model to use

Returns:

- Embedding vector

### `calculate_cosine_similarity(chunk, query_embedding, embedding)`

Calculates cosine similarity between chunk and query embeddings.

Parameters:

- `chunk`: Text chunk
- `query_embedding`: Query embedding vector
- `embedding`: Chunk embedding vector

Returns:

- Tuple of (chunk, similarity score)

### `find_most_relevant_chunks(query, graph)`

Finds the most relevant chunks in the graph based on the query.

Parameters:

- `query`: Input query

- `graph`: NetworkX graph of the text

Returns:

- List of tuples containing (chunk, similarity score)

### `answer_query(query, graph)`

Generates an answer to the query using the graph and a language model.

Parameters:

- `query`: Input query

- `graph`: NetworkX graph of the text

Returns:

- Generated answer string

### `visualize_graph(graph)`

Visualizes the graph structure using matplotlib.

Parameters:

- `graph`: NetworkX graph object

<div>

<img title="graph visialisation of a sotry by Ruskin Bond" alt="GRAPHRAG" src="./plots/A_cherry_tree.png">

<div>

## Example Usage

```python
# Load a graph
graph = load_graph("./graphs/sample_graph.gpickle")

# Ask a question
query = "What is the significance of the cherry seed in the story?"
answer = answer_query(query, graph)
print(f"Question: {query}")
print(f"Answer: {answer}")
```

## Visualization

The `visualize_graph` function can be used to create a visual representation of the graph structure. This is useful for small to medium-sized graphs but may become cluttered for very large texts.

## Limitations and Future Work

1. The current implementation may be slow for very large texts.
2. Graph visualization can be improved for better readability.
3. More advanced graph algorithms could be implemented for better retrieval.
4. Integration with other embedding models and language models could be explored.

Feel free to contribute to this project by submitting pull requests or opening issues for bugs and feature requests.
