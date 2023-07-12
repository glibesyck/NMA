# Intro to Model Fitting

Fitting and comparing models to data is really the bread and butter of data analysis in neuroscience.

wrt = with respect to

We have multiple models(1) and each has parameters(2). 2 sources of questions to discuss.

Validation | Prediction | Intepret | Compare

More generally, linear model is $y = \sum\_{i} \theta_i \phi_i (\mathbf{x}) = \theta^{T}\phi (\mathbf{x})$, $\phi (\mathbf{x})$ can be non-linear in features.

Two philosophies of models: as functions (find model with small errors, minimizing errors) and as generators (find model that assigns high probability to the data, maximizing likelihood). Noise = what we can't control + what we don't care of.

MLE is great when considering independent trials of experiment. Maximizing likelihood with Gaussian noise = minimizing mean squared error. Gaussian noise is sensitive to the outliers.

Parameter uncertainty arises as we deal with limited amount of data. Generally, one assesses parameter uncertainty through bootstrapping (sample a couple of data points and repeat -> capture the distribution of model parameters).

Bias-variance trade-off (model error vs model complexity).

Two philosophies of models comparison: goodness of fit (likelihood + correction for the number of parameters; popular choice is Akaike Information Criterion (AIC), the lower the better), cross validation (training + test).

Bayesian model comparison - implicit complexity penalty by averaging over model parameters.

Matrix of (features x number of data points) is often called the design matrix.

k-fold cross validation is constructed as division of all points into k clusters and holding each cluster as test set (all others are merged into train). The same folds for different models. Leave-one-out cross validation is the extreme type where we leave one point as test (thus we will have as many trained models as data points). We should not do any preprocessing (e.g. normalization) before we divide into subsets or the held-out subset could influence the training subsets.

AIC computes how likely that we observe this particular data under this particular model. AIC estimates how much information would be lost if the model predictions were used instead of the true data. AIC only tells us relative qualities, not absolute - we do not know from AIC how good our model is independent of others. AIC strives for a good tradeoff between overfitting and underfitting by taking into account the complexity of the model and the information lost. AIC is calculated as:

$$
\mathrm{AIC} = 2K - 2 \log(\mathcal{L})
$$

where $K$ is the number of parameters in your model and $\mathcal{L}$ is the likelihood that the model could have produced the output data. With the right derivation for Gaussian noise, one can obtain:

$$
\mathrm{AIC} = 2K + n \log \left( \frac{\mathrm{SSE}}{n} \right)
$$
