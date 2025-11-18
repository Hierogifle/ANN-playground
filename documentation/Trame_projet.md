# Predict Students' Dropout and Academic Success

Ce projet vise à développer un modèle de Perceptron Multicouche (MLP) pour prédire le statut des étudiants (abandon, diplômé, inscrit) en se basant sur diverses caractéristiques démographiques et académiques. Le projet comprend plusieurs étapes clés, allant de la collecte et du prétraitement des données à l'entraînement et à l'évaluation du modèle.

## Étapes du Projet
### 1. **Collecte des Données** : Récupération des données pertinentes à partir de sources fiables. - cf `notebooks/extract_and_load_dataset.ipynb`

Télchargement des datasets depuis l'UCI Machine Learning Repository :
- https://archive.ics.uci.edu/dataset/697/predict+students+dropout+and+academic+success

```python
dataset = fetch_ucirepo(id=697) 
```

Dataset : 37 variables (features) + 1 variable cible (target) - 4433 échantillons.

Analyse des différentes variables disponibles dans le dataset pour comprendre leur signification et leur utilité potentielle dans la prédiction du statut des étudiants. 
- cf `documentation/data_info.md`

### 2. **Prétraitement des Données** : Nettoyage et préparation des données pour l'analyse. - cf `notebooks/extract_and_load_dataset.ipynb`

Verification de la qualité des données :
- valeurs manquantes = Aucune valeur manquante détectée.
- anomalies = Aucune anomalie détectée.
- incohérences = Suppression des lignes où "Mother's occupation" est 125, 173 ou 191 car aucune correspondance métier n'est trouvée.
  - Nombre / Pourcentage de lignes supprimées : 28 / 0.63 %

Ajout de features - Création de nouvelles variables basées sur les données existantes pour enrichir le dataset.
- cf `documentation/data_info.md`

Répartition des cibles :
- Graduate : 2193 (49.9 %)
- Dropout : 1421 (32.3 %)
- Enrolled : 782 (17.8 %)

Dataset après modification : 43 variables (features) + 1 variable cible (target) - 4433 échantillons.

Séparation des données en deux fichiers distincts pour des analyses ciblées :
- `data/data_enrolled.csv` : Contient uniquement les étudiants inscrits (Enrolled).
  - Nombre d'observations : 782
  - Répartition des cibles :
    - Enrolled : 782 (100 %)
- `data/data_graduate_dropout.csv` : Contient les étudiants diplômés (Graduate) et ceux ayant abandonné (Dropout).
    - Nombre d'observations : 3614
    - Répartition des cibles :
        - Graduate : 2193 (60.7 %)
        - Dropout : 1421 (39.3 %)


### 3. **Exploration des Données (EDA)** : Analyse exploratoire pour comprendre les tendances


### 4. **Séparation des Données** : Division des données en ensembles d'entraînement, de validation et de test.
### 5. **Construction du Modèle MLP** : Développement et configuration du modèle de Per
### 6. **Entraînement du Modèle** : Formation du modèle sur les données d'entraînement.
### 7. **Évaluation du Modèle** : Test et validation des performances du modèle.
### 8. **Optimisation et Ajustement** : Amélioration du modèle en ajustant les
### 9. **Documentation et Présentation** : Compilation des résultats et rédaction de la documentation du projet.

## Technologies Utilisées
- Python
- Bibliothèques : NumPy, Pandas, Scikit-learn, TensorFlow/Keras, Matplotlib, Seaborn
- Environnement de Développement : Jupyter Notebook, VSCode
- Gestion de Version : Git, GitHub
- Outils de Visualisation : Matplotlib, Seaborn

## Organisation des Fichiers
- `notebooks/` : Contient les notebooks Jupyter pour chaque étape du projet.
- `data/` : Dossier pour stocker les datasets bruts et prétraités.
- `models/` : Contient les scripts et fichiers liés au modèle MLP.
- `documentation/` : Documentation du projet, y compris ce fichier.
- `scripts/` : Scripts Python pour diverses tâches du projet.
- `results/` : Résultats des analyses et évaluations du modèle.
- `README.md` : Aperçu du projet et instructions pour l'exécution.
- `requirements.txt` : Liste des dépendances Python nécessaires pour le projet.

## Instructions pour l'Exécution
1. Cloner le dépôt GitHub.
2. Installer les dépendances à partir de `requirements.txt`.
3. Exécuter les notebooks dans l'ordre pour reproduire les étapes du projet.
4. Consulter la documentation pour plus de détails sur chaque étape.
5. Analyser les résultats dans le dossier `results/`.