# Coding-agent-LLM-PyTorch-
A Language model trained on python code in torch.

A custom language model, built from scratch, trained on Python code for code generation and error reasoning.
Implemented tokenization, embeddings, and transformer attention in PyTorch
Built custom training loops with loss tracking and evaluation
Experimented with context length, learning rate, and dataset size
Tech: Python, PyTorch, PathLib, os Module

## ------------------------------------- ##
**Problem:**
  - big models run on the cloud, and are usually confusing to read and inaccessible
  - big Coding models are harder to run locally most of the time, and cannot use if there is no internet access

## ------------------------------------- ##
**Solutions:**
  - small model
  - everything runs locally, tokenizer, model, training, absolutely everything(pre-trained model is available in the repo).
  - everything is simplfied and documented for understanding and replicatible from any machine with a capable device.

## ------------------------------------- ##
**Technology Used:**
Python, PyTorch: allow for gpu-acceleration, tensor operations, pre-built layer types such as the Linear layers. torch speeds things up by being based on lua, which can interact with Cuda through C++ and the CPU through the C programming language
os, pathlib: used to scrape raw github repos for data and checking for file existence.

## ------------------------------------- ##
**Issues and their solution:**
1. mismatching shapes when changing hyperparameters: usually deleting an old model file works, if that doesn't changing some code usually work, but more importantly certain ratios have to be true in the hyperparameters.
2. repeating tokens: This usually stems from bad lr, no gradiant norm clipping, or not doing the masking correctly, or incorrecct data loading. those are the main issues that I identified.
3. Loss becoming low while model doesn't improve or worsens: This seemed to appear whenever I didn't mask the sequences. I infered this happens because the model just memorizes/overfits and when new data or context is introduced it doesn't know what to do. Another thing that made this work better was the warmup learning rate which allowed the weights to stabalize more easily.
4. During the data preperation into a txt file an issue with reading bytes occured, this was because the encoding type was not able to understand/decode them, which led to errors. The fix was using the UTF-8 encoding or detecting the OS encoding, the former worked better, and errors were ignored.


## ------------------------------------- ##
**The gist of the things used to actually work:**
1. The data_processor.py file scans a diretory for .py files and extracts the text into a txt file.
2. main.py then builds character-level vocabulary and creates a simple encoder/decoder functions.
3. make training samples(sliding windows), by turning all the encoded text into a long tensor and splits train/eval
4. get_batch() returns a prompt/output duo which are just x as a list of size block_size starting from a random point and y being x shifted by one.
5. 
