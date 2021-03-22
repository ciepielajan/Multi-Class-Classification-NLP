# Multi-Class-Classification-NLP

implementacja jak największej ilości algorytmów i modeli do klasyfikacji w celu przeczwiczenia predykcji i wychwycenia różnic.


maxlen = 7

nazwa| komentarz |teset Accuracy|predykcja Accuracy|predykcja F1_score
-|-|-|-|-
MLP |clean|97.89626598358154|0.97|0.97
MLP-clean-lemma |clean lemma|97.71490693092346|0.96|0.96
MLP-clean-lemma-stop_words |clean lemma stop_words|96.77185416221619|0.94|0.94
SimleRNN |clean|96.77185416221619|0.97|0.97
SimleRNN_Bidirectional |clean Bidirectional| 97.31592535972595     | 0.97|0.97
LSTM  |clean|97.1708357334137|0.97|0.97
LSTM_Bidirectional    |clean Bidirectional| 97.4247395992279     |  0.96     | 0.96
GRU     |clean|97.64236211776733|0.97|0.97
GRU_Bidirectional     |clean Bidirectional| 97.06202149391174     | 0.97|0.97
CNN | clean | 98.04134964942932 | 0.98 |0.98

