# PLANE: a dynamyc resource for compositional entailment :airplane: 

The repo contians the main PLANE resource, and the training-test splits used in the COLING 2022 supervised leanring experiments

## 🤗 Dataset

You can also use the train/test splits used in the supervised experiments via hugging face `datasets` library:


```py
from datasets import load_dataset

dataset = load_dataset("lorenzoscottb/PLANE-ood")
```

You can find the dataset with its card [here](https://huggingface.co/datasets/lorenzoscottb/PLANE-ood).

## 🤗 Tuned Model

A pre-trend BERT model (on the 2nd out-of-distribution split) [here](https://huggingface.co/lorenzoscottb/bert-base-cased-PLANE-ood-2?text=A+fake+smile+is+a+smile), and can be direclty used via the `transformers` library's `pipeline`

```py
from transformers import AutoTokenizer, AutoModelForSequenceClassification, pipeline

model_name = "lorenzoscottb/bert-base-cased-PLANE-ood-2"
tokenizer  = AutoTokenizer.from_pretrained(model_name)
model      = AutoModelForSequenceClassification.from_pretrained(model_name)

test_inferences = [
    "A red car is a vehicle",
    "A small cat is a small mammal",
    "A fake smile is a smile",
]

classifier = pipeline(
    task="text-classification", 
    model=model, 
    tokenizer=tokenizer,
)

predictions = classifier(test_inferences)
```

## Cite

If you use PLANE for your work, please cite the main COLING 2022 paper.
```
@inproceedings{bertolini-etal-2022-testing,
    title = "Testing Large Language Models on Compositionality and Inference with Phrase-Level Adjective-Noun Entailment",
    author = "Bertolini, Lorenzo  and
      Weeds, Julie  and
      Weir, David",
    booktitle = "Proceedings of the 29th International Conference on Computational Linguistics",
    month = oct,
    year = "2022",
    address = "Gyeongju, Republic of Korea",
    publisher = "International Committee on Computational Linguistics",
    url = "https://aclanthology.org/2022.coling-1.359",
    pages = "4084--4100",
}

```
