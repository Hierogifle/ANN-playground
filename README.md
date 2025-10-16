# ANN-playground
Ce projet ANN Playground explore les réseaux de neurones multicouches (MLP) pour des tâches de classification et régression. Il inclut une veille sur l'architecture, la compréhension des concepts clés, des tests d'hyperparamètres, et la comparaison entre un MLP Keras et un MLP développé en Python.

<<<<<<< HEAD
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

Pour une classification binaire → 1 neurone (activation sigmoïde).

Pour une classification multi-classe → 1 neurone par classe (activation softmax).

Pour une régression → 1 neurone sans activation (sortie linéaire).

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
🟢 Propagation avant (Forward Propagation)

Les données circulent de l’entrée vers la sortie, couche par couche :
=======
>>>>>>> d1b1a9761ff9bf4f065447479ccf6f3c68e74f62
