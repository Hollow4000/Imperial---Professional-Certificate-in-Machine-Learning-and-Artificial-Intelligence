Reflection on Data Splits, Model Performance, and Capstone Implications

Adjusting the data-split ratio from 70:15:15 to 60:20:20 provided an instructive way to observe how the proportion of training, validation and test data affects a model’s learning capacity, reliability and generalisation. Using the wine dataset and a logistic-regression classifier, the model achieved a validation accuracy of around 94 per cent and a test accuracy of approximately 97 per cent under the 60:20:20 configuration. These results remained remarkably stable compared with the earlier 70:15:15 split, demonstrating that reducing the training size by roughly ten percentage points did not noticeably degrade the model’s ability to learn the underlying class boundaries.

Impact of the 60:20:20 Split

With 60 per cent of the data devoted to training, the model retained enough examples to estimate robust decision boundaries while gaining a larger validation subset (20 per cent) to assess out-of-sample performance during tuning. This broader validation base reduces statistical noise: every accuracy measurement becomes more representative of how the model will perform on unseen data. The consistency between validation (94 %) and test (97 %) accuracy indicates excellent generalisation and minimal overfitting. Had the validation accuracy been substantially higher than the test result, that would have suggested that hyperparameters were optimised too closely to validation data; here, both scores align, implying the model is stable and well-calibrated.

The marginal drop in training data is a worthwhile trade-off because logistic regression is relatively low-capacity—it does not require enormous sample sizes to estimate its parameters effectively. For more complex, high-variance models such as gradient-boosted trees or neural networks, a smaller training fraction might reduce accuracy more noticeably. In those cases, techniques like k-fold cross-validation could supplement a smaller validation set without sacrificing training size.

Comparison with 70:15:15 Split

Under the original 70:15:15 configuration, the model was trained on a slightly larger dataset and validated on a smaller one. The higher training proportion yielded slightly higher validation accuracy, but with greater variability when results were repeated with different random seeds. This happens because a 15 per cent validation set provides a noisier estimate of generalisation; a few misclassified samples can swing the accuracy several points. The 60:20:20 split therefore produced a more stable and reliable estimate of model performance.

More generally, increasing validation data improves the precision of performance estimates but leaves less information for model fitting. The best split depends on dataset size, model complexity, and the goal of the experiment. For the relatively small wine dataset (~180 samples), a 20 per cent validation share proved optimal. In large, real-world datasets, an 80:10:10 or even 90:5:5 split might be acceptable, since tens of thousands of examples would still remain for validation.

If the Validation Set Were Omitted

Eliminating the validation set and tuning hyperparameters directly against the test data would introduce data leakage: the model would effectively “see” the test distribution during training, producing an inflated measure of performance. This destroys the independence of the test evaluation, meaning the reported test accuracy would no longer reflect true generalisation. In professional settings, this risk translates into over-confident deployment—models may appear highly accurate in-house but fail once exposed to genuinely new client data. Maintaining a clean separation between validation (for tuning) and test (for final evaluation) is therefore essential to model integrity and reproducibility.

Applying Insights to the Capstone Project

These experiments directly inform how I will approach data management and model validation for my wealth-management capstone. In that problem, the objective is to detect product gaps in client portfolios using anonymised demographic, behavioural and holdings data. The dataset will likely be heterogeneous—combining time-dependent features, categorical client attributes and derived financial ratios—so the independence and stationarity assumptions may hold only approximately. To ensure reliability:

Dedicated validation strategy: I will adopt a 60:20:20 or rolling-time-window split, reserving a larger validation subset to evaluate generalisation under shifting economic conditions or tax-rule changes.

Cross-validation and regularisation: Using k-fold cross-validation within the training set will reduce variance in performance estimates, while L1/L2 regularisation will control model complexity and prevent overfitting to adviser-specific patterns.

Model comparison: Simpler interpretable models such as logistic regression or decision trees can establish a baseline, while ensemble models (random forests, gradient boosting) can then be evaluated against the same consistent splits to ensure improvements are genuine and not artefacts of random partitioning.

Continuous monitoring: As the wealth-management environment evolves, I will monitor validation and test metrics for drift. Re-training will be triggered when discrepancies exceed tolerance thresholds.

Conclusion

Experimenting with different data splits highlighted that model reliability depends not only on algorithm choice but also on how training data are allocated and evaluated. The 60:20:20 ratio provided a balanced trade-off between learning capacity and validation robustness, yielding stable, high accuracy without overfitting. Most importantly, these insights emphasise the ethical and professional need for honest model assessment—avoiding data leakage, maintaining independent evaluation sets, and validating performance under realistic conditions. In the capstone context, this approach will help ensure that any model recommending financial interventions for clients is statistically sound, transparent, and generalises responsibly across the evolving population of investors.
