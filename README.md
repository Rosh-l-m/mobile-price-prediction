Feature Extraction and Price Prediction for Mobile Phones

Predicting the price of a mobile phone (in rupees) from its specifications, and finding out which features drive price.

Dataset
541 phones, 12 raw columns: model, colour, memory, RAM, battery, rear camera, front camera, AI lens, screen height, processor, price.
Median price ₹13,499, average ₹16,228. Price is right-skewed (skewness 2.4). Only 8 phones cost more than ₹50,000.
Approach
Cleaning. The processor column had brand spellings, part numbers and entries that were not processors at all (for example Android, IOS, 6 Core, 208MHz). I standardised these by looking up the real chip. Prices stored as text with commas and camera values such as 13MP were converted to numbers.
Leakage check. The row-number column and PriceRange (built from price) were left out of the features.
Feature engineering. Tier (Flagship / Mid / low / other) and Manufacturer were created from the processor name only, never from price.
Models. Linear Regression (baseline), Decision Tree, Random Forest, Extra Trees, Gradient Boosting, AdaBoost and XGBoost. 80/20 train-test split (432 / 109 phones), categorical columns one-hot encoded.
Evaluation. R², MAE and RMSE on the test set, plus 5-fold cross-validation on the training set.
Results 
Result: XGBoost predicts a typical phone within about ₹1,100 (test R² = 0.904, MAE = ₹1,126). The chipset class (Tier, Processor, Manufacturer) accounts for about 94% of what the model relies on.


- Roshani Mor – Data Science & AI
