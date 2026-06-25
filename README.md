# 🥗 RAG Ablation Study: Mediterranean Diet Q&A System

## 📖 Introduction
This project aims to build a Retrieval-Augmented Generation (RAG) Question & Answering system specifically tailored to Mediterranean diets and recipes. To explore the most efficient RAG architecture under limited computational resources, we conducted a comprehensive **Ablation Study** using **lightweight models** across four core stages: Chunking, Embedding, Retrieval, and Prompt Assembly.

Through a rigorous quantitative evaluation framework, we successfully identified an optimal combination of models and strategies that significantly reduces computational overhead while maintaining high generation quality.

## 👥 Team & Contributions
This project is a collaborative effort by a multidisciplinary team. The core members and their engineering contributions are as follows:

- **Yixuan Wang (Core Architecture & Data Engineering Lead): Directed the overall RAG system architecture and end-to-end pipeline integration. Solely responsible for building the underlying corpus, which included automated web scraping, multi-dimensional data cleaning, and structured extraction. Independently designed and implemented the core strategies for the text chunking phase.
- **Ziwei Wan (Algorithm Evaluation & Co-Architect): Participated in the collaborative design of the top-level system architecture and assisted with early-stage data preprocessing. Spearheaded the critical tasks of LLM information mapping and quantitative testing. Independently handled the selection and feature extraction of the Embedding models, and led the development of the project's fully automated Evaluation benchmark framework.
- **Yangce Chen (Retrieval & Prompt Engineering Lead): Focused on optimizing the RAG system's context recall rate and generation quality. Designed and implemented multidimensional ablation studies for the Retrieval algorithms and deeply fine-tuned the assembly logic for structured Prompts. Additionally, managed the computational resources for the LLM foundation models and ensured the seamless integration of API endpoints.

## 📊 Dataset
The dataset for this project was built from scratch, focusing on the traditional recipes and culinary culture of Mediterranean countries:
- **Corpus Sources**: Raw text data scraped and cleaned from Wikibooks (Cookbook), Wikipedia, and 80Cuisines using Python.
- **Full Corpus**: A total of **83** structured recipe documents were merged and cleaned (A sample `Background_Corpus.json` is provided in this repository for demonstration).
- **Benchmark Dataset**: `RAG_Benchmark_Dataset.json`, containing **300** manually curated/generated QA pairs tailored to Mediterranean recipes for final system evaluation.

## 💻 Hardware & Environment
To ensure full reproducibility, both the benchmark testing and LLM inference were executed on the following local hardware setup:
- **Device**: ASUS Tianxuan 2
- **CPU**: AMD Ryzen 7
- **GPU**: NVIDIA GeForce RTX 3060 (6GB VRAM)
- **Python Version**: Python 3.13
- **Core Dependencies**: PyTorch, Transformers, Sentence-Transformers, FAISS, Ragas, LangChain

## 🗂️ Project Structure
The project workflow is divided into 7 core modules, covering data preparation, baseline construction, ablation studies, and evaluation:

- `Crawler_Part.ipynb`: Web scraping and data cleaning module. Extracts structured fields (e.g., Ingredients, Procedure) from HTML and merges them into a unified JSON corpus.
- `1Main_Pipeline.ipynb`: **Baseline Model**. Implements a standard RAG pipeline: Contextual Chunking + BAAI Embedding + L2 Distance Retrieval + Standard Context Prompting.
- `2Chunking_Strategy_Variation.ipynb`: **Ablation Test 1**. Compares Fixed-length chunking (500 chars) against the baseline contextual chunking.
- `3Embedding_Model_Variation.ipynb`: **Ablation Test 2**. Evaluates the vector representation quality of the lightweight `all-MiniLM` model against the baseline BAAI model.
- `4Retrieval_Algorithm_Variation.ipynb`: **Ablation Test 3**. Tests the impact of Cosine Similarity versus the baseline L2 Distance on retrieval recall.
- `5Prompt_Assembly_Variation.ipynb`: **Ablation Test 4**. Compares the LLM generation quality between hard text concatenation and structured context formatting.
- `Evaluation.ipynb`: Utilizes the **Ragas Framework** to perform quantitative evaluations on the generated `Rag_result_*.json` from all pipelines.

## 🔬 Key Findings
By comparing the outputs of the 5 pipelines, we concluded the following:

1. **Chunking Strategy**: Fixed-length chunking outperformed contextual chunking, elevating the baseline score from 0.6759 to **0.7002**.
2. **Embedding Model**: The lightweight `all-MiniLM-L6-v2` yielded better representation quality for our corpus than the baseline `BAAI/bge-small-en-v1.5`, improving the score to **0.6933**.
3. **Retrieval Algorithm**: Cosine Similarity demonstrated better retrieval accuracy compared to L2 Distance, raising the score to **0.6827**.
4. **Prompting Engineering**: The baseline's structured context formatting (0.6759) significantly outperformed the brute-force hard concatenation method (0.6653).
5. **Optimal Lightweight Architecture**: Based on comprehensive evaluations, the best configuration for this project is: **Fixed-length Chunking + all-MiniLM-L6-v2 Embedding + Cosine Similarity + Structured Context Prompting**.

## 🚀 Quick Start

### 1. Clone the Repository
```bash
git clone https://github.com/wanziwei677-netizen/rag-ablation-study.git
cd rag-ablation-study