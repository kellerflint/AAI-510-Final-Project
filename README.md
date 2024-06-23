# Stellar Scout: Model Development and Evaluation for Exoplanet Identification

This project aims to develop a machine learning model that can predict the probability of an object being an exoplanet based on data from NASA's Exoplanet Archive.  

The objectives of the project are to:  
1. Analyze and pre-process the data from the K2 Planets and Candidates table *(see the "data_prep" notebook for details)*.
2. Investigate and develop regression models that can output the probability of an object being an 
exoplanet based on the selected features *(see "lg_models", "dt_models", and "nn_models" notebooks for details)*.
3. Evaluate and compare the performance of the models using appropriate metrics to determine which were most successful in exoplanet identification.

The data is from NASA's Exoplanet Archive, primarily the K2 and Kepler Planets and Candidates tables. The target variable is the "Archive Disposition" column which 
contains a classification of whether the object was positively or negatively identified as a planet or if it has yet to be determined.

# Contributors

- Ethan Schmitt (https://github.com/EthanSchmitt7)
- Keller Flint (https://github.com/kellerflint)
- Tyler Clinscales (https://github.com/tylerkc)

# Evaluation

In order get a complete understanding of each model's performance, we used a variety of visualization tools and metrics including log loss, accuracy, ROC, calibration curve / integrated calibration index, and histograms of predicted probabilities.

Assessing the models only on standard binary classification metrics such as accuracy, confusion matrices, and F1 scores was not sufficient because our project focuses on providing accurate probabilities, not just classifications. The goal of our models is not to remove human involvement and let the machine make a decision, but to help focus attention and resources in the most promising areas by providing an accurate estimate of positive exoplanet identification.

# Conclusion

While all of the models showed some level of predictive accuracy, the logistic regression approach (with an accuracy of 83.48%) was far less effective than the others we evaluated. We suspect this is due to some level of non-linearity present in the data as approaches using decision trees and neural networks both proved much more capable in this regard. Ultimately, neural networks were the most accurate at classification (with accuracy of 95.31%) beating out both decision tree models by about 5% (random forests with an accuracy of 90.25% and gradient boosting with an accuracy of 90.34%).  

Despite their classification accuracy, it appears that neural networks may be somewhat less capable of giving accurate probabilities than other models. The calibration curve and integrated calibration index suggest that random forests and logistic regression were more capable of providing probability estimates that aligned well with the actual ratio of positive to negative classifications for a given range. Gradient boosting does not seem like a good approach for this problem as it's slight increase in accuracy comes a the cost of a significant drop in its ability to predict probabilities.

Based on the observed metrics, we believe that neural networks and random forests may both be potentially useful for exoplanet identification. Neural networks are very accurate, but the predicted probabilities histogram also shows that they have a tendency to be more confident in their predictions and can lean more towards the extremes. Random forests still provide good classification accuracy but with a more balanced probability distribution which could be more appropriate if the primary goal is a probability estimate.

# Application: Predicting the Probability of Candidate Exoplanet Confirmation

Our model was trained only on exoplanets that had been definitively confirmed or refuted. However, the goal of the project is to apply it to candidate plants to give professionals working on identification a metric to help understand the likelihood of a positive classification.  

To demonstrate this capability, we've run the predictions on the list of candidate exoplanets for which sufficient information was available for. Our models suggest that approximately 426 to 681 out of 1,875 candidates are highly likely to be confirmed as exoplanets. Using the probabilities predicted by our model, resources could be directed to rapidly identifying these objects rather than working through the roughly 70% of candidates that are much less likely to be positively identified.
