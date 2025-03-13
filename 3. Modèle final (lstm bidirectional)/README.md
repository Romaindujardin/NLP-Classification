# Amélioration par Approche Deep Learning et Perspectives d'un Pipeline Complet

Après avoir développé un modèle de base reposant sur une vectorisation TF-IDF couplée à une régression logistique, nous avons pu établir une référence pour la classification des commentaires toxiques. Ce modèle baseline, bien que performant pour capturer la présence ou l'absence de certains termes, souffre de plusieurs limitations :

- **Perte d'information contextuelle** : Le TF-IDF ne tient pas compte de l'ordre des mots ni des relations sémantiques, ce qui limite la compréhension des nuances dans les phrases.
- **Difficulté avec les formulations subtiles** : Le modèle ne parvient pas à distinguer des expressions comme "ce n'est pas une insulte" et "c'est une insulte", qui sont traitées de manière similaire.
- **Détection limitée des classes rares** : Les classes sous-représentées (ex. : severe_toxic, threat, identity_hate) sont difficilement apprises et prédictes.

Pour pallier ces limites, nous avons implémenté une approche deep learning qui se décline en deux volets :

1. **Modèles Deep Learning avec Embeddings** :
- **MLP avec Embeddings seuls** : Grâce à une couche d'embedding et un GlobalAveragePooling, nous obtenons des représentations denses qui capturent mieux les similarités sémantiques entre les mots.
- **Réseau de neurones récurrent (LSTM)** : En intégrant des couches LSTM, nous sommes en mesure de saisir le contexte et l'ordre des mots, offrant ainsi une meilleure compréhension des phrases complexes.

Ces modèles améliorent légèrement la détection des classes majoritaires grâce à une meilleure représentation sémantique, mais ils rencontrent encore des difficultés pour identifier les classes rares.

2. **Perspectives d'un Pipeline Complet** :

Pour aller encore plus loin, nous prévoyons de mettre en place un pipeline complet qui inclura :
- **Nettoyage avancé des commentaires** : Suppression des stopwords, lemmatisation, gestion des caractères spéciaux, etc.
- **Tokenisation et Encodage optimisés** : Pour générer des séquences de mots de qualité adaptées aux modèles de deep learning.
- **Modèle Final pour la Classification** : En exploitant ces données prétraitées, nous pourrons concevoir un modèle de classification plus robuste, capable de mieux gérer les classes rares et d'exploiter pleinement le contexte et la sémantique des commentaires.

En résumé, l'approche deep learning apporte une amélioration par rapport au modèle baseline en capturant des informations contextuelles et sémantiques essentielles. Néanmoins, pour atteindre une performance optimale sur toutes les classes, notamment les plus rares, l'intégration d'un pipeline complet de prétraitement et d'optimisation reste indispensable.
