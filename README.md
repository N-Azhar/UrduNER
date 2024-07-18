# UrduNER
Fine-tuning RoBERTa to perform Named Entity Recoginition (NER) on Urdu text.

## Fine-tuning Dataset
The dataset used to train the model for NER of the Urdu news is called the MK-PUCIT corpus which was developed by S. Kanwal et al. in the research article titled ["Urdu named entity recognition: Corpus generation and deep learning applications"](https://dl.acm.org/doi/abs/10.1145/3329710) as an extention of the KPU-NE dataset by M. Kamran Malik in the research article titled ["Urdu Named Entity Recognition and Classification System Using Artificial Neural Network"](https://dl.acm.org/doi/abs/10.1145/3129290). It is composed of 926,776 tokens out of which 99,718 are NE tokens. There are a total of 3 NE types, namely, **Person**, **Location**, **Organization**, and the rest are tagged Other. It is currently the largest corpus publically available to train NER models for Urdu, which is why I chose it for this task.

## Models Used
1. [muril-base-cased:](https://huggingface.co/google/muril-base-cased) The MuRIL (Multilingual Representations for Indian Languages) model, developed by Google, is a BERT-based language model pre-trained on a diverse dataset encompassing 17 Indian languages (including Urdu) and their transliterated counterparts. The model, named muril-base-cased, is built upon the BERT base architecture and trained from scratch using a comprehensive corpus derived from various sources, including Wikipedia, Common Crawl, PMINDIA, and Dakshina.
2. [roberta-urdu-small:](https://huggingface.co/urduhack/roberta-urdu-small) Developed by [Urduhack](https://github.com/urduhack/urduhack) (NLP library for Urdu language), this language model is specifically tailored for the Urdu language, with a model size of 125 million parameters. it is trained on a corpus of Urdu news data sourced from Pakistani news resources.
