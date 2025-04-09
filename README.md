# RAG-EDA
## Structures of the directory:
- [benchmark](./benchmark) 
  - [ORD-QA.jsonl](./benchmark/ORD-QA.jsonl) (**ORD-QA benchmark containing 90 question-reference-answer triplets**)
  - [openroad_documentation.json](./benchmark/openroad_documentation.json) (**OpenROAD documentation chunks**)
- [training_dataset](./training_dataset)
  - [generator_dataset](./training_dataset/generator_dataset)
    - [eda_corpus_pretrain.jsonl](./training_dataset/generator_dataset/eda_corpus_pretrain.jsonl) (**corpus for generator pre-train**)
    - [QA_finetuning_v1v2amend1.jsonl](./training_dataset/generator_dataset/QA_finetuning_v1v2amend1.jsonl) (**corpus for generator fine-tuning**)
  - [reranker_dataset](./training_dataset/reranker_dataset)
    - [openroad_pos_neg_backup_data.jsonl](./training_dataset/reranker_dataset/openroad_pos_neg_backup_data.jsonl) (**corpus for reranker finetuning**)
  - [text-embedding-model_dataset](./training_dataset/text-embedding-model_dataset)
    - [embedding_contrastive_corpus.csv](./training_dataset/text-embedding-model_dataset/embedding_contrastive_corpus.csv) (**corpus for text embedding model finetuning**)

## One example of QA in ORD-QA
```
{
    "id": 67,
    "type": "functionality",
    "question": " Once the design is routed, how can I estimate the parasitics?\n",
    "ref_num": 1,
    "reference": [
        "global_routing_12"
    ],
    "reference_content": [
        "id:global_routing_12\n### Estimate Global Routing Parasitics\n\nTo estimate RC parasitics based on global route results, use the `-global_routing`\noption of the `estimate_parasitics` command.\n\n```{note}\nTo see the function definition for `estimate_parasitics`, refer to \n[Resizer docs](../rsz/README.md#estimate-parasitics).\n```\n\n```tcl\nestimate_parasitics -global_routing\n```\n\n## Commands\n\n```{note}\n- Parameters in square brackets `[-param param]` are optional.\n- Parameters without square brackets `-param2 param2` are required.\n```\n\n"
    ],
    "answer": " You can estimate the parasitics after global routing by running:\\n\\n```tcl\\nestimate_parasitics -global_routing\\n```\\n\\n\n"
}
```
- id: the id of the QA.
- type: the question type. There are three question types in total, namely, *functionality*, *vlsi_flow* and *gui & installation & test*.
- question.
- ref_num: number of document(s) used for answering the question.
- reference: the id(s) of the relevant document(s).
- reference_content: the content of the relevant document(s).
- answer.

## Scoring Criterion for Query-Document Relevance

Scoring criterion for the relevance degrees between one query $q$ and one document $d$. This scoring criterion is used for generating the corpus for the LLM reranker.

| Score | Description                                                                 |
|-------|------------------------------------------------------------------------------|
| 100   | `d` is perfectly relevant to `q` and can be used to directly answer `q`.    |
| 80    | `d` is relevant to `q` and can partially answer `q`.                        |
| 60    | `d` is relevant to `q` but cannot be directly used to answer `q`.           |
| 40    | It is possible that `d` is relevant to `q`, but more information is required to verify the relevance. |
| 20    | `d` is basically not relevant to `q`.                                       |
| 0     | `d` is totally irrelevant to `q`.                                            |
