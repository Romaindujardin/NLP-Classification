# Modèle de base (TF-IDF)

## 1. Introduction

Dans le cadre de notre projet de classification de commentaires toxiques, nous avons développé plusieurs modèles afin de mesurer l'évolution des approches utilisées. Ce document décrit le **Modèle Baseline** (Modèle 1), ses mécanismes de fonctionnement et ses limitations, justifiant ainsi la transition vers une approche plus avancée (Modèle 2).

## 2. Description du Modèle Baseline

Le modèle de base repose sur une approche traditionnelle en plusieurs étapes :

- Prétraitement et Nettoyage : Les textes sont convertis en minuscules et nettoyés des caractères spéciaux, garantissant une uniformisation des données.
- Vectorisation par TF-IDF : Le modèle transforme les textes en vecteurs numériques en se basant sur la fréquence pondérée des termes. Cette méthode permet de représenter chaque commentaire par un vecteur de features, sans tenir compte de l’ordre des mots.
- Classification Multi-label : En sélectionnant six catégories (toxic, severe_toxic, obscene, threat, insult, identity_hate), nous utilisons un classificateur OneVsRest avec une régression logistique pour gérer la classification multi-label.
- Séparation et Évaluation : Les données sont divisées en ensembles d’entraînement et de test. Après entraînement, le modèle est évalué à l’aide de rapports de classification pour mesurer sa performance sur chaque classe.

## 3. Limitations du Modèle Baseline

Bien que simple et rapide à implémenter, le modèle baseline présente plusieurs inconvénients :

- Perte d’Information Contextuelle : Le TF-IDF ne prend pas en compte l’ordre des mots. Ainsi, des phrases ayant des significations opposées (par exemple, « Ce n'est pas une insulte » vs. « C'est une insulte ») peuvent être représentées de manière similaire.
- Incapacité à Capturer les Nuances Linguistiques : La méthode se focalise uniquement sur la fréquence des mots, rendant difficile la détection des subtilités telles que le sarcasme ou l'ironie.
- Problème d’Équilibre des Classes : Certaines catégories (comme threat ou identity_hate) sont sous-représentées, ce qui complique l’apprentissage de motifs spécifiques à ces classes.
- Absence de Compréhension des Relations Sémantiques : Le modèle traite les mots de façon indépendante. Par conséquent, des termes synonymes (par exemple, « stupide » et « idiot ») sont considérés comme complètement distincts, alors qu’ils véhiculent un sens similaire.

## 4. Vers un Modèle Plus Avancé

Afin de surmonter ces limitations, nous envisageons d’évoluer vers une approche basée sur le deep learning, comme détaillé dans le Modèle 2. Cette nouvelle stratégie reposera notamment sur :

- L’Utilisation d’Embeddings : Contrairement au TF-IDF, les embeddings permettent d’apprendre des représentations vectorielles qui capturent les relations sémantiques entre les mots (synonymie, contexte, etc.).
- Approches par Réseaux de Neurones :
  - Test d’un MLP : Un Multilayer Perceptron sera d’abord expérimenté avec des embeddings pour mesurer l’impact des représentations sémantiques sur la classification.
  - Implémentation d’un RNN avec LSTM : Pour une meilleure capture de l’ordre et du contexte des mots, un réseau de neurones récurrent doté de couches LSTM sera ensuite déployé.
  
## 5. Objectif de l’Évolution

L’objectif principal du passage au deep learning est de :

- Mieux saisir le sens et le contexte des commentaires.
- Améliorer la détection des nuances subtiles (sarcasme, ironie).
- Optimiser la gestion des classes rares pour une performance globale accrue.
  
En résumé, si le modèle baseline fournit une première base fonctionnelle, ses limitations en termes de contextualisation et de compréhension fine du langage nécessitent une approche plus sophistiquée. Le passage aux techniques de deep learning promet ainsi d’améliorer significativement la classification des commentaires toxiques.
