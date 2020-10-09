# gold-recovery
Build model that predicts the amount of gold that can be recovered from gold ore
The data can be found here www.kaggle.com/dataset/43fc6fcc1e372c56bbe1504fc075d3f2b831e4c165e1273b259f5839f9dc5fcf. \
Some parameters are not available because they were measured and/or calculated much later. That's why, some of the features that are present in the training set may be absent from the test set. The test set also doesn't contain targets.

Recovery calculation:
- To simulate the process of recovering gold from gold ore we will use the following formula:

> Recovery = C\*(F-T)/(F\*(C-T))\*100

C — `rougher.output.concentrate_au` (for finding the rougher concentrate recovery)/ `final.output.concentrate_au` (for finding the final concentrate recovery) \
F — `rougher.input.feed_au`(for finding the rougher concentrate recovery)/ `primary_cleaner.output.concentrate_au` (for finding the final concentrate recovery) \
T — `rougher.output.tail_au`(for finding the rougher concentrate recovery)/ `final.output.tail_au` (for finding the final concentrate recovery)

Evaluation metric:\
We will use sMAPE(symmetric Mean Absolute Percentage Error).\
We need to predict two values: \
rougher concentrate recovery `rougher.output.recovery`
final concentrate recovery `final.output.recovery` \
Final sMAPE = 25% sMAPE(rougher) + 75% sMAPE(final)

Step 1: Prepare the data
- Check that recovery is calculated correctly.
- Analyze the features not available in the test set.
-  Perform data preprocessing.

Step 2:Analyze the data
- Take note of how the concentrations of metals (Au, Ag, Pb) change depending on the purification stage.
- Compare the feed particle size distributions in the training set and in the test set. If the distributions vary significantly, the model evaluation will be incorrect.
- Consider the total concentrations of all substances at different stages: raw feed, rougher concentrate, and final concentrate.Describe the findings and remove anomalies.

Step 3: Build the model
- Write a function to calculate sMAPE
- Train different models. Evaluate them using cross-validation. Pick the best model and test it using the test sample. Provide findings.
