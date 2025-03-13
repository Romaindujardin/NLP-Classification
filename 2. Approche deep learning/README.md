# Modele 2 (Approche deep learning)

## 1. Introduction

Ce modèle deep learning marque une évolution par rapport à l'approche baseline. L’objectif ici est d’exploiter les techniques d’embeddings et les réseaux de neurones pour améliorer la classification des commentaires toxiques. Le pipeline s'articule en deux sous-modèles complémentaires :

- Modèle A : Un MLP (Multilayer Perceptron) utilisant uniquement des embeddings.
- Modèle B : Un RNN avec couches LSTM, permettant de capturer l’ordre et le contexte des mots.

## 2. Pipeline et Fonctionnement

**Prétraitement et Vectorisation**
- Importation et Nettoyage des Données : Les données sont importées depuis Google Drive. Chaque commentaire est converti en minuscules et nettoyé des caractères spéciaux via une fonction de nettoyage.
- Tokenisation et Création de Séquences : Un Tokenizer de Keras est utilisé pour transformer les textes nettoyés en séquences d'entiers, suivies d’un padding (max_len) afin d’uniformiser la longueur des séquences.
- Préparation des Labels : Les six classes (toxic, severe_toxic, obscene, threat, insult, identity_hate) sont extraites pour constituer les cibles de la classification multi-label.
- Séparation Train/Validation : Le jeu de données est divisé en ensembles d’entraînement et de validation pour permettre une évaluation régulière durant l’apprentissage.
  
**Modèle A – MLP avec Embeddings**
- Architecture :
  - Couche d’Embedding : Conversion des indices en vecteurs denses.
  - GlobalAveragePooling1D : Agrégation des informations des embeddings.
  - Couches Dense et Dropout : Apprentissage des caractéristiques avec régularisation.
  - Couche de Sortie : Activation sigmoïde pour la prédiction multi-label.
- Entraînement et Évaluation : Le modèle est entraîné sur les données d’entraînement et évalué sur le jeu de validation. Le rapport de classification montre une amélioration par rapport au modèle baseline, mais révèle encore des difficultés pour certaines classes.
  
**Modèle B – RNN avec LSTM**
- Architecture :
  - Couche d’Embedding : Utilise le même vocabulaire que pour le MLP.
  - Deux Couches LSTM :
    - La première LSTM retourne la séquence complète pour enrichir l’information contextuelle.
    - La seconde LSTM se concentre sur la dernière sortie pour résumer le contexte.
  - Couches Dense et Dropout : Pour affiner l’apprentissage et réduire le surapprentissage.
  - Couche de Sortie : Activation sigmoïde pour la classification multi-label.
- Entraînement et Évaluation : Le modèle LSTM démontre une capacité supérieure à capturer l’ordre des mots et le contexte, bien qu’il continue de rencontrer des difficultés, notamment sur des classes rares comme threat et identity_hate.

## 3. Limitations du Modèle Deep Learning (Modèle 2)

Bien que l'approche deep learning améliore la représentation sémantique par rapport au TF-IDF, certaines limitations persistent :

- Captation Partielle du Contexte : Même avec les LSTM, le modèle peut peiner à saisir certaines nuances contextuelles ou à gérer des séquences particulièrement longues.
- Classes Sous-Représentées : Les classes rares (ex. : threat et identity_hate) continuent de poser problème, avec des scores faibles malgré l’utilisation des embeddings et des LSTM.
- Complexité et Généralisation : L’augmentation de la complexité du modèle peut mener à un surapprentissage, surtout lorsque le déséquilibre entre les classes est marqué.
  
## 4. Vers le Modèle 3 : Nouvelles Perspectives

Pour pallier ces limitations, le modèle 3 introduira plusieurs améliorations clés :

- LSTM Bidirectionnel : L’utilisation de couches LSTM bidirectionnelles permettra de capturer les dépendances contextuelles dans les deux sens (avant et arrière), améliorant ainsi la compréhension globale des séquences.
- TextVectorization : L’intégration d’une couche TextVectorization (de Keras) offrira une vectorisation plus robuste et efficace, améliorant la qualité des embeddings et la représentation des textes.
- Pipeline TensorFlow Optimisé : La création d’un dataset TensorFlow (avec caching, batching et prefetching) permettra d’améliorer significativement la performance durant l’entraînement et d’assurer une meilleure gestion des données.
- Architecture Plus Profonde : L’ajout de couches denses supplémentaires après le LSTM bidirectionnel aidera à apprendre des caractéristiques plus complexes et affinées, optimisant la prédiction des classes difficiles.
  
## 5. Objectifs et Perspectives

L’évolution vers le Modèle 3 vise à :

- Améliorer la Compréhension Contextuelle : Grâce à l’utilisation du LSTM bidirectionnel, le modèle pourra mieux saisir les dépendances dans les deux sens.
- Optimiser la Prédiction des Classes Rares : En renforçant l’architecture et en améliorant la vectorisation, le modèle devrait mieux traiter les classes sous-représentées.
- Augmenter la Robustesse Globale : Une architecture plus profonde et un pipeline optimisé permettront de réduire le surapprentissage et d’améliorer la généralisation.
