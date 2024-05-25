# AI Zoning Project

## Introduction
This GitHub repository hosts a project that utilizes Large Language Models (LLMs) to parse zoning documents. We introduce an innovative approach called generative regulatory measurement, which decodes and interprets statutes and administrative documents using LLMs for data collection and analysis. This tool constructs a detailed assessment of U.S. zoning regulations, estimating the correlation between these regulations, housing costs, and construction. Our work demonstrates the effectiveness and reliability of LLMs in measuring and interpreting complex regulatory datasets.

## Research Foundation
This project is based on the research paper "[The Costs of Housing Regulation: Evidence From Generative Regulatory Measurement](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=4627587)" by Alexander Bartik, Arpit Gupta, and Daniel Milo. The paper provides the theoretical foundation and methodology used in this project.

## Installation and Setup

### Prerequisites
- **Python 3.8 or higher**: Ensure Python 3.8+ is installed on your system. You can check your Python version by running `python --version` or `python3 --version` in your terminal.

### Installation
1. **Clone the Repository**:
   Clone the project repository to your local machine using the following command:
   ```bash
   git clone https://github.com/RitulSoni/Ritul-Code-Task.git
   ```
2. **Navigate to the Project Directory**:
   Change into the project directory with:
   ```bash
   cd Ritul-Code-Task
   ```
3. **Install Dependencies**:
   Install the required Python libraries listed in `requirements.txt` using pip:
   ```bash
   pip3 install -r requirements.txt
   ```

### Configuration
1. **Create a `config.yaml` File**:
   You need to create a `config.yaml` file in the root directory of the project. This file should contain all necessary paths and API keys as per the structure below:

   Here is a basic template for `config.yaml`:
   ```yaml
   embeddings: path/to/your/embeddings
   raw_data: path/to/your/raw_data
   processed_data: path/to/your/processed_data
   muni_text: path/to/municipality/texts
   exllama_path: path/to/exllama/repository
   llama13b_path: path/to/llama13b/model
   llama70b_path: path/to/llama70b/model
   openai_key: your_openai_api_key_here
   num_neighbors: 5  # or any other appropriate number
   ```

2. To create embeddings and inference, we have to configure config.yaml for

| Key                 | Description                                                              |
|---------------------|--------------------------------------------------------------------------|
| `muni_text`         | Path where the raw text of all municipalities is stored.                 |
| `embeddings`        | Path where you want to store the embeddings.                             |
| `raw_data`          | Path where the questions are present.                                    |
| `exllama_path`      | Path of the cloned exllama repository if using Llama2.                   |
| `llama13b_path`     | Path where the Llama2 13B model is downloaded.                           |
| `llama70b_path`     | Path where the Llama2 70B model is downloaded.                           |
| `openai_key`        | OpenAI API key if you are using GPT.                                     |
| `processed_data`    | Path where you want to store the inference results.                      |
| `num_neighbors`     | Optional. Determines the number of chunks of text to include in the context. |

3. **Set up Environment Variables**:
   For additional security, especially with your API keys, consider using an `.env` file to store sensitive information such as your OpenAI key. Ensure that `.env` is included in your `.gitignore` file to prevent it from being committed to your version control system.

### Running the Project
Once the configuration is set up, you can run the project by executing the main script from the command line:
```bash
python3 QA_Code_V7.py
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

### Context_Building Diagram

```mermaid
flowchart TD
    subgraph Initialize_Environment
        A1[Load Libraries]
        A2[Set Random Seed]
        A3[Load Environment Variables]
        A4[Retrieve API Key]
    end

    subgraph Setup_Directories_and_Configuration
        B1[Change Working Directory]
        B2[Load Configuration]
    end

    subgraph Load_Data
        C1[Load Question Embeddings]
        C2[Load Keywords]
        C3[Set Max Tokens]
    end

    subgraph Context_Building_Functions
        D1[Flatten Tree]
        D2[Sort Chunks]
        D3[Keyword Reranker]
        D4[Reranking Parent Function]
        D5[Semantic Reranker]
        D6[Select Chunks]
    end

    subgraph Utility_Functions
        E1[Get Embedding]
        E2[Process Text]
        E3[Get Keywords]
        E4[Load Tree]
        E5[Context Builder]
    end

    Initialize_Environment --> Setup_Directories_and_Configuration
    Setup_Directories_and_Configuration --> Load_Data
    Load_Data --> Context_Building_Functions
    Context_Building_Functions --> Utility_Functions
```

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


## Conclusion
This guide provides a comprehensive overview of the Zoning AI project, detailing each major component and their roles within the system. By following the installation and setup instructions, you can get the project up and running, and start contributing to its development.

---

## License
This project is licensed under the MIT License. See the `LICENSE` file for details.