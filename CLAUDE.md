# BPE tokenizer

Learning project following Andrej Karpathy's "Let's build the GPT Tokenizer" video.

## What this is

Implementing BPE (byte pair encoding) from scratch in Python. The goal is to understand how tokenizers like GPT-4's tiktoken work under the hood.

## File roles

- `minbpe/base.py` - base `Tokenizer` class with shared save/load logic
- `minbpe/basic.py` - `BasicTokenizer`: core BPE algorithm, built first
- `minbpe/regex.py` - `RegexTokenizer`: BPE with regex pre-tokenization (GPT-4 style)
- `minbpe/gpt4.py` - wrapper replicating GPT-4's exact tokenizer
- `train.py` - trains both tokenizers on Taylor Swift lyrics text
- `tests/test_tokenizer.py` - correctness tests

## Context

All files in `minbpe/` start as empty stubs. They are filled in incrementally as the video progresses. Do not add features or abstractions beyond what the video covers at the current point.
