# Recipe summarization

This repo implements a sequence-to-sequence encoder-decoder using Keras to summarize coktails ingredients instructions by predicting a coktails title. This code is based on Siraj Raval's [How to Make a Text Summarizer](https://github.com/llSourcell/How_to_make_a_text_summarizer) and https://github.com/rtlee9/recipe-summarization


## Data
I scraped 125,000 recipes from various websites for training (additional details can be found [here](https://github.com/rtlee9/recipe-box)). Each recipe consists of:

* A Coktails title
* A list of ingredients
* Preparation instructions

The model was fitted on the recipe ingredients, instructions and title. Ingredients were concatenated in their original order to the instructions.

## Training
This model was pre-trained on a food-recipe dataset, than a final training on the coktails dataset was made. Training consisted of several training iterations, in which the learning rate is exponentialy decremented and incremented the ratio of flip augmentations.

## Sampled outputs
Below are a few _cherry-picked_ in-sample predictions from the model:

### Example 1:
* __Generated:__ Late Cocktail
* __Original:__  After Dinner Cocktail
* __Recipe:__ Apricot brandy; Triple sec; Lime; Shake all ingredients (except lime wedge) with ice and strain into a cocktail glass. Add the wedge of lime and serve.


### Example 2:
* __Generated:__ Island
* __Original:__ Cuba Libre
* __Recipe:__ Light rum; Lime; Coca-Cola ; Build all ingredients in a Collins glass filled with ice. Garnish with lime wedge ;

### Example 3:
* __Generated:__ Elizabeth
* __Original:__ Kir Royale
* __Recipe:__ Creme de Cassis; Champagne ;Pour Creme de cassis in glass, gently pour champagne on top.

## Usage (Python 3.6)

* Clone repo: `git clone https://github.com/burlamix/recipe-summarization.git`
* Initialize submodules: `git submodule update --init --recursive`
* Install dependencies: `pip install -r requirements.txt`
* Setup directories: `python src/config.py`
* Download the dataset
* Tokenize data: `python src/tokenize_recipes.py`
* Initialize word embeddings with GloVe vectors:
  * Get GloVe vectors: `wget -P data http://nlp.stanford.edu/data/glove.6B.zip; unzip data/glove.6B.zip -d data`
  * Initialize embeddings: `python src/vocabulary-embedding.py`
* Train model: `python src/train_seq2seq.py`
* Make predictions: use src/predict.ipynb

