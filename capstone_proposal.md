# Machine Learning Engineer Nanodegree
## Capstone Proposal
Eric Hannell

December 1st, 2017

## Proposal
Pricing items correctly in marketplaces is difficult. Too high and the seller never sells the item, too low and they leave money on the table. In this project I intend to tackle the [Mercari Kaggle competition](https://www.kaggle.com/c/mercari-price-suggestion-challenge) which aims to *"build an algorithm that automatically suggests the right product prices."* To create the model we are given user-inputted `text descriptions` of products, including details like `product category name`, `brand name`, and `item condition`.

### Domain Background
*"[Mercari](https://www.mercari.com/) is the biggest community-powered shopping app from Japan, for anyone to buy and sell anything, from anywhere, in seconds."* Helping users correctly price their items will create a better marketplace, happier users, and a more sucessful business. The aim is to predict prices by using real data from listings such as: user-inputted text descriptions of their products, product category name, brand name, and item condition. These features can be helpful in predicting the price but you can also derive other features such as key words in the product description.

I am personally interested in this Kaggle challenge since I have never completed a Kaggle competition and would like to see how I rank against others. The data also lends itself to different kinds of analysis and I would like to compare a few methods that I have learned during the nanodegree. 

### Problem Statement
For a given listing of a product we are trying to predict the price given past examples of prices for products. Since price is a a continuous variable we are going to be doing regression. We can use the features we are given and also engineer new ones. For example, there is a lot of information captured in the text input from the users (`name` and `item_description`). I will try an approach that only uses categorical features and then another that also uses the free-text features.

### Datasets and Inputs
Free-text Features:
* `name` - the title of the listing
* `item_description` - the full description of the item

Categorical features:
* `brand_name` - the brand of the product
* `category_name` - category of the listing
* `shipping` - 1 if shipping fee is paid by seller and 0 by buyer
* `item_condition_id` - provided by the seller (1 - New, 2 - Like New, 3 - Good, 4 - Fair, 5 - Poor)

Target variable:
* `price` - the USD price that the item was sold for

All of the features contain information that is relevant to the price, however the free-text fields contain information that is harder to extract and need to be processed before they can be used. I will use word embeddings which represents words using dense vectors (instead of sparse vectors like in a [bag of words model](https://www.wikiwand.com/en/Bag-of-words_model)). Using word embeddings takes into consideration the placement of the word in the sequence of words in a sentence (which is ignored in a simple bag of words model). With Keras we will basically turns words into integers, so a sentence like "great iPhone, barely used" would turn into a vector like [17, 8, 33, 4] which can be used in a neural network as an [Embedding](https://keras.io/layers/embeddings/#embedding) layer.

### Solution Statement
I want to compare a simple model to a complex one so I will create two models to solve this problem:

- First a simple solution which disregards the free-text features and only uses `brand_name`, `category_name`, `shipping` and `item_condition_id`. I will use a [decision tree regressor](http://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeRegressor.html) for this.

- Second, a neural network which uses all of the features (including the `name` and `item_description` text fields).

### Benchmark Model
I will compare their performance against a baseline model which, given a listing, simply predicts the price based on the median price for all listings with the same `brand_name`, `category_name`, `shipping` and `item_condition_id` values. A simpler model would be to take the mean of all items and use that value for all predictions, but that seems too naive. Other alternatives would be the mean price, but there are outliers so I prefer to use the median.

### Evaluation Metrics
Each model will be tested against the [test set data](https://www.kaggle.com/c/mercari-price-suggestion-challenge/data) that is provided in the Kaggle challenge and I will evaluate the results by using [mean squared error](https://en.wikipedia.org/wiki/Mean_squared_error).

For the decision tree regressor you can use [mean squared error](http://scikit-learn.org/stable/modules/generated/sklearn.metrics.mean_squared_error.html#sklearn.metrics.mean_squared_error) as a regression loss metric. The performance metric for the Keras model will also be [mean squared error](https://keras.io/losses/#mean_squared_error) which is specified when you compile the model.

### Project Design
First I will create the simple decision tree regressor. To do this I will 

In this final section, summarize a theoretical workflow for approaching a solution given the problem. Provide thorough discussion for what strategies you may consider employing, what analysis of the data might be required before being used, or which algorithms will be considered for your implementation. The workflow and discussion that you provide should align with the qualities of the previous sections. Additionally, you are encouraged to include small visualizations, pseudocode, or diagrams to aid in describing the project design, but it is not required. The discussion should clearly outline your intended workflow of the capstone project.

-----------

**Before submitting your proposal, ask yourself. . .**

- Does the proposal you have written follow a well-organized structure similar to that of the project template?
- Is each section (particularly **Solution Statement** and **Project Design**) written in a clear, concise and specific fashion? Are there any ambiguous terms or phrases that need clarification?
- Would the intended audience of your project be able to understand your proposal?
- Have you properly proofread your proposal to assure there are minimal grammatical and spelling mistakes?
- Are all the resources used for this project correctly cited and referenced?
