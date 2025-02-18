# UrduNER
Fine-tuning RoBERTa to perform Named Entity Recoginition (NER) on Urdu text.

## Fine-tuning Dataset
The dataset used to train the model for NER of the Urdu news is called the [MK-PUCIT](https://www.kaggle.com/datasets/safiakanwal/mkpucit-ner-dataet) corpus which was developed by S. Kanwal et al. in the research article titled ["Urdu named entity recognition: Corpus generation and deep learning applications"](https://dl.acm.org/doi/abs/10.1145/3329710) as an extention of the KPU-NE dataset by M. Kamran Malik in the research article titled ["Urdu Named Entity Recognition and Classification System Using Artificial Neural Network"](https://dl.acm.org/doi/abs/10.1145/3129290). It is composed of 926,776 tokens out of which 99,718 are NE tokens. There are a total of 3 NE types, namely, **Person**, **Location**, **Organization**, and the rest are tagged Other. It is currently the largest corpus publically available to train NER models for Urdu, which is why I chose it for this task.

## Models Used
1. [muril-base-cased:](https://huggingface.co/google/muril-base-cased) The MuRIL (Multilingual Representations for Indian Languages) model, developed by Google, is a BERT-based language model pre-trained on a diverse dataset encompassing 17 Indian languages (including Urdu) and their transliterated counterparts. The model, named muril-base-cased, is built upon the BERT base architecture and trained from scratch using a comprehensive corpus derived from various sources, including Wikipedia, Common Crawl, PMINDIA, and Dakshina.
2. [roberta-urdu-small:](https://huggingface.co/urduhack/roberta-urdu-small) Developed by [Urduhack](https://github.com/urduhack/urduhack) (NLP library for Urdu language), this language model is specifically tailored for the Urdu language, with a model size of 125 million parameters. it is trained on a corpus of Urdu news data sourced from Pakistani news resources.

## Dependencies
pandas == 2.0.3  
numpy == 1.25.2  
sklearn == 1.2.2  
huggingface-hub == 0.23.0      
datasets == 2.19.1   
seqeval == 1.2.2   
transformers[torch] == 4.40.2     
evaluate == 0.4.2    

## Fine-tuning Results
roberta-urdu-small achieved 94.19% F1-score, while muril-based-cased achieved an F1-scoe of 94.14%. 

## Findings
In the evaluation of the fine-tuned roberta-urdu-small by comparing true labels with predicted labels, it was observed that our fine-tuned model demonstrated corrective abilities by rectifying mis-classifications present in the labeled test dataset.

For instance, "نیویارک لیبر ڈیپارٹمنٹ" (New York Labor Department) should be labeled as an organization, however, in the MK-PUCIT corpus it is labeled as "Other" meanwhile our model tags "نیویارک" (New York) as "Location" while "لیبر" (Labor) and " ڈیپارٹمنٹ" (Department) are tagged as "Other". Another notable example is found in the phrase "رنبیر کی نئی کامیڈی فلم" (Ranbir’s new comedy film), where our model correctly classifies "رنبیر" (Ranbir) as a "Person," recognizing it as the name of a renowned Bollywood actor. In contrast, MK-PUCIT labels "رنبیر" as a "Location," introducing a misclassification that could impact the model's training. There are numerous such examples where the entities are misclassified in MK-PUCIT.

Some other errors are the misclassifications of punctuation marks. For example, in the train text file of the fold 2 folder, there are 365 instances where a comma is tagged as a Location, 217 instances as a Person, and 37 instances as an Organization. There are also instances of round brackets or colons being mislabeled. "لاہور"  (Lahore) is labeled as Other about 115 times instead of Location. Similar cases can be observed for many city, country, or province names within the train text file.

Based on these findings it can be incurred that a model trained on MK-PUCIT showing high accuracy or F1-score might learn the mislabeled tags in the dataset and is overfitting. Though the results of our fine-tuned model are promising yet they can be improved if a properly labeled dataset is provided to the model.

In conclusion, through analyzing the results of the fine-tuned "roberta-urdu-small" model, it was found that there are many labeling errors in the MK-PUCIT dataset. Upon further analysis of the dataset, we found that these errors are significant enough to affect a model's training. MK-PUCIT is currently the largest training corpus available for the Urdu language, and any model trained on this dataset cannot be wholly relied upon, especially for high-risk tasks like PEP analysis and stock market analysis that use NER in their processes.

## Future Work
To address the issues discussed above, we are currently fixing the errors found in the MK-PUCIT corpus and extending it by collecting data from news articles rich in named entities like locations, persons, and organizations focused mainly on Pakistan. Furthermore, we have also introduced a fourth named entity tag "Designation" for titles refering to any person in the data. Once completed, this dataset will be made publically available for the research community InshaAllah.
