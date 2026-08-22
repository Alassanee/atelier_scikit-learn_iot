# atelier_scikit-learn_iot
# Atelier Scikit-learn – Classification de l'état des capteurs IoT

## 📋 Contexte

Une entreprise possède plusieurs bâtiments équipés de capteurs IoT collectant en continu des données de **température**, **humidité**, **pression** et **consommation énergétique**. Chaque mesure est associée à un état : `OK`, `ALERTE` ou `ERREUR`.

**Objectif :** construire un modèle de Machine Learning capable de prédire automatiquement l'état d'un capteur à partir de ses mesures.

## 🔄 Workflow du projet

```
Dataset → Chargement → Exploration → Nettoyage → X / y → Train / Test 
→ Prétraitement → Encodage → Modèle → fit() → predict() → Évaluation 
→ Sauvegarde → Chargement → Réutilisation → Optimisation (v2)
```

## 📁 Structure du projet

```
atelier_scikit-learn_iot/
│
├── data/
│   └── mesures_capteurs.csv
├── notebooks/
│   └── atelier_scikit-learn_iot.ipynb
├── models/
│   ├── modele_capteur.joblib
│   ├── modele_capteur.pkl
│   ├── modele_capteur_v2.joblib
│   └── modele_capteur_v2.pkl
└── README.md
```

## 🛠️ Prérequis

- Python 3.x
- pandas
- numpy
- scikit-learn
- seaborn
- matplotlib
- joblib

Installation des dépendances :
```bash
pip install pandas numpy scikit-learn seaborn matplotlib joblib
```

## 🧭 Étapes de l'atelier

### Partie 0 – Mise en place de l'environnement
Structuration du projet, import du dataset `mesures_capteurs.csv` dans un DataFrame `df` et exploration initiale.

### Partie 1 – Gestion des doublons
Détection et suppression des doublons éventuels dans `df`.

### Partie 2 – Sélection de X et y
- **Cible (y)** : `etat`
- **Caractéristiques (X)** : `temperature`, `humidite`, `pression`, `consommation`

Type de problème : **classification multi-classe** (3 classes : OK, ALERTE, ERREUR).

### Partie 3 – Découpage Train/Test
Split 80/20 avec `random_state` fixé pour la reproductibilité et `stratify=y` pour conserver les proportions de classes.

### Partie 4 – Gestion des valeurs manquantes
Imputation par la **médiane** via `SimpleImputer` (robuste aux valeurs aberrantes, contrairement à la moyenne).

### Partie 5 – Mise à l'échelle
Standardisation des données avec `StandardScaler` (fit sur `X_train`, transform sur `X_train`/`X_test`).

### 🎁 Bonus intégré – Encodage de la cible avant l'entraînement
Avant la Partie 6, encodage de la variable cible `etat` (OK / ALERTE / ERREUR) avec `OrdinalEncoder`, nécessaire car scikit-learn travaille sur des données tabulaires numériques.

### Partie 6 – Entraînement et prédiction (KNN)
Modèle **K-Nearest Neighbors** (k=5), entraînement sur `X_train_scaled` / `y_train_encoded`, prédiction sur `X_test_scaled`.

### Partie 7 – Évaluation du modèle
- Accuracy
- Matrice de confusion (visualisée avec Seaborn)
- Rapport de classification (precision, recall, F1-score)

| Métrique | Cas d'usage indiqué |
|---|---|
| Accuracy | Classes équilibrées |
| Precision | Coût élevé des fausses alertes |
| Recall | Coût élevé des faux négatifs (ex: classe `ERREUR`) |
| F1-score | Classes déséquilibrées, compromis precision/recall |

### Partie 8 – Sauvegarde du modèle
Sauvegarde avec **Joblib** (`modele_capteur.joblib`) et **Pickle** (`modele_capteur.pkl`).

### Partie 9 – Chargement et réutilisation
Rechargement du modèle sauvegardé et prédiction sur une nouvelle mesure.

### 🎁 Partie 10 – Bonus : optimisation des hyperparamètres (modèle v2)
Ajustement des hyperparamètres du modèle KNN via `GridSearchCV` (ex: `n_neighbors`, `weights`, `metric`) afin d'obtenir une version optimisée **v2** du modèle, sauvegardée séparément dans `models/modele_capteur_v2.joblib` et `.pkl`.

## ▶️ Utilisation

```bash
jupyter notebook notebooks/atelier_scikit-learn_iot.ipynb
```

## 📦 Livrable

Dépôt public GitHub contenant l'ensemble du dossier `atelier_scikit-learn_iot`, mis à jour au fur et à mesure via des commits explicites.

## 👤 Auteur

Alassane Mbengue: Master 2 Cyber Sécurité UCAD
Orange Digital Center
@bl4ckcyph3r
