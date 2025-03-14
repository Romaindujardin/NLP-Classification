# Projet de Classification de Commentaires Toxiques

## 1. Introduction

Ce projet s’inscrit dans le cadre du défi [Kaggle Jigsaw Toxic Comment Classification Challenge](https://www.kaggle.com/competitions/jigsaw-toxic-comment-classification-challenge/discussion/52557). L’objectif principal est de développer un modèle capable de prédire les labels associés à chaque commentaire afin d’identifier différentes formes de toxicité dans les textes.

## 2. Sommaire des Solutions

Plusieurs approches ont été mises en œuvre pour améliorer la performance de la classification :

- **Modèle Baseline (TF-IDF + OneVsRest Logistic Regression)** : La première approche utilise la vectorisation TF-IDF pour transformer les textes en vecteurs numériques, combinée à un classificateur OneVsRest basé sur la régression logistique. [Accéder au dossier du Modèle Baseline]()
- **Modèle Deep Learning (Embedding + LSTM)** : Cette approche introduit des embeddings et des réseaux de neurones LSTM pour capturer l’ordre des mots et le contexte. Deux variantes ont été explorées :
  - Un MLP avec embeddings seuls.
  - Un RNN avec LSTM pour une meilleure modélisation des séquences.
  - [Accéder au README du Modèle Deep Learning]()
- **Modèle Final (LSTM Bidirectionnel)** : La version finale intègre une architecture de LSTM bidirectionnel, permettant de capter le contexte dans les deux directions. Ce modèle bénéficie également d’un pipeline optimisé incluant une vectorisation via TextVectorization, la création d’un dataset TensorFlow, et un calcul approfondi des métriques. [Accéder au README du Modèle Final]()
  
## 3. Résultats Globaux

Les performances du modèle final se traduisent par les métriques suivantes :

- Recall par label : [0.98043053, 0.86792453, 0.97472924, 0.76470588, 0.96835443, 0.8705036]
- F1-score par label : [0.98267408, 0.84662577, 0.97649186, 0.80412371, 0.97204574, 0.89962825]
- F1-score macro (moyenne des F1-scores) : 0.9135982355653286
- F1-score micro (calculé globalement) : 0.9667812142038946

Ces résultats témoignent de la robustesse et de la précision du système final dans la détection des différents types de toxicité.
