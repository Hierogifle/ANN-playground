# Sélection des features

Ce document décrit les différentes méthodes de sélection des features utilisées dans le projet, ainsi que les critères de choix et les résultats obtenus.

## 1. Introduction

La sélection des features est une étape cruciale dans le processus de modélisation, car elle permet d'améliorer la performance du modèle, de réduire le surapprentissage et de diminuer le temps de calcul. Plusieurs techniques peuvent être utilisées pour sélectionner les features les plus pertinentes.

## 2. Méthodes de sélection des features

### 2.1. Sélection basée sur la corrélation

Cette méthode consiste à calculer la matrice de corrélation entre les features et à éliminer celles qui sont fortement corrélées entre elles, afin de réduire la redondance.

Résultats de l'analyse de corrélation :
- Features fortement corrélées (|r| ≥ 0.8) :
  - Curricular units 1st sem (credited) ↔ Curricular units 2nd sem (credited) : 0.9415
  - Curricular units 1st sem (enrolled) ↔ Curricular units 2nd sem (enrolled) : 0.9142
  - Curricular units 1st sem (approved) ↔ Curricular units 1st sem (Approved/Enrolled) : 0.8953
  - Curricular units 1st sem (approved) ↔ Curricular units 2nd sem (approved) : 0.8889
  - Curricular units 2nd sem (approved) ↔ Curricular units 2nd sem (Approved/Enrolled) : 0.8648
  - Curricular units 2nd sem (grade) ↔ Curricular units 2nd sem (Approved/Enrolled) : 0.8601
  - Curricular units 1st sem (credited) ↔ Curricular units 1st sem (enrolled) : 0.8594
  - Curricular units 1st sem (grade) ↔ Curricular units 1st sem (approved) : 0.8583
  - Curricular units 1st sem (Approved/Enrolled) ↔ Curricular units 2nd sem (Approved/Enrolled) : 0.8528
  - Curricular units 2nd sem (grade) ↔ Curricular units 2nd sem (approved) : 0.8513
  - Curricular units 1st sem (grade) ↔ Curricular units 1st sem (Approved/Enrolled) : 0.8400
  - Curricular units 1st sem (enrolled) ↔ Curricular units 2nd sem (credited) : 0.8383
  - Nationality Group ↔ International : 0.8335
  - Curricular units 1st sem (Approved/Enrolled) ↔ Curricular units 2nd sem (grade) : 0.8047
  - Curricular units 1st sem (grade) ↔ Curricular units 2nd sem (grade) : 0.8014

### 2.2. Sélection basée sur l'importance des features

Cette méthode utilise des algorithmes d'apprentissage automatique (comme les forêts aléatoires ou les modèles de gradient boosting) pour évaluer l'importance de chaque feature dans la prédiction de la variable cible. Les features les moins importantes sont ensuite éliminées.

Dans ce projet, nous avons utilisé 2 modèles pour évaluer l'importance des features et sélectionner celles qui contribuent le plus à la performance du modèle :
1. Random Forest Feature Importance
  - Curricular units 1st sem (credited) ↔ Curricular units 2nd sem (credited) : 0.9415
  - Curricular units 1st sem (enrolled) ↔ Curricular units 2nd sem (enrolled) : 0.9142
  - Curricular units 1st sem (approved) ↔ Curricular units 1st sem (Approved/Enrolled) : 0.8953
  - Curricular units 1st sem (approved) ↔ Curricular units 2nd sem (approved) : 0.8889
  - Curricular units 2nd sem (approved) ↔ Curricular units 2nd sem (Approved/Enrolled) : 0.8648
  - Curricular units 2nd sem (grade) ↔ Curricular units 2nd sem (Approved/Enrolled) : 0.8601
  - Curricular units 1st sem (credited) ↔ Curricular units 1st sem (enrolled) : 0.8594
  - Curricular units 1st sem (grade) ↔ Curricular units 1st sem (approved) : 0.8583
  - 
  - Curricular units 1st sem (Approved/Enrolled) ↔ Curricular units 2nd sem (Approved/Enrolled) : 0.8528
  - Curricular units 2nd sem (grade) ↔ Curricular units 2nd sem (approved) : 0.8513
  - Curricular units 1st sem (grade) ↔ Curricular units 1st sem (Approved/Enrolled) : 0.8400
  - 
  - Curricular units 1st sem (enrolled) ↔ Curricular units 2nd sem (credited) : 0.8383
  - Nationality Group ↔ International : 0.8335
  - Curricular units 1st sem (Approved/Enrolled) ↔ Curricular units 2nd sem (grade) : 0.8047
  - Curricular units 1st sem (grade) ↔ Curricular units 2nd sem (grade) : 0.8014

Features à supprimer :
- Curricular units 2nd sem (credited)
- Curricular units 2nd sem (enrolled)
- Curricular units 2nd sem (approved)
- Curricular units 2nd sem (grade)
- 
- Curricular units 1st sem (approved)
- Curricular units 1st sem (enrolled)
- Curricular units 1st sem (credited)
- Curricular units 1st sem (grade)
- International


1. XGBoost/LightGBM Feature Importance

### 2.3. Sélection récursive

La sélection récursive des features (RFE) est une technique qui consiste à entraîner un modèle, à évaluer l'importance des features, puis à éliminer les moins importantes de manière itérative jusqu'à obtenir un ensemble optimal de features.

## 3. Résultats

Après application des différentes méthodes de sélection des features, nous avons obtenu un ensemble réduit de features qui ont été utilisées pour l'entraînement du modèle final. Les performances du modèle ont été évaluées à l'aide de métriques appropriées, montrant une amélioration significative par rapport à l'utilisation de l'ensemble complet des features. Les résultats détaillés sont présentés dans la section des résultats du projet.

## 4. Conclusion

La sélection des features est une étape essentielle pour optimiser les performances des modèles d'apprentissage automatique. En combinant plusieurs méthodes de sélection, nous avons pu identifier un ensemble de features pertinentes qui ont contribué à l'amélioration des résultats du modèle. Des analyses supplémentaires pourraient être envisagées pour affiner davantage la sélection des features et explorer d'autres techniques avancées.
