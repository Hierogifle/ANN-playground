# ANN-playground
Ce projet ANN Playground explore les réseaux de neurones multicouches (MLP) pour des tâches de classification et régression. Il inclut une veille sur l'architecture, la compréhension des concepts clés, des tests d'hyperparamètres, et la comparaison entre un MLP Keras et un MLP développé en Python.
# Veille théorique

# I Architecture des réseaux de neurones
# 1 Principe général

Les réseaux de neurones artificiels (ANN – Artificial Neural Networks) sont des modèles d’apprentissage automatique inspirés du fonctionnement biologique du cerveau.
Ils sont constitués d’unités appelées neurones artificiels, organisées en couches interconnectées. Chaque neurone reçoit des signaux, les pondère, les additionne, applique une fonction d’activation et transmet la sortie à la couche suivante.

# 2 Structure d’un réseau

Un réseau de neurones typique est constitué de trois types de couches :

- Couche d’entrée (Input Layer)
Représente les variables explicatives (features) du problème.
Chaque neurone correspond à une variable d’entrée.
Aucun calcul complexe n’y est effectué : cette couche transmet simplement les données à la première couche cachée.

- Couches cachées (Hidden Layers)
Effectuent la transformation non linéaire des données d’entrée.
Chaque neurone calcule une somme pondérée de ses entrées, ajoute un biais, puis applique une fonction d’activation :
    
    z⁽ˡ⁾ = W⁽ˡ⁾ · a⁽ˡ⁻¹⁾ + b⁽ˡ⁾,   a⁽ˡ⁾ = φ(z⁽ˡ⁾)


Les couches cachées permettent au réseau d’apprendre des représentations internes plus abstraites et puissantes des données.
Plus il y a de couches cachées, plus le réseau peut modéliser des relations complexes.

- Couche de sortie (Output Layer)

Produit le résultat final du modèle :

  -Pour une classification binaire → 1 neurone (activation sigmoïde).
  -Pour une classification multi-classe → 1 neurone par classe (activation softmax).
  -Pour une régression → 1 neurone sans activation (sortie linéaire).

# II Concepts clés
# 1 Fonction d’activation
Les fonctions d’activation introduisent la non-linéarité nécessaire pour apprendre des relations complexes. Sans elles, le réseau ne ferait qu’une simple transformation linéaire.
Quelques fonctions courantes :

| Fonction     | Expression                                     | Domaine de sortie | Particularités                                            |
|--------------|------------------------------------------------|-------------------|-----------------------------------------------------------|
| **Sigmoïde** | σ(z) = 1 / (1 + e⁻ᶻ)                          | (0, 1)            | Idéale pour probabilités mais provoque vanishing gradient |
| **Tanh**     | tanh(z) = (eᶻ - e⁻ᶻ) / (eᶻ + e⁻ᶻ)              | (-1, 1)           | Centrée, meilleure que Sigmoïde                           |
| **ReLU**     | ReLU(z) = max(0, z)                            | [0, ∞)            | Très utilisée, efficace en Deep Learning                  |
| **Softmax**  | softmax(zᵢ) = eᶻⁱ / Σ eᶻʲ                     | (0, 1), somme = 1 | Utilisée en sortie pour classification multi-classe       |

# 2 Propagation et rétropropagation
🟢 Propagation avant (Forward Propagation)²notepad
Les données circulent de l’entrée vers la sortie, couche par couche :

   a⁽ˡ⁾ = φ(W⁽ˡ⁾ · a⁽ˡ⁻¹⁾ + b⁽ˡ⁾)

où :
- **W⁽ˡ⁾** : matrice des poids de la couche *l*
- **b⁽ˡ⁾** : biais de la couche *l*
- **φ** : fonction d’activation
- **a⁽ˡ⁾** : sortie (activation) de la couche *l*

Le réseau calcule la sortie ^y à partir des entrées x.

🔴 Rétropropagation (Backpropagation)

C’est la phase d’apprentissage du réseau.
Elle consiste à calculer l’erreur entre la sortie réelle 
𝑦 et la sortie prédite, puis à ajuster les poids pour la réduire :

   wᵢ ← wᵢ − η · (∂L / ∂wᵢ)
