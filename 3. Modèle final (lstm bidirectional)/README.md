# Modèle final (LSTM bidirectional)

## 1. Introduction

Ce modèle final représente l’aboutissement de notre travail sur la classification de commentaires toxiques. Il intègre des améliorations significatives par rapport aux versions précédentes en utilisant une architecture de LSTM bidirectionnel. Cette approche permet de capturer le contexte dans les deux directions, offrant ainsi une meilleure compréhension des séquences textuelles. De plus, un pipeline de prétraitement et d’évaluation optimisé garantit une manipulation efficace des données et une analyse fine des performances.

## 2. Fonctionnalités et Pipeline

### 2.1 Importation des Packages et des Données
- Packages Utilisés : Les bibliothèques essentielles telles que TensorFlow, Keras et scikit-learn sont importées pour la manipulation des données, la construction du modèle et le calcul des métriques.
- Chargement des Données : Les données d’entraînement sont importées depuis Google Drive via un lien partagé. Un aperçu rapide du DataFrame permet de vérifier l’importation et d’extraire des exemples de commentaires toxiques.

### 2.2 Prétraitement : Vectorisation du Texte
- TextVectorization : Le texte est transformé en séquences d’entiers grâce à la couche TextVectorization de Keras.
  - max_tokens : Fixé à 200 000, permettant de prendre en compte un vaste vocabulaire.
  - output_sequence_length : Limité à 2000 tokens, assurant une uniformisation des séquences.
- Adaptation du Vectoriseur : Le vectoriseur est adapté aux données textuelles pour apprendre le vocabulaire et convertir l’ensemble des commentaires en séquences vectorisées.
  
### 2.3 Création du Dataset TensorFlow
- Construction du Dataset : Un dataset TensorFlow est créé à partir des séquences vectorisées et des labels.
- Optimisation des Performances :
  - Caching et Shuffling : Pour garantir des batches aléatoires et accélérer l’accès aux données.
  - Batching et Prefetching : Division en batches de taille 16 et préchargement des données pour améliorer l'efficacité pendant l'entraînement.
- Division des Données : Le dataset est partitionné en trois ensembles : 70 % pour l’entraînement, 20 % pour la validation et 10 % pour le test.
  
### 2.4 Construction et Entraînement du Modèle
- Architecture du Modèle :
  - Embedding : Conversion des indices en vecteurs denses avec une couche d’embedding adaptée à la taille du vocabulaire.
  - LSTM Bidirectionnel : Une couche LSTM bidirectionnelle (avec activation tanh) capture les dépendances contextuelles dans les deux directions.
  - Couches Denses : Plusieurs couches fully-connected (avec activations ReLU) permettent d’extraire et d’affiner des caractéristiques complexes.
  - Sortie : Une couche finale à 6 neurones avec activation sigmoïde pour réaliser une classification multi-label.
- Compilation : Le modèle est compilé avec la fonction de perte BinaryCrossentropy et l’optimiseur Adam, en surveillant l’accuracy.
- Entraînement : Le modèle est entraîné pendant 20 epochs avec validation régulière sur un ensemble dédié.
  
### 2.5 Prédictions et Évaluations Initiales
- Exemples de Prédiction : Des exemples de texte sont vectorisés et soumis au modèle pour obtenir des prédictions initiales.
- Evaluation sur Batch de Test : Les prédictions sont comparées aux labels réels sur des batches du jeu de test pour une première évaluation qualitative.
  
### 2.6 Calcul des Métriques
- Avec Keras : Les métriques de précision et de rappel sont calculées sur les batches de test. Le F1-score est ensuite déduit pour fournir une mesure synthétique des performances.
- Avec scikit-learn : Les prédictions sont binarisées et évaluées pour chaque label, avec des métriques par classe (précision, rappel, F1-score) ainsi que des scores globaux macro et micro.
  
### 2.7 Sauvegarde et Chargement du Modèle
- Sauvegarde : Le modèle entraîné est sauvegardé au format H5 afin de pouvoir être réutilisé sans avoir à réentraîner.
- Chargement : Une procédure de chargement est implémentée pour recharger le modèle sauvegardé et vérifier son intégrité.
  
### 2.8 Fonction de Scoring d'un Commentaire
- Scoring : Une fonction dédiée permet de scorer un commentaire individuel. Le texte est vectorisé, passé dans le modèle, et les prédictions pour chaque classe de toxicité sont renvoyées sous forme d’indicateurs booléens.
  
### 2.9 Evaluation Complémentaire avec Accuracy Score
- Accuracy Score : Un calcul complémentaire de l’accuracy est réalisé sur l’ensemble des données de test en agrégant les prédictions et les labels réels. Cela permet de quantifier la performance globale du modèle sur des exemples individuels.
  
## 3. Axes d'Amélioration

Bien que le modèle final présente une architecture robuste et des performances intéressantes, plusieurs axes d'amélioration peuvent être envisagés pour optimiser encore davantage ses résultats :

- Optimisation des Hyperparamètres : Ajuster le nombre d’unités dans les couches LSTM, la taille des embeddings ou le taux de dropout pourrait permettre d’atteindre un meilleur compromis entre sous-apprentissage et surapprentissage.
- Enrichissement de l'Architecture : Explorer l’ajout de couches supplémentaires (par exemple, des couches convolutionnelles pour extraire des motifs locaux) ou intégrer des mécanismes d’attention afin de mieux peser l’importance des mots dans les séquences.
- Amélioration de la Gestion des Classes Déséquilibrées : Implémenter des stratégies telles que le suréchantillonnage des classes rares ou l’utilisation de fonctions de perte pondérées pour améliorer la prédiction sur des labels sous-représentés.
- Utilisation d’Embeddings Pré-entrainés : Remplacer la couche d’embedding par des embeddings pré-entraînés (comme GloVe ou FastText) pourrait enrichir la représentation des mots et capturer des informations sémantiques plus fines.
- Affinage du Pipeline de Prétraitement : Tester différentes configurations de vectorisation (ajustement de la longueur des séquences, filtrage de stop-words, etc.) et optimiser la préparation des données pour maximiser la qualité des inputs.
- Expérimentation avec l’Ensemble Learning : Combiner ce modèle final avec d’autres approches (par exemple, des modèles basés sur Transformers) dans une stratégie d’assemblage (ensemble) pourrait augmenter la robustesse et la précision globale du système.
  
## 4. Conclusion

Le modèle final, basé sur une architecture de LSTM bidirectionnel, offre une approche avancée et robuste pour la classification des commentaires toxiques. Grâce à un pipeline optimisé incluant une vectorisation de texte performante, une gestion efficace des données avec TensorFlow, et une évaluation complète par divers indicateurs, ce modèle se distingue par sa capacité à capturer des dépendances contextuelles riches. Les axes d'amélioration identifiés offrent des pistes concrètes pour pousser encore plus loin les performances et la précision du système de classification.
