Building a RAG system which can answer advanced queries related to Machine Learning using standard, high-quality research papers. The bottleneck often is the retrieval part of RAG. So, a sentence transformer is fine-tuned using synthetic data to improve retrieval performance. Then, the retrieval performance of the base encoder is compared with the fine-tuned encoder using LLM-as-a-judge. The evaluation confirms that fine-tuning using synthetic queries actually improves the retrieval performance.

1. fetch_data.ipynb - scrapes data from NeurIPS proceedings, parses the html to get the paper year, title, author and abstract. Around 20,000 documents.

2. generate_queries.ipynb - Uses a T5 model to generate 3 sets of synthetic queries for each abstract.

3. finetune_encoder.ipynb - Fine-tunes a DistilBERT model on our synthetic (query, abstract) pairs, using Multiple Negatives Ranking Loss.

4. evaluate_rag.ipynb - Uses LLM-as-a-judge to score the top 3 retreivals from both the base and fine-tuned encoders. Assigns a relevancy score from 1-10 to each retrieved abstract for each query and also assigns a binary score 0 or 1. Then both the encoders are compared across mean relevancy scores and mean precision across all the retrieved abstracts. Then, the fine-tuned encoder is used in the RAG system to answer highly specific queries related to ML>

5. Currently, the retrieval only works on abstracts, it will support whole papers in the future.
