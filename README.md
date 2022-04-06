# Predicting-Matching-Products-between-Two-E-Commerce-Websites-Zalando-and-AboutYou-Based-on-Text
## Abstract
Online shopping has become a growing and trending aspect in today’s era. The popularity of this mode of shopping has led to success and prosperity of many online platforms. It provides a varied range of choices to its customers on articles ranging from high-end fashion to daily essentials. Typically, consumers can view and select a particular product from varied online platforms as generally, many online merchants provide alike products in multiple platforms. Due to this, e-commerce websites strive to offer reliable prices to their customers to maintain their customer base and ensure their revenue growth. This project aims to assist Zalando (an e-commerce website) in identifying exact product matches across different European competitors for its hundreds of thousands of products.

The project will analyze models and methods to match the products between Zalando and AboutYou. This project only takes the textual data like a product’s Title, Color,Description into consideration. To measure the effectiveness, the overall F1 score of the implemented model is evaluated.

## Methodology
For the given project, below approach was adopted:
1. The detail of Zalando and AboutYou products present in matches_training. parquet was obtained from offers_training.parquet. Then, the products of Zalando and AboutYou were segregated into two separate CSV files.
2. The data was then pre-processed and prepared for Binary Classification.
3. Then we basically followed Divide and Conquer approach. The task of getting exact product matches between the two e-commerce websites was divided into two 
sub-tasks:
a. Binary Classification (using CNN-LSTM Model)
• In the first stage, a Binary Classifier was implemented to classify whether the two products (of "Zalando" and "AboutYou") were possible match or not.
• For the classification one product of "Zalando" was matched with a series of products of "About You". Only those products were considered that were classified as possible matches (Binary 1) by the model .
b. Ranking Mechanism:
• In the second stage, the concatenated result of Title and Colour of "Zalando" products were vectorized. Similarly, the 
concatenated result of Title and Colour of "About You" products (that were classified as possible matches by Binary Classifier in step 1b) were vectorized. Sentence 
vectorization was implemented using a pretrained multilingual Bert Model(trained on German text data).
• After vectorization, Cosine Similarity was performed between the vector of "Zalando" products and the vector of "AboutYou" products to determine the product of "About You" which has very high semantic similarity to "Zalando" product.
• This project investigates the predictive accuracy of the ML model by calculating F1 score 
F1 score =(TP)/(TP+1/2(FP+FN)).
Each abbreviation is tabulated below:
TP True Positive
FP False Positive
TN True Negative
FN False Negative

## Result
The matches_training dataset was split into train (75%) and test (25%) data. Around 8000 datapoints were taken. The main idea was to minimize the number of False Negatives (The products are actually a match, but the predicted result shows that they are not). The confusion matrix as obtained from the code is as below:
Positive (1) Negative (0)
Positive (1) 3024 (TP) 854 (FP)
Negative (0) 445 (FN) 3259 (TN)
It resulted in an F1 score of 83% . After the Binary Classification model was trained and validated, the predicted possible matches between products of Zalando and AboutYou was obtained by testing the model with unseen dataset ‘offers_test.parquet’. The final predicted result contains matching product/offer IDs of Zalando and AboutYou.

## Future Work
For future work, we can try implementing this with Siamese Twin network. Additionally, in this project , text data like title and color of the products were used to 
determine product matching. For future work, description attribute can also be used to improve the overall accuracy and F1 score. Also, we can use Image Embedding along with Text Embedding to obtain a more accurate semantic relationship between the products of Zalando and AboutYou
