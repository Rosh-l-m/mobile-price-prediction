Feature Extraction and Price Prediction for Mobile Phones

Predicting the price of a mobile phone (in rupees) from its specifications, and finding out which features drive price.

Result: XGBoost predicts a typical phone within about ₹1,100 (test R² = 0.904, MAE = ₹1,126). The chipset class (Tier, Processor, Manufacturer) accounts for about 94% of what the model relies on.

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
Model	R²	MAE (₹)	RMSE (₹)	5-fold CV MAE (₹)
XGBoost	0.904	1,126	3,639	958 ± 90
Decision Tree	0.868	1,206	4,261	1,529 ± 351
Gradient Boosting	0.863	1,948	4,342	1,724 ± 116
Random Forest	0.856	1,534	4,454	1,478 ± 144
Linear Regression (baseline)	0.834	1,917	4,779	2,171 ± 376
Extra Trees	0.823	1,165	4,935	1,177 ± 225
AdaBoost	0.728	4,304	6,126	3,821 ± 245


- Roshani Mor – Data Science & AI
