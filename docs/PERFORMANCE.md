# Performance Comparison: Local vs. Cloud

| Metric | Local System (Week 2) | Cloud System (Week 3) |
| :--- | :--- | :--- |
| **Response Time** | ~7-10 Seconds | **~0.5 - 1.2 Seconds** |
| **Embedding Model** | Ollama (Llama 3) | Mixedbread-AI (via Upstash) |
| **LLM Provider** | Local CPU (Slow) | **Groq Cloud (Ultra Fast)** |
| **Data Capacity** | Limited by RAM | Scalable Cloud Storage |

### Key Observations:
- **Speed:** The Groq API is significantly faster than running Llama 3 locally on my machine.
- **Accuracy:** By increasing the descriptions in `food_data.json` to over 75 words, the AI has more context to provide detailed, professional answers.
- **Accessibility:** Unlike the local version, the Upstash database is accessible from anywhere with an internet connection.