# RAG-EDA
## Structures of the directory:
- [benchmark](./benchmark)
  - [OPR-QA.jsonl](./benchmark/OPR-QA.jsonl)
  - [openroad_documentation.json](./benchmark/openroad_documentation.json)
- [trainning_dataset](./trainning_dataset)
  - [generator_dataset](./training_dataset/generator_dataset)
    - [eda_corpus_pretrain.jsonl](./training_dataset/generator_dataset/eda_corpus_pretrain.jsonl)
    - [QA_finetuning_v1v2amend1.jsonl](./training_dataset/generator_dataset/QA_finetuning_v1v2amend1.jsonl)
  - [reranker_dataset](./training_dataset/reranker_dataset)
    - [openroad_pos_neg_backup_data.jsonl](./training_dataset/reranker_dataset/openroad_pos_neg_backup_data.jsonl)
  - [text-embedding-model_dataset](./training_dataset/text-embedding-model_dataset)
    - [embedding_contrastive_corpu.csv](./training_dataset/embedding_contrastive_corpu.csv)
