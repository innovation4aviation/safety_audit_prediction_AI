# safety_audit_prediction_AI

Two AI models have been implemented to predict the variation of the CMA Audit EI using:
1) Machine Learning
2) Linear regression

The variation has been defined as:
- increasing: ΔEI>10%
- stable: -10%<ΔEI<10%
- decreasing: ΔEI<-10%

About 50 states have two CMA Audit results. Among these states, 6 of them are selected as validation states: with 2 of each case (increasing, stable and decreasing). The remaining 44 states consist of 9 increasing, 22 stable and 13 decreasing.

The machine learning and linear regression models share the same input parameters:
1) The first CMA audit result. Based on this result, the variation is estimated.
2) GDP, which is strongly correlated with the air traffic and with other economic parameters such as GDP per capita and growth
3) ΔYear between two CMA Audits
4-6) Three critical elements are considered: ce6, ce3, and ce2. The selection of these three has been based on the least correlation among these elements.
The mean values of the above parameters are considered as the threshold to define the input: above the mean, the input value will be set to 1 and otherwise to 0.

#-----------------------
# machine learning
#-----------------------
For the machine learning model, the neural network consists of 3 layers with 6x6x3 neurons. As can be expected, the overfitting issue is severe. In both dropout and weight decay techniques have been tested and shown hardly improvements. To run this model, you need to run the following scripts consequently:
1) s1_EI_prepare_input, which creates input parameters (for training, validation, and application in the first block of the code)
2) s2_EI_machineLearning, which is the core code of the model
3) s3_EI_test_execute, which performs the validation of the model
4) s4_EI_application_execute, through which the prediction of the CMA Audit EI at the current or future year.

#-----------------------
# linear regression
#-----------------------
Since the machine learning model shows overfitting issue, I decided to take a step backward by considering a linear regression model. The same input and output parameters as for the machine learning model are considered. So we have 6 parameters and 50 data, and the overfitting problem should not exist for this method. The coefficient of determination is around 0.36 which is not that bad (the best possible score is 1 and a constant model that always predicts the expected value of y, disregarding the input features, would get 0.0).
1) s1_EI_prepare_input
2) s2_EI_linear_regression: constructs the model, do the validation and application at the same time
