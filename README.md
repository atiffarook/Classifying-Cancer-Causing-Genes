# Classifying Cancer Causing Genes

## I. Background 
Successful discovery of cancer-driving genes, such as tumor suppressor genes (TSGs) and oncogenes (OGs), is crucial to preventing, diagnosing, and treating cancer. In this project, we will use statistical methods that we have learned in this course to identify both TSGs and OGs. We will use a comprehensive gene feature dataset as our training set. The predictors are various features of the genes. The response under study involves three classes: a gene being OG, TSG or NG. If we can have an accurate prediction of the class of genes, we can use this model to discover new TSGs and OGs, which will be very useful in cancer diagnosis.

## II. Processing
### 1. Cleaning and Transforming Our Data
Since the data did not contain any NA values, we did not need to significantly clean the data. In addition, since we did not use a KNN model, we did not need to standardize or transform the predictors. Instead, our main preprocessing was choosing which predictors to use in our model. While it would have been possible to create a model with all 96 available predictors, such a model would be both computationally expensive and fraught with multicollinearity. Thus, to select predictors, we first looped through all pairs of predictor variables and excluded predictor pairs with high correlation (based on a threshold of 0.8).

### 2. Feature Selection and Cross Validation
To select our final predictors from this list of potential variables, we first created a logistic regression model with all predictors and then identified the predictors that have coefficients with extremely significant p-values (< 0.00001). Then, we applied cross validation to create a multinomial regression model with all predictors, and similarly identified the predictors with coefficients with significant p-values. We combined these lists of predictors to create a concise dataset with only these 13 predictors and the “class” variable.

### 3. Visualizing the Variables
After reducing our dataset, we conducted exploratory data analysis by constructing scatter and jitter plots for each predictor variable (Appendix a.) against the different classes to understand their distribution. We also created side-by-side boxplots ((Appendix b.) to inspect the distribution of predictors segmented by class, which allowed us to identify predictors that varied notably by class and were thus likely associated with class.

### 4. Further reduction using Cross Validation, Loops and Combinations
After completeing the processing above, we were left with 13 variables (Appendix c.). To further reduce the number of variables we created a loop that models and tests every possible combination of the 13 selected variables. That is, the code loops through every combination of predictors where n = 1,2, 3, . . . , 13, and n
outputs a list of coefficients and probabilities based on simple threshold values and then finally returns an test error rate. Based on the results from this loop we were able to further reduce our model to 8 variables.

## III. The Model
We used a multinomial regression model, built using the multinom function from the nnet package on 70% of the training data. We ultimately used 8 predictors. The R Source Code file shows how we created the model and you can find coefficients we used in the Report file.  