où :
- **η** : taux d’apprentissage (*learning rate*)
- **∂L / ∂wᵢ** : gradient de la fonction de perte par rapport au poids *wᵢ*

La rétropropagation applique la règle de la chaîne pour propager les gradients depuis la sortie vers les premières couches.

# 3 Fonction de perte (Loss Function)
Elle mesure l’écart entre la prédiction et la vérité.
Le but de l’apprentissage est de minimiser cette perte.

| Type de tâche              | Fonction de perte                | Expression                                       | Description |
|-----------------------------|----------------------------------|--------------------------------------------------|--------------|
| **Régression**             | Mean Squared Error (MSE)         | L = (1/n) Σ (yᵢ − ŷᵢ)²                           | Mesure l’écart quadratique moyen entre les vraies et les prédictions |
| **Régression robuste**     | Mean Absolute Error (MAE)        | L = (1/n) Σ |yᵢ − ŷᵢ|                            | Moins sensible aux valeurs extrêmes que MSE |
| **Classification binaire** | Binary Cross-Entropy             | L = −[y log(ŷ) + (1 − y) log(1 − ŷ)]             | Mesure la distance entre la prédiction et la probabilité réelle |
| **Classification multi**   | Categorical Cross-Entropy        | L = −Σ yᵢ log(ŷᵢ)                                | Utilisée avec une sortie Softmax |
| **Régularisation**         | L2 (Weight Decay)                | L = (1/2λ) Σ wᵢ²                                 | Empêche les poids de devenir trop grands |

# 4 Descente de gradient
C’est l’algorithme d’optimisation utilisé pour mettre à jour les poids :
L’objectif est de **minimiser la fonction de perte** (*Loss Function*)  
en ajustant progressivement les paramètres du modèle.

La règle de mise à jour des poids est :

θ ← θ − η · ∇θL

où :
- **θ** : ensemble des paramètres du modèle (poids et biais)
- **η** : *learning rate* (taux d’apprentissage)
- **∇θL** : gradient de la fonction de perte par rapport à θ

# 5 Vanishing Gradient
Problème rencontré lors de l’entraînement des réseaux profonds :
les gradients deviennent très faibles dans les premières couches, bloquant l’apprentissage.
Causes :

-Fonctions saturantes (sigmoid, tanh)
-Mauvaise initialisation des poids
   Solutions :
-Utiliser ReLU, LeakyReLU
-Initialisations He ou Xavier
-Batch Normalization ou Skip Connections

# III Hyperparamètres et bonnes pratiques
# 1 Principaux hyperparamètres

| Hyperparamètre                   | Rôle                                       | Bonnes pratiques                                                       |
| -------------------------------- | ------------------------------------------ | ---------------------------------------------------------------------- |
| **Learning Rate (η)**            | Contrôle la vitesse d’apprentissage        | Trop grand → instable, trop petit → lent ; souvent entre 0.001 et 0.01 |
| **Nombre de couches / neurones** | Définit la capacité du réseau              | Commencer petit, augmenter si sous-apprentissage                       |
| **Batch Size**                   | Taille des lots de données par mise à jour | 32 à 128 généralement                                                  |
| **Époques (Epochs)**             | Nombre de passages sur le dataset          | Surveiller la perte sur validation, utiliser *early stopping*          |
| **Optimiseur**                   | Méthode d’ajustement des poids             | Adam recommandé en pratique                                            |
| **Régularisation (Dropout, L2)** | Réduit le surapprentissage                 | Dropout entre 0.1 et 0.5                                               |
| **Initialisation des poids**     | Améliore la convergence                    | He pour ReLU, Xavier pour Tanh                                         |
| **Scheduler du learning rate**   | Ajuste η pendant l’entraînement            | Réduction progressive pour stabiliser la fin de l’apprentissage        |

# Conclusion

Le Perceptron Multicouches (MLP) constitue la base du Deep Learning moderne.
Grâce à ses couches cachées et à la rétropropagation, il peut modéliser des relations non linéaires complexes.
Son efficacité dépend fortement :

  -d’une bonne architecture,
  -d’un choix judicieux des fonctions d’activation,
  -et d’un réglage précis des hyperparamètres.
  -Une compréhension solide de ces concepts théoriques est indispensable avant de passer à la mise en œuvre pratique du modèle.


	​


