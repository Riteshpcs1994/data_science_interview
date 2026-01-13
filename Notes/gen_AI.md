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



