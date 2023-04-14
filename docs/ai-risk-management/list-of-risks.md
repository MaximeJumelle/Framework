---
sidebar_position: 3
---

# List of Risks

In this section, we list a (*non exhaustive*) list of risks that may arise in the AI lifecycle. For each risk, we provide a definition with examples, as well as mitigation strategies that can be implemented to minimize or prevent the risk as much as possible.

## Risks of Datasets

The first risks we will discuss is that of datasets. Even before creating the first model, it is important to identify and address any potential risks that may arise when analyzing or processing the dataset. This is typically performed by Data Analysts or Data Scientists responsible for creating the training sets used to build models. By carefully analyzing the dataset, these experts can identify issues such as data quality issues, data bias, or data privacy concerns. These risks must be addressed before model development begins to ensure that the resulting model is accurate, reliable, and ethical.

### Bias Risk

#### Definition

Datasets can contain inherent biases that are reflected in the model's predictions. This can occur if the data used to train the model is not representative of the population intended to be modelized. Bias can occur when a subgroup of the population is overly representated that it is in the real distribution.

#### Examples

There are many examples of biaised datasets that we can find, whether they are voluntarily biased, or they are because the phenomenom is biased itself.

For example, if a facial recognition model is trained on a dataset that is predominantly male, it may not be accurate when used on people of other genders.

On the other hand, bias can also arise from the underlying phenomenon being studied. For example, suppose you are building a model to predict the likelihood of a candidate's success in an HR recruitment process. Since integration into a team is highly correlated with the team's composition, your model is based on the actual employees in the team. However, if your team has a majority of male employees, the model is likely to favor male candidates over female candidates. This is because the model is trained on a dataset that is biased towards male candidates, and it will implicitly favor males even if the organization aims to provide equal opportunities for all candidates. This is another example of biased datasets, where bias arises from the data that is collected and used to train the model. 

#### Mitigations

Solving bias in datasets is a complex problem that requires careful analysis and consideration. One of the most effective ways to reduce bias in datasets is **to collect a representative sample of data that is diverse and includes examples from a variety of sources**. However, this situation is not always possible, as data may not be diverse enough, or because the underlying phenomenom is also biased.

The first step in mitigating bias is to detect whether there is bias in the dataset. Data analysis methods can be used to identify potential sources of bias in the dataset, and measurements such as **distribution analysis of the data distribution** and **evaluation of the impact of various factors** on the model's performance can be useful in detecting bias.

Once bias has been identified, there are many possibilities that can be used to reduce it. First, data preprocessing techniques can be used to address potential sources of bias in the dataset. For example, techniques such as data cleaning, data normalization, and feature scaling can be used to address potential sources of bias in the dataset. These techniques can help reduce the impact of outliers and ensure that the dataset is consistent and reliable. Additionally, algorithmic techniques such as **oversampling, undersampling, or synthetic data generation** can be used to balance the dataset and reduce bias.

Finally, it is also important to **regularly update the dataset and retrain the model** to ensure that it remains accurate and up-to-date. This can help to reduce bias that may have been introduced due to changes in the real-world phenomenon being studied.

### Privacy Risk

Datasets can contain sensitive or confidential information that must be protected to ensure data privacy and security. This can include personal information such as names, addresses, and social security numbers, as well as financial information, medical records, and other sensitive data.

### Data Quality Risk

Having a dataset which presents a lot of quality problems (missing values, voluntarily imputed values) might impact the future quality of the model. As an example, if a subgroup of population inside the dataset does contain empty values, filling with an arbitrary value might create future bias.

### Data Drift Risk

#### Definition

The dataset can contain, directly or indirectly, variables with statistical properties that evolves over time. Since a model has been trained on a specific moment on the dataset, it might no longer be able to propose relevant answers, as some parts of the variables are not up-to-date. Technically, this situation occurs when the input's statistical distribution changed over time.

#### Examples

The first situation where data drift can occur is when the input contains at least one time variable. This situation is relatively easy to identify, as a variable would directly contain time-based values. For instance, suppose a model estimates the affluence of a grocery store, where date and time values can be considered as exogenous variables. If the model is not trained on every single day within a year, it may need frequent updates to provide accurate estimations.

