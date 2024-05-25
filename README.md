# AI Zoning Project

## Introduction
This project is designed to assist in determining zoning regulations within various municipalities in the United States. The core functionality revolves around processing and responding to zoning-related questions using an AI model. The project includes several key components, each encapsulated in its respective Python file.

## Research Foundation
This project is based on the research paper "[The Costs of Housing Regulation: Evidence From Generative Regulatory Measurement](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=4627587)" by Alexander Bartik, Arpit Gupta, and Daniel Milo. The paper provides the theoretical foundation and methodology used in this project.

## Installation and Setup

### Prerequisites
- Python 3.x
- Required Python libraries (listed in `requirements.txt`)

### Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/your-repo/zoning-ai.git
   ```
2. Navigate to the project directory:
   ```bash
   cd zoning-ai
   ```
3. Install the dependencies:
   ```bash
   pip install -r requirements.txt
   ```

### Configuration
1. Create a `config.yaml` file in the project root directory based on the provided template.
2. Add your OpenAI API key and other necessary configurations in `config.yaml`.

### Running the Project
To run the main script:
```bash
python QA_Code_V7.py
```

## Table of Contents
1. [QuestionMuniPair.py](#questionmunipairpy)
2. [QA_Code_V7.py](#qa_code_v7py)
3. [Helper_functionsV7.py](#helper_functionsv7py)
4. [Context_buildingv4.py](#context_buildingv4py)
5. [Gpt_functions.py](#gpt_functionspy)

## QuestionMuniPair.py

### Overview
`QuestionMuniPair.py` contains a class `QuestionMuniPair` that processes and stores the state of every municipal question pair. This class handles the logic of processing a question related to zoning laws, fetching relevant context, and interacting with the AI model to generate answers.

### Key Components
- **Initialization**: Sets up the initial state of the object.
- **Processing Subtasks**: Manages subtask processing if the question requires multiple steps.
- **Main Processing**: Handles the main question processing, including context building and AI interaction.
- **Response Handling**: Processes the AI responses and updates the state accordingly.

### Flow Diagram
![QuestionMuniPair Process Flow](QuestionMuniPair_Process_Flow.png)

## QA_Code_V7.py

### Overview
`QA_Code_V7.py` is the main script that runs the model. It manages the overall workflow, including setting up parameters, fetching data, and invoking the processing functions.

### Key Components
- **Configuration Loading**: Loads settings from `config.yaml`.
- **Munis and Questions**: Fetches the list of municipalities and questions to process.
- **Batch Processing**: Manages batching of requests to optimize API calls.
- **Main Execution**: Controls the flow of the script, ensuring proper sequence of operations.

### Flow Diagram
![QA_Code_V7 Process Flow](QA_Code_V7_Process_Flow.png)

## Helper_functionsV7.py

### Overview
`Helper_functionsV7.py` includes a variety of utility functions that support the main script. These functions handle tasks such as loading data, managing files, and assisting with API interactions.

### Key Components
- **Data Loading**: Functions for loading question details, embeddings, and municipal data.
- **Batch Management**: Utilities for managing batch processes and tracking status.
- **Error Handling**: Functions for capturing and managing errors during processing.

### Flow Diagram
![Helper Functions Flow](Helper_Functions_Flow.png)

## Context_buildingv4.py

### Overview
`Context_buildingv4.py` is responsible for building the context that the language model sees from Retrieval-Augmented Generation (RAG). This context is critical for ensuring the model has all necessary information to provide accurate answers.

### Key Components
- **Tree Flattening**: Converts hierarchical data structures into flat lists.
- **Chunk Sorting**: Sorts text chunks based on relevance using cosine similarity.
- **Context Selection**: Selects and combines relevant text chunks to form the final context.

### Flow Diagram
![Context Building Flow](Context_Building_Flow.png)

## Gpt_functions.py

### Overview
`Gpt_functions.py` encapsulates all interactions with the OpenAI API. This includes functions for making API calls, uploading data, and retrieving results.

### Key Components
- **API Calls**: Functions for generating completions, embeddings, and managing files.
- **Batch Management**: Functions for creating, retrieving, and managing batches of API requests.
- **Embedding Management**: Utilities for working with text embeddings.

### Flow Diagram
![GPT Functions Flow](Gpt_Functions_Flow.png)



## Contributing
1. Fork the repository.
2. Create a new branch (`git checkout -b feature-branch`).
3. Commit your changes (`git commit -am 'Add new feature'`).
4. Push to the branch (`git push origin feature-branch`).
5. Open a pull request.

## Authors
- **Alexander Bartik**  
  University of Illinois at Urbana-Champaign - Department of Economics

- **Arpit Gupta**  
  NYU Stern School of Business

- **Daniel Milo**  
  New York University


## License
This project is licensed under the MIT License. See the `LICENSE` file for details.

## Conclusion
This guide provides a comprehensive overview of the Zoning AI project, detailing each major component and their roles within the system. By following the installation and setup instructions, you can get the project up and running, and start contributing to its development.

---

This README includes diagrams that can be added for visual aid. These diagrams should represent the logical flow of each component and can be created using tools like draw.io or any other diagramming software. The file paths in the flow diagrams should be updated to reflect the actual paths where the images will be stored.