# Bachelorarbeit Darko Cutkovic - README

## Overview
Dieses Repository enthält alle Dateien für die Bachelorarbeit von Darko Cutkovic
Anbei finden Sie Instruktionen zum Ausführen

## Files and Directories

- **`CNN_Notebook.ipynb`**: Dieses Notebook enthält den Code für das Convolutional Neural Network.

- **`LSTM_Notebook.ipynb`**: Dieses Notebook enthält den Code für das Long-Short-Term-Memory Network.

- **`BERT_Notebook.ipynb`**: Dieses Notebook enthält den Code für BERT.

- **`communication_data`**: Diese File enthält die Negoisst Verhandlungsdaten.

Alle weiteren Files sind ausschließlich Teil der Google Drive da sie zu viel Speicher für GitHub einnehmen

- **`crawl-300d-2M-subword.vec`**: Diese  File enthält vortrainierte FastText Embeddings

- **`GoogleNews-vectors-negative300.bin`**: Diese File enthält vortrainierte Word2Vec Embeddings.

- **`BERT_BEST_MODEL.pth`**: Das BERT Modell mit den besten Ergebnisse. Ergibt sich aus den Finetuning auf den letzten 510 Zeichen.

- **`CNN_BEST_MODEL.pth`**: Das CNN Modell mit den besten Ergebnisse. Ergibt sich aus dem erste Hyperparameteroptimierungsprozess.

- **`LSTM_BEST_MODEL.pth`**: Das LSTM Modell mit den besten Ergebnisse. Ergibt sich aus dem erste Hyperparameteroptimierungsprozess.


## Setup and Dependencies

Der Code dieser Arbeit wurde mit Jupyter Notebook erstellt.
Zur Verwendung von Cloud Rechenressourcen wurden diese Notebooks in der Google Colab Umgebung gehostet.
Der Code kann auch lokal ausgeführt werden, jedoch müssen dafür Änderungen vorgenommen werden auf die nun eingegangen wird.
Eine Ausführung über Colab wird empfohlen

Das GitHub Repository finden sie dafür unter diesem Link wieder

https://github.com/DarkoCutkovic/Thesis-Cutkovic-Darko

### Vor der Nutzung müssen zusätzliche dependencies installiert werden

!pip install wordsegment
!pip install num2words
!pip install skorch

### Außerdem wird im Code auf bestimmte Files zugegriffen

Beim Zugriff aud die Negoisst Daten muss der Path ausgetauscht werden.
Der Code dafür findet sich in jedem Notebook im "Loading Data" Block wieder.

df = pd.read_excel('/content/drive/MyDrive/Bachelorarbeit Cutkovic Darko/communication_data.xlsm')

Außerdem wird für das CNN und LSTM auf Embedding Files zugegriffen, diese finden sich im "Create Embeddings" Block wieder.

embeddings = load_pretrained_vectors(word2index, '/content/drive/MyDrive/Bachelorarbeit Cutkovic Darko/crawl-300d-2M-subword.vec', target_dim)

Für den Zugriff auf Word2Vec kann der auskommentierte Code verwendet werden.

Modelle die Sie selbst erstellen, können sie speichern, den Dateipfad dafür müssen sei den Dateipfad am Ende der Notebooks ändern.

torch.save(best_model_crossfold, '/content/drive/MyDrive/Bachelorarbeit Cutkovic Darko/YOUR_MODEL_NAME.pth')


## Ausführung des Codes

### Datenaufbereitung

Eine separate File die die Daten verarbeitet gibt es nicht, dies erfolgt immer zu Beginn wenn die entsprechenden
"Data Preparation" Abschnitte ausgeführt werden. Aufgrund des WordSegment Algorithmus der syntaktische Fehler
behebt kann dies ca. 10 Minuten in Anspruch nehmen.

### Ausführung CNN und LSTM

Die Modelle sind im Anschluss an den Abschnitt für die Datenaufbereitung definiert.
Sie finden den Code zur Ausführung im "Executing, Tuning and Validating" Block wieder, mit zusätzlichen Anmerkungen.
Die Ausführung erfolgt ausschließlich durch die RandomSearch Optimierungsmethode.
Sie können den SearchSpace und zusätzliche Parameter wie die Anzahl an Iterationen selbst definieren, im Code sind diese
Werte beispielhaft definiert.

random_search.fit() führt die Optimierung aus.

### Ausführung BERT

Der Code für BERT unterscheidet sich von dem für das CNN und LSTM.
Sie finden den Code zur Ausführung im Model Execution Block.
Die Trainings und Validierungsloop wurden hierfür manuell implementiert.
Auch Kreuzvalidierung und Hyperparameteroptimierung wurden manuell implementiert
Im Block der Optimization Loop können Sie Änderungen an der Konfiguration vornehmen mit der das Modell trainiert werden soll, eine Evaluierung erfolgt automatisch.

optimizer.run_grid_search() führt die Optimierung aus


### Modelle

Die drei Modelle die im Verlauf die besten Resultate aufzeigen konnten sind beigefügt.
Um diese Modelle zu laden kann der folgende Code ausgeführt werden: 

model = torch.load('model_path', map_location='device')
