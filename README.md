# Multi-Class-Classification-NLP



implementacja jak największej ilości algorytmów i modeli do klasyfikacji w celu przeczwiczenia predykcji i wychwycenia różnic.

## Analiza zbioru - wstępne wnioski


## Szukanie optymalnej długości dla intencji (maxlen)
[MLP_searching_optymal_maxlen](https://github.com/ciepielajan/Multi-Class-Classification-NLP/blob/main/MLP_searching%20_optymal_maxlen.ipynb)


|    |   maxlen |   Accuracy | model_name      |
|---:|---------:|-----------:|:----------------|
|  0 |        2 |    85.5277 | model_maxlen_2  |
|  1 |        8 |    98.3315 | model_maxlen_8  |
|  2 |       10 |    98.2952 | model_maxlen_10 |
|  3 |       12 |    98.4766 | model_maxlen_12 |
|  4 |       13 |    98.5129 | model_maxlen_13 |
|  5 |       33 |    98.3678 | model_maxlen_33 |

## Szukanie optymalnego proprocesingu 
base clear, lemmatyzacja, usunięcie stop_words, placehoder

nazwa| komentarz |test Accuracy|predykcja Accuracy|predykcja F1_score
-|-|-|-|-
MLP-clean |clean|97.89626598358154|0.97|0.97
MLP-clean-lemma |clean lemma|98.04134964942932|0.97|0.97
MLP-clean-lemma-stop_words |clean lemma stop_words|96.69930934906006|0.94|0.94
SimleRNN-clean |clean|96.77185416221619|0.97|0.97
LSTM-clean  |clean|97.35219478607178|0.97|0.97
GRU-clean          |clean|97.4247395992279|0.97|0.97
GRU-clean-lemma     |clean-lemma|96.30032777786255|0.93|0.93
CNN-clean | clean |  98.803049325943 | 0.98|0.98
CNN-clean-lemma  | clean-lemma  |  98.36779236793518 | 0.96|0.96

#### Implementacja różnych modeli

nazwa| komentarz |test Accuracy|predykcja Accuracy|predykcja F1_score
-|-|-|-|-
RandomForestClassifier |clean TfidfVectorizer|0.98|0.98|0.98
MultinomialNB   |clean  TfidfVectorizer|0.98|0.98|0.98
MultinomialNB   |clean  TfidfVectorizer Chi-Square |||
MLP-clean_glove.6B.100d|clean glove.6B.100d|98.25897812843323|0.99|0.99
MLP-clean_glove.6B.300d|clean glove.6B.300d| 98.404061794281 |0.99|0.99
MLP-clean_glove.twitter.27B.100d|clean glove.twitter.27B.100d|98.1864333152771|0.98|0.98
SimleRNN-clean_Bidirectional |clean Bidirectional| 97.31592535972595     | 0.97|0.97
LSTM-clean_Bidirectional    |clean Bidirectional| 97.35219478607178     |  0.97     | 0.97
GRU-clean_Bidirectional     |clean Bidirectional| 97.1708357334137     | 0.98|0.98 #1mistake


#### CNN RandomizedSearchCV
|    |   batch_size |   best_score_ |   embedding_dim |   epochs |   kernel_size |   maxlen |   num_filters |   vocab_size |
|---:|-------------:|--------------:|----------------:|---------:|--------------:|---------:|--------------:|-------------:|
|  0 |           32 |      0.982879 |             200 |       20 |             3 |       13 |           128 |         9462 |


#### CNN GridSearchCV

param_grid:
{'num_filters': [32, 64, 128], 'kernel_size': [3, 5, 7], 'vocab_size': [9462], 'embedding_dim': [100, 200], 'maxlen': [13], 'epochs': [30], 'batch_size': [16, 32, 64]}

|    |   batch_size |   best_score_ |   embedding_dim |   epochs |   kernel_size |   maxlen |   num_filters |   vocab_size |
|---:|-------------:|--------------:|----------------:|---------:|--------------:|---------:|--------------:|-------------:|
|  0 |           64 |      0.983169 |             200 |       30 |             3 |       13 |           128 |         9462 |
