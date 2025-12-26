# Coding Agent LLM (PyTorch)

A lightweight, locally runnable language model trained on Python code, designed to demonstrate transformer fundamentals, training workflows, and applied machine learning engineering in PyTorch.

This project implements a custom language model from scratch, including tokenization, embeddings, and transformer attention, with a focus on understandability, reproducibility, and local execution.

---

## Problem

Most modern coding language models:
- Require cloud infrastructure
- Are difficult to run locally
- Are opaque and hard to understand internally
- Depend on constant internet access

This makes them inaccessible for learning, experimentation, debugging, and offline use.

---

## Solution

This project implements a small transformer-based language model that:
- Runs entirely locally (training and inference)
- Includes custom tokenization, embeddings, and attention mechanisms
- Is designed for readability and experimentation
- Can be replicated on any machine with sufficient compute
- Includes a pretrained model for immediate testing

The goal is not state-of-the-art performance, but clear implementation and practical understanding.

---

## Key Features

- Custom character-level tokenizer
- Transformer-based architecture implemented from scratch
- Training loop with loss tracking and evaluation
- Masked attention to prevent information leakage
- Learning rate warmup for training stability
- Hyperparameter experimentation (context length, learning rate, dataset size)
- Local-only execution with no external services

---

## Technology Used

- **Python**
- **PyTorch** – GPU acceleration, tensor operations, neural network layers
- **os, pathlib** – filesystem access and dataset preparation

---

## How to Run

1. Clone the repository:
git clone https://github.com/Waelalzoub1/Coding-agent-LLM-PyTorch-
cd Coding-agent-LLM-PyTorch-


2. Install dependencies:
pip install torch


3. Prepare training data:
- `data_processor.py` scans a directory of `.py` files and extracts text into a single `.txt` dataset.

4. Train the model:
python main.py


5. Run inference:
- A pretrained model is included in the repository for testing without retraining.

---

## Architecture Overview

- `data_processor.py`
- Scans directories for Python files
- Extracts and aggregates source code into a text dataset

- `main.py`
- Builds a character-level vocabulary
- Implements encoder/decoder mappings
- Creates training samples using sliding windows
- Splits data into training and evaluation sets
- Trains the transformer model using masked attention

Training samples are generated as `(x, y)` pairs, where:
- `x` is a sequence of tokens of length `block_size`
- `y` is the same sequence shifted by one token

---

## Engineering Challenges & Solutions

- **Shape mismatches when changing hyperparameters**  
Occurred when loading incompatible saved model states. Resolved by retraining or maintaining valid dimensional ratios across hyperparameters.

- **Repeating tokens during generation**  
Identified causes included learning rate instability, missing gradient norm clipping, incorrect attention masking, and flawed data loading.

- **Loss decreasing without meaningful improvement**  
Occurred due to missing sequence masking, causing memorization and overfitting. Resolved by implementing proper masking and learning rate warmup.

- **Encoding errors during dataset preparation**  
Byte decoding failures occurred when reading scraped files. Resolved by enforcing UTF-8 decoding with error handling.

These issues were identified through experimentation, debugging, and iterative refinement of the training pipeline.

---

## Purpose of the Project

This project is intended to:
- Demonstrate applied understanding of transformer architectures
- Show practical ML engineering and debugging skills
- Provide a clear, readable reference for how language models work internally
- Enable local experimentation without cloud dependencies

---

## Future Improvements

- Token-level or subword tokenization
- More efficient attention mechanisms
- Evaluation metrics beyond loss
- Inference API integration

---

## Author

Wael Alzoubi  
Software Developer | Python, PyTorch, FastAPI  
GitHub: https://github.com/Waelalzoub1