The other situation where data drift can occur is when some variables are directly impacted by the effect of seasonality, with time acting as a confounding factor. For example, suppose an E-commerce company wants to predict how many users will likely purchase a specific article using AI systems. Since they have a large number of users, they only process user events from the last two weeks to compute buying probabilities. Depending on the article, user behavior may be subject to seasonality effects, such as holidays, weather, or Christmas and New Year. In this situation, if the model has been trained on a dataset generated in the middle of the year, it may not be relevant now, particularly if the article is popular during Christmas. Many examples are subject to this case when a variable is impacted by a time effect : GPS is used to predict trip duration, road traffic, as well as for hire vehicles to predict the price. The housing market is also dependent on many confounding factors that evolve over time, such as inflation, global liquidity of banks, or social tendencies.

#### Mitigations

Usually, preventing data drift only requires **regularly updating the dataset and retraining the model**. In this situation, the dataset will be able to capture the new effects that time would have over input variables. However, even when using automated pipelines to update the model without human intervention, statistics and visualizations still need to be performed as post-building monitoring.

### Concept Drift Risk

#### Definition

During the modeling process, it is possible that the dataset becomes outdated and no longer reflects the current state of the phenomenon being studied (what we try to reproduce). In this case, the resulting model may attempt to reproduce a phenomenon that is no longer representative of reality, leading to inaccurate predictions and unreliable results. This problem arises when the target variable is no longer relevant for the underlying phenomenon.

#### Examples

One notable example of this is spam detection, where the definition of spam has evolved significantly over the years : a 2010’s spam is not the same as a 2020’s spam. This is what happens when models are trained on outdated definitions and are then unable to accurately detect modern spam.

In the case of fraud detection, a model can be trained on a dataset of historical fraudulent transactions to predict new instances of fraud. However, since fraudsters are constantly adapting their tactics, the patterns of fraudulent activity may change over time, causing the model to become less accurate over time. This is an example of concept drift, as the definition of a fraud evolved with the new patterns fraudsters developed.

Another example of concept drift that has emerged with the rise of social networks is the definition of cyberbullying. Sentiment analysis algorithms were initially developed to detect cyberbullying in conversations. However, with the increasing use of the internet and the vast range of communication methods available, sentiment analysis is no longer sufficient for flagging comments or chats as cyberbullying. Over time, slang, dark humor, and cultural norms have evolved, making it more difficult for models to accurately detect instances of cyberbullying. This can lead to an increase in false positives and a decrease in the model's effectiveness.

#### Mitigation

To mitigate the risk of models becoming outdated due to concept drift, it is essential **to regularly update the dataset and retrain the model**. However, unlike data drift which can be solved without not much attention, monitoring for concept drift **requires the expertise of domain experts**, as it is not a metric that can be easily measured. Concept drift refers to the shift between the dataset and the underlying phenomenon being studied, rather than a shift within the dataset itself. As such, experts can adequatly identify situations where a concept drift might occur, and ask to collect new data.

## Risks of Models

### Performance Risk

If a model does not perform enough on the testing set, it can be unsure whether outputs are relevant or not according to the training set, which can lead to erroneous outputs.

### Robustness Risk

If the model is not able to generalize its predictions outside the training set, it might not produce relevant outputs on unseen data instance emaning from the same population of the training set. As an example, in fraud detection, the model would not be able to detect a fraud even if the pattern is close to existing ones, because the model is too fitted to specific key patterns for each fraud strategy.

### Fairness Risk

The model might have learned discriminatory bias on the training set and reproduces them. For example, in a KYC context, a model that would reject women more frequently than men would not be fair towards women.

### Stability Risk

If the model is not able to take into account small perturbations applied on data instances, it might generate wrong outputs. For example, in life insurance, a model would accept to cover a person of 60 years old, but refuse to cover the same person with the age of 59 years old.

### Data Criticisms Risk

If the model does not succeed to produce relevant outputs for data criticisms, they can have negative impact if it encounters a future data instance that is close to a data criticism. For example, in the case of fraud detection, the model is not able to detect a certain type of fraud as it was not representative enough in the training set.

## Risks of Services

### Availability Risk



### Costs Risk

Inferences of models, especially for LLM or Computer Vision model, can induce unexpected costs.

### Security Risk

When a model is deployed in production, it is vulnerable to various types of attacks such as adversarial attacks, where an attacker attempts to deceive the model by making small changes to the input data. For instance, in the context of autonomous vehicles, an attacker could add specific random noises to the camera's input to make a stop sign appear as a speed sign, causing the vehicle to accelerate instead of stopping. Adversarial attacks can also occur in other contexts, such as natural language processing or facial recognition systems, where an attacker could manipulate input data to produce false outputs.