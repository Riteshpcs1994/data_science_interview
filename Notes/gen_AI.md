## 1.What key metrics do you use to measure the effectiveness of LLM guardrails in production?

- **Safety & Compliance**: toxicity rate, policy violations, and PII leakage.
- **Factuality**: hallucination rate, faithfulness, and groundedness against retrieved documents.
- **Robustness**: prompt-injection and jailbreak success rates.
- **Operational**: schema compliance, refusal accuracy, p95 guardrail latency, and cost per request.
These were continuously monitored through dashboards and alerts.

```
User Input
   ↓
Input Guardrails (prompt injection, PII check)
   ↓
LLM (GPT / Azure OpenAI / LLaMA)
   ↓
Output Guardrails
   ↓
Content-Safety Classifier (toxicity, hate, abuse)
   ↓
Decision Engine (thresholds)
   ↓
Safe Response / Block / Rewrite
```

## 2. What does **Recursive** mean in RecursiveCharacterTextSplitter?
Try to split the text nicely first.
If it’s still too big, split it again in a more aggressive way.
Keep doing this until the text is small enough.

## 3. What is mean by **correct chunking** ?
Firtly **correct** does not mean perfect. It means **fit-for-purpose**.
I feel like perfect chunking is impossible.
Because:
1.  Language is fuzzy.
2.  Topics overlap.
3. Different questions need different boundaries.

Chunking is **perfect** if it satisfies these 3 goals:

1. `Semantic coherence` : Each chunk should talk about one main idea. If you read a chunk alone, does it still make sense?

2. `Retrieval effectiveness` : When a question is asked: 
   1. The right chunk should be retrieved.
   2. With high similarity score
   3. Without mixing unrelated topics

3. `LLM usability` : Chunks must

   1. Fit in context window
   2. Not repeat too much text
   3. Contain enough context to answer
</br>

We don’t aim for perfect chunking, but we validate that chunks are semantically coherent, retrievable, and usable by the LLM through manual inspection and retrieval-based evaluation.

## How do we do semantic chunking ?

`Semantic chunking` = splitting text where the topic changes, not where the text length ends.

How we implement using langchain we follow to step:

Step 1 : Choose an embedding model:

```
from langchain_community.embeddings.fastembed import FastEmbedEmbeddings

embed_model = FastEmbedEmbeddings(
    model_name="BAAI/bge-base-en-v1.5"
)
```

Step 2: Use SemanticChunker:
```
from langchain_experimental.text_splitter import SemanticChunker

semantic_splitter = SemanticChunker(
    embed_model,
    breakpoint_threshold_type="percentile",
    breakpoint_threshold_amount=95
)

documents = semantic_splitter.create_documents([text])
```

Step 3 : Further split large chunks

```
    size_splitter = RecursiveCharacterTextSplitter(
        chunk_size=max_size,
        chunk_overlap=overlap,
        length_function=len,
        
    )
    
    final_chunks = []
    for chunk in semantic_chunks:
        if len(chunk.page_content) > max_size:
            # Split oversized chunks
            sub_chunks = size_splitter.split_text(chunk.page_content)
            final_chunks.extend(sub_chunks)
        else:
            final_chunks.append(chunk.page_content)
```














