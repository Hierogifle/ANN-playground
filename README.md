# 🧠 ANN Playground

> **Exploration des réseaux de neurones artificiels** - Du concept théorique à l'implémentation pratique

## 🎯 Vue d'ensemble

**ANN Playground** est un projet éducatif complet qui explore l'univers des réseaux de neurones artificiels de type **Perceptron Multicouches (MLP)**. Ce projet combine théorie, expérimentation et implémentation pour maîtriser les concepts fondamentaux du Deep Learning.

### 🚀 Objectifs du projet

- 📚 **Comprendre** l'architecture des réseaux de neurones multicouches
- 🔬 **Expérimenter** avec TensorFlow Playground pour visualiser l'apprentissage
- 🎓 **Prédire** le décrochage et la réussite scolaire d'étudiants
- 💻 **Implémenter** un MLP from scratch avec NumPy
- ⚖️ **Comparer** les performances entre Keras et implémentation personnalisée

## 📊 Données

Le projet utilise le dataset **"Predict Students' Dropout and Academic Success"** de l'UCI Machine Learning Repository :

```python
from ucimlrepo import fetch_ucirepo

# Récupération des données
dataset = fetch_ucirepo(id=697)
X = dataset.data.features  # Variables explicatives
y = dataset.data.targets   # Variable cible (dropout/success)
```

## 🛠️ Technologies utilisées

- **Python 3.8+**
- **TensorFlow/Keras** - Pour l'implémentation des modèles MLP
- **NumPy** - Pour l'implémentation from scratch
- **Pandas** - Manipulation et analyse des données
- **Matplotlib/Seaborn** - Visualisations
- **Scikit-learn** - Métriques d'évaluation

## 📁 Structure du projet

```
ANN-playground/
├── 📓 notebooks/
│   └── ann_playground.ipynb   # Notebook principal avec analyse complète
├── 🐍 src/
│   └── mlp_class.py           # Classe MLP implémentée from scratch
├── 📊 data/
│   └── ...                    # Données (automatiquement téléchargées)
├── 📈 results/
│   └── ...                    # Graphiques et résultats d'expérimentations
├── 📋 requirements.txt        # Dépendances Python
└── 📖 README.md               # Ce fichier
```

## 🎯 Phases du projet

### 1. 🔍 **Veille théorique**
- Architecture des réseaux de neurones (couches d'entrée, cachées, sortie)
- Concepts clés : fonctions d'activation, rétropropagation, loss function
- Hyperparamètres et bonnes pratiques

### 2. 🎮 **Expérimentation avec TensorFlow Playground**
- Classification sur différents datasets
- Test de configurations variées (neurones, couches, learning rate)
- Analyse du phénomène de Vanishing Gradients

### 3. 📊 **Analyse de données réelles**
- Analyse exploratoire complète du dataset étudiant
- Preprocessing et nettoyage des données
- Visualisations des patterns de décrochage/réussite

### 4. 🤖 **Modélisation avec Keras**
- Construction d'architectures MLP variées
- Optimisation des hyperparamètres
- Techniques de régularisation (Dropout, Normalisation)

### 5. 💻 **Implémentation from scratch**
- Développement d'une classe MLP en NumPy pur
- Programmation orientée objet
- Comparaison avec l'implémentation Keras

## 📈 Métriques d'évaluation

- **Matrice de confusion** - Analyse détaillée des prédictions
- **Accuracy** - Taux de bonnes classifications
- **Rapport de classification** - Précision, Rappel, F1-Score
- **Courbes d'apprentissage** - Évolution des performances par epoch
- **Détection d'overfitting** - Analyse des écarts train/validation

## 🚀 Installation et utilisation

1. **Cloner le repository**
```bash
git clone https://github.com/[username]/ANN-playground.git
cd ANN-playground
```

2. **Installer les dépendances**
```bash
pip install -r requirements.txt
```

3. **Lancer le notebook**
```bash
jupyter notebook notebooks/ann_playground.ipynb
```

## 💡 Résultats clés

- ✅ **Modèle optimal** : Architecture à [X] couches cachées avec [Y] neurones
- 📊 **Performance** : Accuracy de [Z]% sur le jeu de test
- 🔄 **Comparaison** : Écart de performance entre Keras et implémentation NumPy
- 🎯 **Insights** : Facteurs principaux influençant le décrochage scolaire

## 🎓 Compétences développées

- **Deep Learning** - Compréhension approfondie des réseaux de neurones
- **Programmation** - Implémentation d'algorithmes complexes from scratch
- **Analyse de données** - Preprocessing et exploration de datasets réels
- **Visualisation** - Communication efficace des résultats

## 📚 Références

- [The Essential Main Ideas of Neural Networks](link)
- [Your First Deep Learning Project in Python with Keras Step-by-Step](link)
- [TensorFlow Playground](https://playground.tensorflow.org/)
- [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/index.php)