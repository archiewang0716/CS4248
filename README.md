# CS4248-Fake-News-Detection

CS4248 Group 23 Project: Combining Syntax- and Semantic-level Representations for Unreliable News Classification

Reference Github: https://github.com/MysteryVaibhav/fake_news_semantics

## Introduction

We have researched on some models such as BERT and LSTMs which have currently been implemented. Furthermore, we’ve started exploring different feature extraction methods (on both semantics and syntax).


## Datasets

- [Labeled Unreliable News (LUN)](https://github.com/BUPT-GAMMA/CompareNet_FakeNewsDetection/releases/tag/dataset)
- [Satirical and Legitimate News (SLN)](http://victoriarubin.fims.uwo.ca/news-verification/data-to-go/)
- [Global Vectors for Word Representation (GloVe)](https://nlp.stanford.edu/projects/glove/)

Please make sure your dataset is downloaded and placed as follows:
```
CS4248-Fake-News-Detection
│   README.md
│   *.py
│   
└───src
    │   *.py
│   
└───data
    │   balancedtest.csv
    │   fulltrain.csv
    |   test.xlsx
    |   glove.6B.100d.txt
```

## Dependencies
Python version: `3.7`

Please install dependencies by running the following command:
```
pip install -r requirements.txt
```

## Instructions
To train a CNN model, you should run the following command:
```
python main.py --batch_size 1024 --config cnn --encoder 1 --ntags 4 --mode 0
```

To train a LSTM model, you should run the following command:
```
python main.py --batch_size 1024 --config lstm --encoder 0 --ntags 4 --mode 0
```

To train a BiLSTM model, you should run the following command:
```
python main.py --batch_size 1024 --config bilstm --encoder 0 --ntags 4 --mode 0 --bidirectional
```

To train a LSTM + Attention model, you should run the following command:
```
python main.py --batch_size 512 --config lstm_att --encoder 0 --ntags 4 --mode 0 --attention
```

To train a BiLSTM + Attention model, you should run the following command:
```
python main.py --batch_size 512 --config bilstm_att --encoder 0 --ntags 4 --mode 0 --bidirectional --attention
```

To train a GRU + Attention model, you should run the following command:
```
python main.py --batch_size 512 --config gru_att --encoder 0 --ntags 4 --mode 0 --attention
```

To train a BiGRU + Attention model, you should run the following command:
```
python main.py --batch_size 512 --config bigru_att --encoder 0 --ntags 4 --mode 0 --bidirectional --attention
```

To train a LSTM + Attention + GCN model, you should run the following command:
```
python main.py --batch_size 32 --max_epochs 10 --config lstm_att_gcn --max_sent_len 50 --encoder 2 --ntags 4 --mode 0 --attention
```

To train a BiLSTM + Attention + GCN model, you should run the following command:
```
python main.py --batch_size 32 --max_epochs 10 --config bilstm_att_gcn --max_sent_len 50 --encoder 2 --ntags 4 --mode 0 --attention --bidirectional
```

To train a BERT + LSTM model, you should run the following command:
```
python bert_classifier.py --batch_size 4 --max_epochs 10 --max_seq_length 500 --max_sent_length 70 --ntags 4 --mode 0
```

If you want to use pretrained embeddings, add `--pte data/glove.6B.300d.txt --emb_dim 300` to your command to use GloVe embeddings.

You can also download our trained models in the [Google Drive link](https://drive.google.com/drive/folders/12kBrRDdM08Hp4YCxjLcYCZjjuUiiyCx4?usp=sharing).

To test the accuracy of the models, run the following command:

Evaluate the Logistic Regression model on in-domain dev set:
```
python traditional.py lr val tfidf
```

Evaluate the Logistic Regression model on out-of-domain test set:
```
python traditional.py lr test tfidf
```

Evaluate the CNN model:
```
python main.py --batch_size 1024 --encoder 1 --model_file model_cnn.t7 --ntags 4 --mode 1
```

Evaluate the LSTM model:
```
python main.py --batch_size 1024 --encoder 0 --model_file model_lstm.t7 --ntags 4 --mode 1
```

Evaluate the BiLSTM model:
```
python main.py --batch_size 1024 --encoder 0 --model_file model_bilstm.t7 --ntags 4 --mode 1
```

Evaluate the LSTM + Attention model:
```
python main.py --batch_size 1024 --encoder 0 --model_file model_lstm_att.t7 --ntags 4 --mode 1
```

Evaluate the BiLSTM + Attention model:
```
python main.py --batch_size 1024 --encoder 0 --model_file model_bilstm_att.t7 --ntags 4 --mode 1
```

Evaluate the GRU + Attention model:
```
python main.py --batch_size 1024 --encoder 0 --model_file model_gru_att.t7 --ntags 4 --mode 1
```

Evaluate the BiGRU + Attention model:
```
python main.py --batch_size 1024 --encoder 0 --model_file model_bigru_att.t7 --ntags 4 --mode 1
```

Evaluate the LSTM + Attention + GCN model:
```
python main.py --batch_size 32 --max_sent_len 50 --encoder 2 --model_file model_lstm_att_gcn.t7 --ntags 4  --mode 1
```

Evaluate the BiLSTM + Attention + GCN model:
```
python main.py --batch_size 32 --max_sent_len 50 --encoder 2 --model_file model_bilstm_att_gcn.t7 --ntags 4  --mode 1
```

Evaluate the BERT + LSTM model:
```
python bert_classifier.py --batch_size 4 --model_file model_bert.t7 --max_seq_length 500 --max_sent_length 70 --ntags 4 --mode 1
```


## Experiment Results (Not completed)

### In domain dev set accuracy (train.csv 80:20 split)
Model | Acc | Prec | Recall | F1
--- | --- | --- | --- | ---
LR  | 86.22 | 85.96 | 84.36 | 85.07 / 86.22
CNN | - | - | - | -
BERT + LSTM | 95.3 | 95.3 | 94.7 | 95.0 / 95.3
LSTM | - | - | - | -
BiLSTM | - | - | - | -
GRU | - | - | - | -
BiGRU | - | - | - | -
LSTM + Attention | 93.3 | 93.3 | 92.4 | 92.5 / 93.3
BiLSTM + Attention | - | - | - | -
LSTM + Attention + GCN | 98.2 | 98.1 | 98.1 | 98.1 / 98.2
BiLSTM + Attention + GCN | - | - | - | -


### Out of domain test set accuracy (balancedtest.csv)
Model | Acc | Prec | Recall | F1
--- | --- | --- | --- | ---
LR | 69.52 | 71.48 | 69.52 | 68.44 / 69.52
CNN | - | - | - | -
BERT + LSTM | 56.0 | 57.0 | 56.0 | 55.1 / 56.0
LSTM | - | - | - | -
BiLSTM | - | - | - | -
GRU | - | - | - | -
BiGRU | - | - | - | -
LSTM + Attention | 62.1 | 63.8 | 62.1 | 61.8 / 62.1
BiLSTM + Attention | - | - | - | -
**LSTM + Attention + GCN** | **63.2** | **66.3** | **63.0** | **62.8 / 64.1**
BiLSTM + Attention + GCN | - | - | - | -

## Contributors

- [Chen Xihao](https://github.com/howtoosee)
- [Wang Changqin](https://github.com/archiewang0716)
- [Zhang Haolin](https://github.com/A0236053M)
- [Zhang Lei](https://github.com/AronnZzz)
- [Hon Jia Jing](https://github.com/JiaJingHon)
