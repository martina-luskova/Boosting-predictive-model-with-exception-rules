This thesis presents a novel hybrid approach to predictive modelling that enhances logistic
regression with exception rules. While regression-based models are widely used for their
simplicity and generalisation ability, they often fail to capture localised, non-linear patterns.
To address this limitation, the proposed algorithm integrates rule-based refinement into a
standard logistic regression model by mining exception rules using the 4ft-Miner algorithm.
These rules identify compact and interpretable subgroups in the data with elevated prediction
confidence and are used to boost the baseline model. The hybrid model is implemented in
Python and evaluated on the Telco Customer Churn dataset. The results show that while
the overall predictive accuracy of the hybrid and baseline models is comparable, performance
improved in uncertain prediction regions, instances where logistic regression predicted class
probabilities near 0.5. Notably, some individual rules showed strong generalisation and sub-
stantially outperformed the baseline model in their respective subspaces. The design also
incorporated techniques to prevent overfitting, including training-only rule mining, support
constraints, and rule complexity limits. The findings confirm that boosting predictive models
with exception rules is not only feasible but also beneficial in enhancing interpretability and
performance.

ALGORITHM:
1. Data splitting: The dataset is divided into a training and testing set using stratified
sampling.
2. Training the baseline model: A logistic regression model is trained on the training set,
and its predicted class labels and probabilities are recorded for the observations in the
test set.
3. Mining exception rules: Exception rules targeting the positive class are extracted from
the training data using the 4ftMiner algorithm, as previously described.
4. Rule transformation: The discovered rules are converted into a binary matrix represen-
tation. This matrix contains all possible values of variables recorded as dummies. For
each rule, we assign its unique identifier and a corresponding confidence value.
5. Rule application: For each observation in the test set, we check whether one or more
rules apply. If so, the maximum confidence among the applicable rules is computed and
stored in a new column together with the unique identifier of the given rule. If no rule
applies, a missing value is recorded.
6. Hybrid prediction: The confidence value of the strongest matching rule is compared with
the predicted probability produced by the logistic regression model. If the confidence of
the rule exceeds the model’s probability estimate, we use the corresponding confidence.
Otherwise, the logistic regression prediction is retained.
7. Selective evaluation: If the hybrid strategy does not improve overall accuracy in all
cases, a further evaluation focuses on the subset of instances where the logistic regression
model is uncertain. That is, where the predicted probabilities lie within a narrow
interval of around 0.5. In addition, we examine the results for each rule.
