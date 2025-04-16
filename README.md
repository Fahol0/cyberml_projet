# Détection d’Anomalies & Attaques Adversariales – CYBERML
Projet réalisé dans le cadre du cours CyberML par :
Paul Giraud, Raphaël Hatte, Fabien Holard, Maui Tadeje

Ce projet a pour but de concevoir une chaîne de traitement pour la détection d'anomalies dans des données de cybersécurité industrielles et d'analyser la vulnérabilité des modèles face aux attaques adversariales.

## Dataset : SWaT (Secure Water Treatment)
Données issues d’un système d’assainissement d’eau, collectées toutes les secondes.

14 998 lignes, 80 colonnes dont 77 capteurs (pH, pression, concentrations…)

2 553 secondes simulées d’attaques (Switch ON/OFF, Close, Spoofing)

Pas de valeurs nulles

## Prétraitement des données
Parsing de champs JSON

Encodage des colonnes discrètes

Conversion des timestamps et mise en index

Normalisation des valeurs (z-score)

Suppression des colonnes cibles pour les modèles non-supervisés

## Détection d’anomalies
Deux méthodes ont été utilisées :

## Isolation Forest
Contamination fixée à 0.15

Résultats :

Accuracy : 76.44%

Precision : 28.22%

Recall : 24.78%

F1 Score : 26.44%

## One-Class SVM
Kernel RBF, γ = 0.001, ν = 0.2

Résultats :

Accuracy : 78.47%

Precision : 38.73%

Recall : 45.52%

F1 Score : 41.85%

#### Conclusion : One-Class SVM > Isolation Forest sur ce jeu de données

## Attaques adversariales
Étude de la robustesse des modèles via deux attaques :

1. Boundary Attack sur Random Forest
Modèle non différentiable (robuste de base)

Utilisation d’ART (Adversarial Robustness Toolbox)

Résultats visuellement dégradés mais attaque limitée

2. FGSM sur Neural Network (3 couches denses)
Implémentation avec TensorFlow + ART

Attaque par gradient rapide → forte chute de performance

Mise en évidence de la sensibilité des réseaux de neurones

## Visualisations
PCA des anomalies détectées

Matrices de confusion avant/après attaques

Comparaison visuelle des performances

## Dépendances
Python ≥ 3.10

scikit-learn

matplotlib

pandas

numpy

tensorflow

adversarial-robustness-toolbox

=> pip install -r requirements.txt

## Perspectives
Tester d’autres modèles robustes (ex : autoencoders, GANs)

Ajouter des métriques de robustesse spécifiques

Comparer plusieurs attaques : PGD, DeepFool, Carlini-Wagner…
