# BPE Tokenizer

A Python implementation of Byte Pair Encoding (BPE).

## Project structure

```
bpe/
  tokenizer.py    - shared base class with save/load logic
  bpe_basic.py    - basic BPE tokenizer operating on raw bytes
  bpe_regex.py    - BPE with regex pre-splitting (GPT-4 style)
  gpt4.py         - replicates GPT-4's exact tokenizer via tiktoken
tests/
  test_tokenizer.py
train.py          - trains tokenizers on text and saves vocab files
notebook.ipynb    - step-by-step walkthrough of how BPE works
```

## How to use

**Train a tokenizer on your own text:**

```python
from bpe import BasicTokenizer

tokenizer = BasicTokenizer()
tokenizer.train(open("mytext.txt").read(), vocab_size=512)

tokenizer.encode("hello world")   # -> list of token ids
tokenizer.decode([...])           # -> string
tokenizer.save("mymodel")         # saves mymodel.model and mymodel.vocab
```

**Use the regex tokenizer (GPT-4 style pre-splitting):**

```python
from bpe import RegexTokenizer

tokenizer = RegexTokenizer()
tokenizer.train(text, vocab_size=512)
```

**Load a saved tokenizer:**

```python
tokenizer = RegexTokenizer()
tokenizer.load("mymodel.model")
```

**Train on the included dataset:**

```
python train.py
```

This trains both tokenizers on Taylor Swift lyrics and saves the results to `models/`.

## The three tokenizers

- **BasicTokenizer** - simplest version, runs BPE directly on raw UTF-8 bytes with no preprocessing
- **RegexTokenizer** - splits text into chunks using a regex pattern before BPE, so merges never cross word/punctuation/number boundaries. Also supports special tokens like `<|endoftext|>`
- **GPT4Tokenizer** - loads GPT-4's pretrained merges from tiktoken, output matches OpenAI's tokenizer exactly

## Tests

```
pytest tests/
```

21 tests covering encode/decode identity, GPT-4 parity, and save/load.

## Requirements

```
pip install -r requirements.txt
```
