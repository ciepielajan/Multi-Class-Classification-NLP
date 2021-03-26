# Multi-Class-Classification-NLP



implementacja jak największej ilości algorytmów i modeli do klasyfikacji w celu przeczwiczenia predykcji i wychwycenia różnic.

## Analiza zbioru - wstępne wnioski


## Szukanie optymalnej długości dla komendy (maxlen)
[MLP_searching_optymal_maxlen](https://github.com/ciepielajan/Multi-Class-Classification-NLP/blob/main/MLP_searching%20_optymal_maxlen.ipynb)

MLP_searching _optymal_maxlen text na predykcji ! do przerobienia

|    |   maxlen |   Accuracy | model_name      |
|---:|---------:|-----------:|:----------------|
|  0 |        2 |    85.5277 | model_maxlen_2  |
|  1 |        8 |    98.3315 | model_maxlen_8  |
|  2 |       10 |    98.2952 | model_maxlen_10 |
|  3 |       12 |    98.4766 | model_maxlen_12 |
|  4 |       13 |    98.5129 | model_maxlen_13 |
|  5 |       33 |    98.3678 | model_maxlen_33 |

> za najoptymalniejszą długość komendy przyjmiemy 13 tokenów, które są zawarte w 95% wszystkich analizowanych komend

## Szukanie optymalnego preprocesingu 
base clear, lemmatyzacja, usunięcie stop_words

placehoder - do zrobienia pod glvoe tweeter

nazwa| komentarz |test Accuracy|predykcja Accuracy|predykcja F1_score
-|-|-|-|-
MLP-clean |clean|97.89626598358154|0.97|0.97
MLP-clean-lemma |clean lemma|98.04134964942932|0.97|0.97
MLP-clean-lemma_glove.6B.100d |clean lemma glove.6B.100d |97.93253540992737|0.96|0.96
MLP-clean-lemma-stop_words |clean lemma stop_words|96.69930934906006|0.94|0.94
MLP-clean-lemma-stop_words_glove.6B.100d |clean lemma stop_words glove.6B.100d|96.88066840171814|0.94|0.94
SimleRNN-clean |clean|97.27964997291565|0.97|0.97
SimleRNN-clean-lemma |clean-lemma|96.88066840171814  | 0.94 | 0.94
LSTM-clean  |clean|97.35219478607178|0.97|0.97
LSTM-clean-lemma |clean-lemma|97.13456630706787  |0.96  | 0.96
GRU-clean          |clean|97.4247395992279|0.97|0.97
GRU-clean-lemma     |clean-lemma|96.30032777786255|0.93|0.93
CNN-clean | clean |  98.803049325943 | 0.98|0.98
CNN-clean-lemma  | clean-lemma  |  98.36779236793518 | 0.96|0.96

> powyższe zestawienie pokazuje że lemmatyzacja oraz usunięcie stop_words wpływa na pogroszenie wyników. W kolejnych krokach będę stosował podstawowe czyszczenie usuwające znaki html, interpunkcje, liczby, maile, url, sprowadznie do małych liter oraz usunięcie niepotrzebnych spacji. 

## Szukanie optymalnego Embedingu 

dla ml  word2vwc doc2vec: https://towardsdatascience.com/multi-class-text-classification-model-comparison-and-selection-5eb066197568

nazwa| komentarz |test Accuracy|predykcja Accuracy|predykcja F1_score
-|-|-|-|-
ML_clean_LogisticRegression | clean | ? | ?|?   
ML_clean_LogisticRegression_word2vec | clean word2vec| ? | ?|?  
ML_clean_LogisticRegression_doc2vec | clean doc2vec| ? | ?|?     
ML_clean_SGDClassifier | clean | ? | ?|?                                 
ML_clean_RandomForestClassifier |clean TfidfVectorizer|0.98|0.98|0.98
ML_clean_MultinomialNB   |clean  TfidfVectorizer|0.98|0.98|0.98
ML_clean_MultinomialNB   |clean  TfidfVectorizer Chi-Square |||
MLP-clean |clean|97.89626598358154|0.97|0.97
MLP-clean_glove.6B.100d|clean glove.6B.100d|98.25897812843323|0.99|0.99
MLP-clean_glove.6B.300d|clean glove.6B.300d| 98.404061794281 |0.99|0.99
MLP-clean_glove.twitter.27B.100d|clean glove.twitter.27B.100d|98.1864333152771|0.98|0.98
CNN-clean | clean |  98.803049325943 | 0.98|0.98
CNN-clean_glove.6B.100d|clean glove.6B.100d| 98.51287603378296   |0.99|0.99
CNN_clean_glove.6B.100d_trainable=True |clean glove.6B.100d trainable=True| 98.36779236793518   |0.99|0.99

#### Implementacja różnych modeli

nazwa| komentarz |test Accuracy|predykcja Accuracy|predykcja F1_score
-|-|-|-|-
SimleRNN-clean_Bidirectional |clean Bidirectional| 97.31592535972595     | 0.97|0.97
LSTM-clean_Bidirectional    |clean Bidirectional| 97.35219478607178     |  0.97     | 0.97
LSTM_clean_Bidirectional_dropout=0.2   |clean Bidirectional dropout=0.2| 97.89626598358154     |  0.98     | 0.98
LSTM_clean_Bidirectional dropout=0.2 recurrent_dropout=0.3 | clean Bidirectional dropout=0.2 recurrent_dropout=0.3  |  98.11389446258545 |  0.98     | 0.98
LSTM_clean_Bidirectional dropout=0.2 recurrent_dropout=0.3 return_sequences=False kernel_initializer='he_uniform'|   clean_Bidirectional_dropout=0.2_recurrent dropout=0.3 return_sequences=False kernel_initializer='he_uniform' |  97.9688048362732 |0.97|0.97
GRU-clean_Bidirectional     |clean Bidirectional| 97.1708357334137     | 0.98|0.98 #1mistake w problematyczej klasie
GRU-clean_glove.6B.100d_Bidirectional     |clean Bidirectional|  97.24338054656982    | 0.98 | 0.98
GRU-clean_glove.6B.300d_Bidirectional     |clean Bidirectional|  98.47660660743713         |0.98 |0.98
GRU-clean_glove.6B.300d_Bidirectional     |clean Bidirectional tokenizer na defuult chyba z 5 na 10 tys (bezsensownie jest ogrnaiczać ilolść słow mają mała :P słow  |  98.47660660743713         |0.98 |0.98


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
