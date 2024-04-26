# MA Thesis: Exploring the Relationship Between Online and Offline Sinophobia Amid COVID-19

## Abstract:

The COVID-19 pandemic has intensified global Sinophobia, leading to escalated verbal and
physical assaults on the Chinese diaspora (Cabral, 2021; Reja, 2021; Salcedo, 2021; Than,
2021). Existing research indicates that online rhetoric, especially from prominent figures,
can incite real-world racial animosity and aggression (Chan et al., 2016; Huang et al., 2022;
Williams et al., 2020). This study aims to first explore the overarching themes of online
discourse centring the COVID-19 news report in the United States, subsequently narrow-
ing its focus to the specific narratives that address China and the Chinese community to
understand how Sinophobia is manifested and associated with the pandemic. Following
the content analysis, it analyzes the temporal relationship between online Sinophobic sen-
timent and offline anti-Asian violence, accounting for the spill-over effect from targeted
anti-Chinese antipathy to a wider anti-Asian hostility. Online Sinophobia is measured by
comments on YouTube news videos about COVID-19 and Google searches for Sinophobic
terms; offline Sinophobia is assessed by FBI hate crime statistics. This study identifies
a bidirectional Granger causality between online and offline manifestations of Sinophobia
during the COVID-19 pandemic: anti-Asian hate crimes Granger-cause Google searches for
Sinophobic terms, and conversely, these searches Granger-cause offline hate crimes, with a
lag of two weeks. Additionally, it highlights a reinforcing dynamic between implicit and
explicit online Sinophobia: the volume and intensity of anti-Chinese comments on YouTube
news videos lead to increased Google searches for Sinophobic terms, and vice versa, with this
effect observable over a ten-week lag. Furthermore, when accounting for confirmed infec-
tion cases, online Sinophobia is positively correlated with offline Sinophobia. These findings
contribute to the existing literature on the relationship between online racist sentiment and
real-life racial violence amidst global crisis.


## Data:
- Original YouTube news video urls and raw comments can be found [here](https://uchicago.box.com/s/nl7a54g7ep8pqpfox8ypk59b67be62le)
- Preprocessed comments with LLM calculated hate score can be found [here](https://github.com/yuzhouw313/thesis_clean/blob/main/Data/scored_china.csv)
- Sentiment labed comments by gpt-3.5 turbo model can be found [here](https://github.com/yuzhouw313/thesis_clean/blob/main/Data/china_sentiment_df.csv)
- Infection cases of corornavirus from 2020 to 2021 can be found [here](https://github.com/yuzhouw313/thesis_clean/blob/main/Data/confirmed_cases.csv)
- FBI recorded hate crime incident statistics can be found [here](https://github.com/yuzhouw313/thesis_clean/blob/main/Data/hate_crime.csv)
- Google searches of Sinophobic terms on weekly level from 2020 to 2021 can be found [here](https://github.com/yuzhouw313/thesis_clean/blob/main/Data/google_trends.csv)

## Methods:
### 1. LDA Topic Modeling:
Latent Dirichlet Allocation is a three-tier hierarchical Bayesian model used to discover abstract topics within this collection. In LDA, documents are represented as random mixtures over latent topics, where each topic is characterized by a distribution over words. LDA can identify each topic by its top terms and examine the complete corpus by analyzing the composition of these topics. This includes determining the most prominent
topics, quantifying how many documents contain a given topic, and assessing the distribution of topics across the entire corpus. 

### 2. Hate Speech Detection: facebook/roberta-hate-speech-dynabench-r4-targe
This pre-trained large language model is provided by Huggingface based on the RoBERTa architecture, and has been fine-tuned on a dataset of text that contains instances of hate speech. Specifically, Vidgen et al. incorporates a human-and-model-in-the-loop process, enabling iterative improvements through four rounds of data generation. After calculating hate speech score, I used a hate threshold of 0.34 to determine if a given comment is a hate speech comment.

### 3. Sentiment Classification: GPT-3.5 Turbo Model 
OpenAI’s GPT-3.5 Turbo model is used to classify all comments in the corpus filtered by China-related keywords. This large language model represents a significant improvement over its predecessors due to its enhanced ability to understand and generate highly context-aware text. It facilitates precise multi-class text classification through zero-shot learning, which allows for effective categorization of comments into predefined sentiment labels without the need for additional labeled training data. This method involves custom prompt engineering to tailor the model’s capabilities to the specific needs of our sentiment analysis, ensuring accurate and detailed understanding of the nuanced public sentiments expressed in the comments.

### 4. OLS Regression
Ordinary Least Squares regression estimates the parameters of a linear regression model, aiming to find the values of the linear regression model’s parameters (i.e., the coefficients) that minimize the sum of the squared residuals. The residuals are the differences between the observed values of the dependent variable and the predicted values of the dependent variable given the independent variables. OLS algorithm assumes that the errors are normally distributed with zero mean and constant variance and that there is no multicollinearity (high correlation) among the independent variables.

### 5. VAR Model
Vector autoregression model operates by regressing each variable on its own lagged past values and the lagged values of all other variables in the system. It
generalizes the single-variable (univariate) autoregressive model by allowing for multivariate time series. The key assumptions of a VAR model are stationarity, linearity, and a constant covariance matrix of the error terms. Additionally, VAR models assume that variables in the system have a contemporaneous effect on each other, capturing the dynamic interactions within the system.

### 6. Granger Causality
To interpret the results for the VAR model, Granger-causality statistics is used to examine whether lagged values of one variable helps to predict another variable. Granger causality is a concept of causality derived from the notion that causes may not occur after effects and that if one variable is the cause of another, knowing the status on the cause at an earlier point in time can enhance prediction of the effect at a later point in time. Granger causality tests determine whether the inclusion of a second time series enhances the prediction of a first time series, implying a causal influence from the latter to the former. 
