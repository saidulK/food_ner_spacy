# Custom Named Entity Recognition on food names based on spaCy

Created a Name Entity recognition model (using spacy) which can detect food names from text and also the default entities of the spacy model.

## Dataset preparation and preprocessing

In order to get food based sentences, used a dataset from kaggle named 'Amazon Fine Food Reviews'. The dataset contained more than 500,000 reviews on different food items. For the purpose of this project, so much data is an overkill. To gather relevant sentences from this dataset, at first a list of some common food items was created (18 foods) namely, gravy', 'ramen', 'burger', 'pizza', 'pasta', 'wings', 'coke', 'sprite', 'water','fanta','pepsi','seven up', 'biriyani','rice', 'pulao', 'bread', 'flat bread' and 'rice bowl'. Also a list of some words which are commonly used in food reviews such as 'flavour','flavours','tasty','delicious','juicy' etc. was created.

For the first 500 reviews of any food, only the ones with any of the helper words was selected and saved in a text file. In order to avoid repetition, for any food, a sentence that has name of a previously iterated food was not selected as it is already present in the file.

#### Name of the file : food_sentences.txt
#### Dataset used: ```https://www.kaggle.com/datasets/snap/amazon-fine-food-reviews```

### Annotation

The file with sentences was annotated for NER using an online annotator tool and saved to a file.

annotation file : annotations.json
online annotator : ```https://tecoholic.github.io/ner-annotator/```

## Model Training

A spacy model was trained with the processed dataset but it showed catastrophic forgetting problem. Two approaches were tried to solve the problem:

1) Revision Data: The model was trained with some data ci=onsisting of the default entities of the model. But this approach was very resource hungry and didn't yield a worthy result.

2) Pipe combination: The 'ner' pipe of the food-trained model was added before the 'ner' of the default spacy language model. This approach showed significant improvement in the result.


## Dependencies 

spacy v3, numpy, pandas

## Download and Usage

1. clone the repository

```
git clone https://github.com/saidulK/food_ner_spacy
```
2. Download reviews dataset

3. Generate dataset
```
run Dataset Generation.ipynb
```

4. Train model
```
run Train Model.ipynb
```