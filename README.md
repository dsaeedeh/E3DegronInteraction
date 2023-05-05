# 🧬 E3 ligases and Degron Interaction

## 📝 Description

In this project, we explore the task of predicting degron-E3 interactions using a deep learning approach. Specifically, we use a pre-trained BERT language model and fine-tune it on a dataset of degron-E3 pairs that we have gathered. We formulate the problem as a question-answering task, where the model takes in a pair of degron and E3 as input and outputs a binary prediction (1 if they are interacting, 0 if they are not). By leveraging the power of transfer learning from the pre-trained BERT model, we aim to improve the accuracy of degron-E3 interaction prediction, which can have important implications for understanding protein degradation pathways and developing therapeutic interventions for diseases.

## 🚀 Next Steps

- **Data augmentation** 📊: Large language models require bigger training data to achieve acceptable performance. We could perform more data augmentation to generate additional training examples and potentially improve the model's performance.

- **Optimizing hyperparameters on a more powerful system 💻**: The current model was trained on a personal system without any GPUs available, leading to a limited number of epochs. By running the model on a high-performance GPU/CPU cluster, we can experiment with more epochs and better hyperparameter tuning.

- **Utilizing specialized pre-trained models 🧪**: We used a base pre-trained BERT model, which was trained on regular English text. However, since our task involves protein sequences, it might be more beneficial to use models pre-trained on protein sequences, such as protein-BERT or GLM4EC models. Due to system limitations, we were unable to load protein-BERT on the personal laptop, but a more powerful system could potentially enable the use of such specialized models.

- **Exploring alternative approaches 🔍**: We encountered multiple solutions that utilized graph neural networks to solve similar problems. Although we have not used this approach ourselves, it could be a promising candidate for further research and development in predicting degron-E3 interactions.

## 📚 Dataset

- E3-substrates-interactions file is downloaded from: http://ubibrowser.bio-it.cn/ubibrowser_v3/home/download
- Collected_degrons file is downloaded from: http://degron.phasep.pro/download/

## 🧹 Preprocessing

1. Read the datasets
2. Remove the rows with NaN or invalid IDs on Entry column in degrons, and unreviewed on their Status column
3. Remove the rows with NaN or invalid IDs on both SwissProt AC (Substrate) and SwissProt AC (E3) columns
4. Merge them together on Entry to a final dataset
5. Keep needed columns: SwissProt AC (Substrate), SwissProt AC (E3), protein seq, start, end, deg_seq, E3_sequence
6. Explode the rows containing # in their E3
7. Add E3 sequences to the dataframe

## 🎯 Model Training: Pre-trained BERT Model and Fine-tuning

We use the pre-trained BERT model for our task of predicting degron-E3 interactions. The specific pre-trained model used is 'bert-base-uncased', which has been trained on uncased English text. The following line of code initializes a BERT (Bidirectional Encoder Representations from Transformers) model for sequence classification with one output label:

```python
model = BertForSequenceClassification.from_pretrained('bert-base-uncased', num_labels=1)
```

The num_labels parameter is set to 1, indicating that the model is designed for binary classification tasks where there are only two possible output labels (1 for interacting and 0 for non-interacting). The initialized model is an instance of the `BertForSequenceClassification` class, which includes a BERT model followed by a linear layer for classification. By fine-tuning the pre-trained BERT model on our dataset of degron-E3 pairs, we aim to achieve high accuracy in predicting their interactions.
