#transformers

A **Transformer** is a type of **deep learning neural network architecture** introduced by researchers at Google in 2017. It was specifically designed to process sequential data (such as natural language) by using an **attention mechanism**, allowing every element in a sequence to directly consider every other relevant element, rather than processing them one at a time.

A formal definition from the original paper is:

> **"The Transformer is the first transduction model relying entirely on self-attention to compute representations of its input and output without using sequence-aligned RNNs or convolution."**

In simpler words:

> **A Transformer is a neural network architecture that learns relationships between all tokens in an input sequence simultaneously using self-attention, enabling efficient parallel computation and better modeling of long-range dependencies than previous sequential architectures such as RNNs and LSTMs.**


# Before Transformers

If each sentence is processed and transformed independently the model losses all sense of context
![[Pasted image 20260720224050.png]]

Earlier models like **LSTM** and **RNNs** handled this by processing one token at a time. Each step would process one token, update an internal memory and pass it to the next step. 
![[Pasted image 20260720224344.png]]

It worked but it came with two big problems. 
 - Firstly, it was sequential. That means no parallel processing, which made training slow
 - Secondly, it struggled with long-term dependency, by the time the network reached the end of a long sequence, much of the early information was lost. 
![[Pasted image 20260720224635.png]]

# After Transformers

The Transformer introduces the **Attention mechanism**, which allows all tokens in a sequence to communicate simultaneously, enabling efficient, parallel processing and superior contextual understanding
![[Pasted image 20260720224831.png]]

A transformer is a sequence of layer but its design is smarter. It adds a special layer called **attention**, which lets all tokens in a sequence talk to each other directly. 

You can think **Attention** as a communication layer built inside the network
![[Pasted image 20260720225132.png]]

**How Attention Works:** The mechanism creates **Query**, **Key**, and **Value** vectors for every token. By calculating the dot product between a _Query_ and other _Keys_, the model determines where to focus its attention, effectively weighting relevant information

## Step 1: The entire sentence enters together

If the input is:

```
I did not like it
```

The tokenizer converts it into tokens.

```
[I] [did] [not] [like] [it]
```

Each token becomes an embedding.

```
E(I)
E(did)
E(not)
E(like)
E(it)
```

These embeddings are **not processed independently**.

Instead, they are placed together into a matrix.

```
┌──────────────┐
│ I            │
│ did          │
│ not          │
│ like         │
│ it           │
└──────────────┘
```

This entire matrix enters the Transformer simultaneously.

## Step 2: Self-Attention connects every word

Now the magic begins.

When the Transformer processes **"like"**, it doesn't only see "like".

It asks:

> Which other words help me understand "like"?

It computes attention like this:

```
like
 │
 ├────────► I
 │
 ├────────► did
 │
 ├────────► not
 │
 └────────► it
```

Suppose the attention weights become

|Word|Attention|
|---|---|
|I|0.05|
|did|0.10|
|not|**0.70**|
|like|0.10|
|it|0.05|

Notice something important.

The word **not** receives the highest attention.

Therefore the representation of "like" becomes something closer to

```
NOT LIKE
```

instead of

```
LIKE
```

The model understands the negation because it looked at the surrounding words.

---

## Step 3: Every word does this simultaneously

The same happens for every token.

```
I     attends to everyone
did   attends to everyone
not   attends to everyone
like  attends to everyone
it    attends to everyone
```

Graphically,

```
          I
       ↗ ↖ ↑ ↘ ↙

did ←→ not ←→ like

       ↘ ↓ ↗ ↖ ↑

          it
```

Every token exchanges information with every other token.

This is why it is called **self-attention**.
