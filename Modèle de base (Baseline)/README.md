## Limites du modèle baseline et nécessité d’un modèle plus avancé

Le modèle baseline, basé sur ** une régression logistique avec TF-IDF **, offre une première approche efficace mais présente plusieurs limitations majeures :

### 1. Perte d’information contextuelle

- Le TF-IDF ignore l’ordre des mots, ce qui empêche le modèle de comprendre le contexte.
- Exemple : "Ce n'est pas une insulte" et "C'est une insulte" auront des représentations similaires, alors qu'ils ont un sens opposé.

### 2. Difficulté avec les formulations subtiles
- L'approche actuelle considère uniquement la présence ou la fréquence des mots, sans comprendre leur signification.
- Exemple : Sarcasme et ironie sont mal détectés.

### 3. Problème d’équilibre des classes
- Certaines classes sont rares (threat, identity_hate), ce qui rend leur prédiction difficile.
- Le modèle a du mal à apprendre des motifs efficaces sur ces catégories sous-représentées.

### 4. Indépendance des mots et absence de synonymie
- "stupide" et "idiot" sont considérés comme différents, alors qu’ils sont synonymes.
- Les modèles TF-IDF ne capturent pas les relations sémantiques entre les mots.

## Pourquoi passer au deep learning ?
Pour pallier ces limites, nous allons introduire une approche par embeddings et réseaux de neurones :

Utilisation des embeddings (Word2Vec, FastText, ou Embeddings Keras)
Contrairement au TF-IDF, ces méthodes apprennent des représentations sémantiques des mots, capturant leurs relations et synonymes.
Test d’un MLP (Multilayer Perceptron)
Cette architecture permettra de voir si les embeddings seuls suffisent à améliorer la classification sans ajouter la complexité des réseaux récurrents.
Utilisation d’un RNN (LSTM/GRU)
Permettra de capturer le contexte et l’ordre des mots pour une meilleure compréhension des phrases complexes.
💡 Objectif du deuxième modèle :
Améliorer la classification des commentaires toxiques en capturant le sens réel des phrases, le contexte des mots, et en gérant mieux les classes rares. 🚀
