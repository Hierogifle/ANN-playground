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

# Expérimentation avec TensorFlow Playground

Cette phase vise à explorer visuellement le fonctionnement d’un réseau de neurones multicouche grâce à **TensorFlow Playground**.
C'est un outil interactif permettant de:
  -tester différentes architectures (nombre de couches et de neurones),

  -modifier les hyperparamètres (fonction d’activation, taux d’apprentissage, bruit, etc.),

  -observer en direct l’évolution de la loss et de la frontière de décision.

L’objectif est de comprendre comment chaque paramètre influence la convergence, la généralisation et la stabilité du réseau.

# 1 Classification sur différents datasets


| Dataset   | Description                             | Objectif |
|-----------|-----------------------------------------|----------|
| **Circle**  | Deux cercles imbriqués                  | Tester la capacité à apprendre des frontières non linéaires simples |
| **XOR**     | Quatre groupes formant une croix        | Vérifier si le réseau peut apprendre des interactions complexes entre features |
| **Spiral**  | Points en spirales imbriquées           | Évaluer la puissance d’un MLP pour modéliser des motifs très complexes |
| **Gaussian**| Deux (ou plusieurs) nuages gaussiens    | Tester la séparation quand les classes sont centrées autour de distributions normales (souvent linéairement séparables si peu de recouvrement) |

Observation:

  -Les datasets **Circle et XOR** peuvent être correctement appris avec 1 couche cachée et quelques neurones.
  -Le dataset **Spiral** nécessite plusieurs couches et des activations non linéaires (ReLU, Tanh) pour obtenir une frontière correcte.
  -Le dataset **Gaussian** (nuages gaussiens) est souvent le plus simple : quand les clusters ont peu de recouvrement, une **frontière linéaire** suffit et un perceptron simple apprend très vite. En présence d’un fort recouvrement (variance élevée), le problème devient plus difficile et demande soit plus de capacité (neurones/couches) soit des features non-linéaires.

# 2 Test de configurations variées
Cette étape consiste à modifier les principaux hyperparamètres pour comprendre leur impact sur l’apprentissage.

# a. Nombre de couches et de neurones

**Manipulations**
  -1 à 3 couches cachées
  -1 → 8 neurones par couche
  -Fonction d’activation : ReLU
  -Learning Rate : 0.01
  -100 % des données pour l’entraînement

**Résultats observés**
| Configuration          | Test Loss | Training Loss | Observation                                                   |
| ---------------------- | --------- | ------------- | ------------------------------------------------------------- |
| 1 couche – 1 neurone   | 0.43      | 0.38          | Modèle trop simple, frontière quasi linéaire (*underfitting*) |
| 1 couche – 4 neurones  | 0.23      | 0.13          | Bonne convergence, frontière courbée, bon compromis           |
| 1 couche – 6 neurones  | ≈ 0       | ≈ 0           | Sur-apprentissage, réseau “mémorise” les données              |
| 2 couches – 4 neurones | 0.27      | 0.20          | Meilleur ajustement mais pas de gain net                      |
| 3 couches – 8 neurones | ≈ 0       | ≈ 0           | Overfitting total, vanishing gradient visible avec Sigmoid    |

**Interprétation**

**Trop peu de neurones** : le modèle n’a pas assez de paramètres pour apprendre des relations complexes.

**Trop de neurones/couches** : la loss d’entraînement chute à 0, mais la loss de test reste élevée → overfitting (en observant la courbe).

L’ajout de couches accroît la capacité du modèle mais complexifie la descente de gradient ; avec des activations saturantes (Sigmoid), cela cause le **vanishing gradient**.

# b. Fonction d’activation

Comparaison entre : **Sigmoid, Tanh et ReLU**

**Résultats**
| Activation     | Comportement de la Loss                          | Analyse                                                               |
| -------------- | ------------------------------------------------ | --------------------------------------------------------------------- |
| **Sigmoid**    | Convergence lente, plateau                       | Gradients s’annulent ; apprentissage difficile (*vanishing gradient*) |
| **Tanh**       | Descente plus fluide                             | Centrée ; réduit le biais ; mais risque de saturation                 |
| **ReLU**       | Convergence rapide et stable                     | Évite le vanishing gradient, favorise la propagation des erreurs      |

**Interprétation**
  -**Sigmoid/Tanh** : compressent fortement les valeurs → pertes d’information et gradients quasi nuls dans les couches profondes.

  -**ReLU** : conserve un gradient constant pour les valeurs positives → apprentissage plus rapide.

Sur le dataset **Spiral**, **Tanh** converge plus lentement mais plus douce et **RuLU** chute rapidement puis se stabilise.

# c. Taux d’apprentissage (Learning Rate η)

**Manipulations**
η ∈ { 0.1 ; 0.01 ; 0.001 ; 0.0001 }

**Résultats**
| η      | Test Loss         | Training Loss     | Observation                                              |
| ------ | ----------------- | ----------------- | -------------------------------------------------------- |
| 0.1    | Forte oscillation | Forte oscillation | Trop grand : le modèle saute le minimum                  |
| 0.01   | 0.51              | 0.43              | Apprentissage rapide mais instable                       |
| 0.001  | 0.47              | 0.47              | Apprentissage lent mais stable, meilleure généralisation |
| 0.0001 | > 0.6             | > 0.6             | Très lent, stagnation, gradients faibles                 |

**Interprétation**
  -**η trop élevé** → perte qui oscille ou diverge.

  -**η trop faible** → apprentissage extrêmement lent.

  -**η ≈ 0.001** offre le meilleur compromis vitesse/stabilité.

# 3 Analyse du phénomène de Vanishing Gradient

**Définition**
Le vanishing gradient survient quand les gradients deviennent trop petits dans les couches proches de l’entrée, empêchant ces couches d’être mises à jour correctement.

**Expérimentation**
Architecture : 4 couches cachées, activation Sigmoid.
Observation :
  -Les couches d’entrée restent quasiment inactives (couleurs statiques).
  -La loss stagne après quelques itérations.

**Solution testée**
Passage à **ReLU** : les neurones s’activent de nouveau, la loss diminue rapidement.

# Synthèse
| Paramètre                | Effet observé                                      | Interprétation                         |
| ------------------------ | -------------------------------------------------- | -------------------------------------- |
| + de neurones            | Capacité accrue                                    | Risque d’overfitting                   |
| + de couches             | Représentation complexe                            | Risque de vanishing gradient           |
| **ReLU**                 | Apprentissage stable                               | Recommandée pour couches cachées       |
| **Sigmoid/Tanh**         | Saturation des gradients                           | À éviter dans les réseaux profonds     |
| **Learning Rate élevé**  | Oscillations                                       | Instabilité du modèle                  |
| **Learning Rate faible** | Convergence lente                                  | Stagnation                             |

# Conclusion

Ces expérimentations confirment que :

Le nombre de neurones et la profondeur du réseau doivent être adaptés à la complexité du problème.

Le choix de la fonction d’activation influence directement la propagation du gradient et la stabilité de l’apprentissage.

Un learning rate modéré (≈ 0.001) donne la meilleure stabilité.

Les phénomènes observés (overfitting, oscillations, vanishing gradient) illustrent parfaitement les défis du Deep Learning.

Ces observations serviront de base à la phase de modélisation avec Keras.