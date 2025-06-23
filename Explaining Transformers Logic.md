# Explaining Transformers Logic

## Overview

This document explains the core logic behind Transformer-based models such as GPT, including the sequential process that occurs when a prompt is given, with a focus on attention mechanisms and token generation strategy.

---

## 1. What are Tokens?

Tokens are the basic units of text that a machine learning model (especially language models like GPT) uses to process language.<br/>
They are not necessarily words — they can be:
 - Entire words (weather)
 - Parts of words (un, believ, able)
 - Punctuation marks (., !, ,)
 - Whitespace or special symbols

### Why Use Tokens Instead of Words?
Computers can’t understand text directly. Language models need numbers, so the text is broken into tokens and mapped to numerical IDs using a tokenizer.<br/>
This gives the model a consistent and manageable way to process inputs of varying complexity.<br/>
The model learns patterns and relationships between these token IDs, not the words themselves.<br/>
Each Token has its own ID depending on the tokenizer. Behind the scenes, tokens are just numbers.<br/>


#### Example: "I love Transformers!"
*GPT-2's tokenizer (which uses Byte Pair Encoding, or BPE):

"I love Transformers!" → ["I", "Ġlove", "ĠTransform", "ers", "!"]<br/>
"Transformers" was split into Transform and ers — that's subword tokenization<br/>
Notice: The space is encoded as Ġ before a word

```python
tokenizer("Hello") ➜ [15496]
tokenizer.decode([15496]) ➜ "Hello"
```

## 2. Tokenizers and Tokenization

Tokenizers are tools that convert text into previously explained tokens — small, machine-readable pieces that a language model can understand and process.<br/>
Each model is trained with a specific vocabulary — a list of all tokens it understands. The tokenizer must match exactly what the model learned.<br/>

| Tokenizer Type           | Description                       | Used In                      |
| ------------------------ | --------------------------------- | ---------------------------- |
| Word-level               | One token per word                | Older models                 |
| Char-level               | One token per character           | Simple tasks                 |
| Subword-level            | Tokens are parts of words         | GPT, BERT, etc.              |
| Byte-Pair Encoding (BPE) | Most common method in modern LLMs | GPT-2, GPT-3, DeepSeek, etc. |

Add special tokens like <EOS> (end of sentence), <PAD> (padding), and <CLS> (classification), depending on the model's needs.

Tokenizer is Part of the Model's Identity
When you load a model from transformers, it often looks like this:

python
Copiar
Editar
from transformers import AutoTokenizer, AutoModelForCausalLM

tokenizer = AutoTokenizer.from_pretrained("gpt2")
model = AutoModelForCausalLM.from_pretrained("gpt2")
You're not just loading the model weights — you're also loading the exact tokenizer used during its training. They’re a matched pair.

---

## 2. Embedding and Attention

Each token is transformed into a vector representation (embedding). The self-attention mechanism calculates dynamic weights for each token, determining how much attention each token should pay to every other token in the sequence.

* These weights (scores) reflect how much each token influences the others.
* Tokens with higher scores have more impact on the resulting representation.
* The model processes these attention-weighted vectors to understand context.

Even though all tokens are considered simultaneously, tokens with higher attention scores have a stronger influence on the decision of the next token.

### Voting Analogy

It is like a voting system, where each token acts as a "voter" in a poll to decide which repose-token will be the next in the sequence. 
Each voter (token) casts their vote, but the votes do not have the same weight: some tokens have a higher "weight" (higher attention score) and, therefore, their opinion weighs more in the final decision.
This "weighted voting" happens in each layer of the Transformer and is dynamically recalculated as the sequence is processed.

---

## 3. Processing by Transformer Layers

Using the attention-weighted embeddings, the data is passed through multiple Transformer layers. Each layer performs mathematical operations to refine the model's understanding of the context.

### Multi-head Attention

* Each layer includes multiple attention heads.
* Each head performs an independent attention calculation.
* Heads focus on different aspects of the input, enabling the model to capture complex relationships.
* The combined outputs from all heads are merged and passed to the next layer.
  
---

## 4. Next Token Generation

Once the context is established, the model generates a probability distribution over possible next tokens.

### Sampling Techniques

1. **top_k**: Restricts the sample to the `k` most likely words (e.g. top_k=50 limits the choice to the 50 most likely words). In other words, even with sampling, it only chooses within these k words.
2. **top_p (nucleus sampling)**: Instead of limiting by a fixed number `k`, it limits the set of chosen words to the most likely ones that, together, add up to the probability `p` (e.g. 0.9 = 90%). This allows for a dynamic set of words, adapting the number of options depending on the probability distribution.
3. **temperature**: Controls the model's “degree of freedom” when choosing the next word. Low values ​​(e.g. 0.2) make the choice more conservative and predictable; high values ​​(e.g. 1.0) allow for more varied and “creative” choices.
4. **do_sample=(True or False)**: Enables stochastic sampling or random sampling, choosing the next word based on the generated probabilities, instead of always choosing the most likely word (Greedy Decoding).

If `do_sample=False`, the model uses Greedy Decoding, always selecting the most probable token.

---

## 5. Finishing The Iterative Token Generation (End Of Sequence Token ID)

Unless a stop token or a token limit, the model repeats the generation process one token at a time, using its own output as the new input context indefinitly.
A token limit may be stablished with the following parameter `max_new_tokens = n`, where `n` is your limiter. Usually models will keep generating ramble or produce incomplete or nonsensical content, burning through your tokens until this limmit is reached.
So we implement a special token that tells the model to stop, this token is called `eos_token_id` or End Of Sequence Token ID, that allows the model to terminate generation early, saving resources and makes output more natural and bounded, especially useful for chat, Q&A, or summarization.


Every tokenizer (like GPT2Tokenizer, AutoTokenizer, etc.) has a special token for the end of a sentence or document. This token is assigned an internal ID.
For example:

GPT-2 uses 50256

DeepSeek uses 32021

This token is added to the vocabulary and known as eos_token_id.

When passed to .generate(), the model:

Continually checks each newly generated token
Stops generation when the eos_token_id is generated


---

## 6. Decoding

The generated tokens are converted back into human-readable text using the tokenizer.

---

## 7. Applicability

This architecture powers most state-of-the-art NLP models, including:

* GPT series
* BERT
* T5
* RoBERTa
* DeepSeek, Falcon, Mistral, etc.

While other architectures exist (e.g., RNNs, CNNs, Mixture-of-Experts), Transformers are the dominant standard for modern AI tasks in NLP.

---

## Summary Diagram (Conceptual)

```
[Input Text]
    -> [Tokenization]
        -> [Embedding]
            -> [Multi-head Attention Layers (with voting)]
                -> [Probability Distribution for Next Token]
                    -> [Sampling with top_k, top_p, temperature, do_sample]
                        -> [Next Token]
                            -> [Repeat until end]
                                -> [Decode to Text]
```

## 8. Example
```python
def gerar_texto(prompt, max_new_tokens=50, temperature=0.2):
  ...
  outputs = model.generate(
      input_ids=inputs["input_ids"],
      attention_mask=(inputs != tokenizer.pad_token_id),
      max_new_tokens=max_new_tokens,
      temperature=0.7,
      top_k=50,
      top_p=0.9,
      do_sample=True,
      eos_token_id=tokenizer.eos_token_id
  )
```
