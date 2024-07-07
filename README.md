# Système de Recommandation de Films Complémentaires

## Aperçu

Ce projet vise à développer un système de recommandation qui fournit des recommandations de films pertinentes et complémentaires pour deux utilisateurs en fonction de leurs préférences. Le système utilise le filtrage collaboratif et la factorisation de matrices pour prédire les notes des films pour un couple d'utilisateurs, en suggérant des films que les deux utilisateurs sont susceptibles d'apprécier.

## Méthodologie

### Collecte et Prétraitement des Données

- **Jeux de Données** : 
  - `ratings.dat` : Contient les notes des utilisateurs pour divers films.
  - `movies.dat` : Contient les métadonnées des films, y compris les titres et les genres.
  - `title.basics.tsv` (IMDb) : Contient des métadonnées supplémentaires d'IMDb, telles que les titres principaux, les années de début et les genres.

- **Étapes de Prétraitement** :
  - **Chargement des Données** : Charger les jeux de données dans des DataFrames pandas.
  - **Extraction des Caractéristiques** : Extraire l'année des titres de films et normaliser les titres en minuscules.
  - **Gestion des Valeurs Manquantes** : Remplir les valeurs manquantes dans les données `title.basics.tsv`.
  - **Fusion des Données** : Fusionner `movies.dat` avec `title.basics.tsv` pour enrichir le jeu de données avec des métadonnées supplémentaires.

### Extraction des Caractéristiques

- **Matrice Utilisateur-Élément** : Créer une matrice d'interaction utilisateur-élément à partir du jeu de données fusionné. Cette matrice est utilisée pour représenter les notes données par les utilisateurs aux films.

### Développement du Modèle

- **Factorisation de Matrice** : Implémenter l'algorithme SVD (Singular Value Decomposition) en utilisant la bibliothèque Surprise.
- **Optimisation des Hyperparamètres** : Utiliser GridSearchCV pour trouver les meilleurs hyperparamètres pour le modèle SVD, en optimisant pour la métrique RMSE.

### Algorithme de Recommandation

- **Prédiction des Notes** : Développer une fonction pour prédire les notes de tous les films pour deux utilisateurs et calculer une note moyenne.
- **Score du Couple** : Calculer un "score du couple" pour chaque film en fonction des notes prédites pour les deux utilisateurs et trier les films par ce score.

### Évaluation

- **Séparation Entraînement-Test** : Diviser les données en ensembles d'entraînement et de test pour évaluer les performances du modèle.
- **Métrique de Performance** : Évaluer le modèle en utilisant la RMSE (Root Mean Squared Error) pour mesurer la précision des prédictions.

## Expériences

### Optimisation des Hyperparamètres

- Des expériences ont été menées pour trouver les meilleurs hyperparamètres pour le modèle SVD en utilisant GridSearchCV. L'espace de recherche comprenait :
  - `n_factors` : [50]
  - `n_epochs` : [10]
  - `lr_all` : [0.005]
  - `reg_all` : [0.1]

### Évaluation du Modèle

- Le modèle a été évalué en utilisant la métrique RMSE sur les données de test. Le RMSE final obtenu était de [insérer la valeur RMSE], indiquant la précision du modèle dans la prédiction des notes des utilisateurs.


### Algorithme de Recommandation
- Fonction recommend_movie_for_user_pair
Cette fonction recommande des films en se basant uniquement sur les notes prédites pour deux utilisateurs. Voici les étapes principales :

Prédictions pour tous les films : Les notes prédites pour chaque film sont calculées pour les deux utilisateurs.
Moyenne des prédictions : La moyenne des prédictions des deux utilisateurs est calculée pour chaque film.
Sélection des meilleurs films : Les films sont triés en fonction des notes moyennes et les meilleurs sont sélectionnés

- Fonction recommend_movies_for_user_pair_with_genres_years
Cette fonction améliore la recommandation en tenant compte des genres et des années des films préférés par les utilisateurs. Voici les étapes principales :

Obtenir les notes des utilisateurs : Les notes des utilisateurs sont obtenues à partir de la matrice utilisateur-élément.
Extraire les genres et années préférés : Les genres et les années des films aimés par chaque utilisateur sont extraits.
Trouver les préférences communes : Les genres et les années communs préférés par les deux utilisateurs sont déterminés.
Prédictions pour tous les films : Les notes prédites pour chaque film sont calculées pour les deux utilisateurs.
Moyenne des prédictions : La moyenne des prédictions des deux utilisateurs est calculée pour chaque film.
Filtrer les films : Les films sont filtrés pour inclure seulement ceux qui correspondent aux genres et aux années préférés.
Sélection des meilleurs films : Les films filtrés sont triés en fonction des notes moyennes et les meilleurs sont sélectionnés.


### Comparaison des Fonctions
- recommend_movie_for_user_pair :
Avantages : Plus simple et plus rapide car elle ne filtre pas les films par genres et années.
Inconvénients : Ne prend pas en compte les préférences spécifiques des utilisateurs en termes de genres et d'années des films.
- recommend_movies_for_user_pair_with_genres_years :
Avantages : Offre des recommandations plus personnalisées en tenant compte des genres et des années que les utilisateurs ont aimés.
Inconvénients : Peut être légèrement plus lente en raison du filtrage supplémentaire des films par genres et années.


## Résultats

Le système recommande avec succès des films complémentaires aux préférences de deux utilisateurs. Les recommandations sont basées sur les notes moyennes prédites pour les deux utilisateurs, garantissant que les films suggérés ont des scores de couple élevés.


## Conclusion

Le système de recommandation fournit des recommandations de films pertinentes et complémentaires pour deux utilisateurs en utilisant des techniques de filtrage collaboratif et de factorisation de matrices. L'utilisation de GridSearchCV pour l'optimisation des hyperparamètres et l'évaluation du modèle à l'aide de la RMSE ont permis d'assurer que les recommandations sont précises et significatives.

## Comment Exécuter le Projet

1. **Cloner le Dépôt** :
   ```bash
   git clone [repository_url]
   cd [repository_name]
   ```

2. **Installer les Dépendances** :
   ```bash
   pip install -r requirements.txt
   ```
