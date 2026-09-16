# Classification des demandes d’hébergement

Projet consacré à la préparation et à la modélisation de demandes d’hébergement. L’objectif est de prédire la variable `granted_number_of_nights`, qui comporte quatre classes (`0`, `1`, `2` et `3`), à partir des informations relatives aux demandes et aux individus concernés.

## Objectif du projet

Le projet met en place un pipeline complet permettant de :

- explorer et nettoyer les données ;
- traiter les valeurs manquantes et les valeurs incohérentes ;
- construire des features ;
- fusionner les informations issues des tables `requests` et `individuals` ;
- entraîner un modèle de classification multiclasse ;

## Données

Les données sont réparties dans quatre fichiers :

| Fichier | Contenu |
| --- | --- |
| `requests_train.csv` | Demandes utilisées pour l’entraînement |
| `requests_test.csv` | Demandes utilisées pour le test |
| `individuals_train.csv` | Individus associés aux demandes d’entraînement |
| `individuals_test.csv` | Individus associés aux demandes de test |

Les fichiers CSV ne sont pas versionnés dans ce dépôt. Ils doivent être placés localement dans le dossier `data/`.

## Structure du projet

```text
housing-assistance-classification/
├── data/                         # Données brutes et nettoyées (non versionnées)
├── models/                       # Modèles entraînés (non versionnés)
├── 01-data-preparation.ipynb     # Exploration, nettoyage et export
├── 02-modelisation.ipynb         # Feature engineering et modélisation
├── .gitignore
├── README.md
└── requirements.txt
```

## Contenu des notebooks

### 1. Préparation des données

Le notebook `01-data-preparation.ipynb` contient :

- le chargement et l’exploration des quatre datasets ;
- la conversion des colonnes de dates ;
- l’analyse des valeurs manquantes ;
- le traitement des identifiants codés avec la valeur `-1` ;
- la correction des variables catégorielles et numériques ;
- la vérification des doublons et des identifiants ;
- l’analyse de la variable cible ;
- l’identification de variables pouvant provoquer une fuite de données, notamment `answer_creation_date` ;
- l’export des quatre datasets nettoyés.

### 2. Modélisation

Le notebook `02-modelisation.ipynb` contient actuellement :

- la création de variables démographiques et temporelles ;
- l’agrégation des individus au niveau de chaque demande ;
- la création d’indicateurs de vulnérabilité ;
- la fusion des caractéristiques avec les demandes ;
- l’étude des relations entre les variables et la cible ;
- une séparation entraînement/validation avec `StratifiedGroupKFold` afin qu’un même groupe ne soit pas présent dans les deux ensembles ;
- l’entraînement de deux configurations de `CatBoostClassifier` ;
- l’utilisation de pondérations pour mieux prendre en compte les classes minoritaires ;
- l’early stopping et la sauvegarde du meilleur modèle.

## Installation

### 1. Cloner le dépôt

```bash
git clone https://github.com/cyrinenighaoui/housing-assistance-classification.git
cd housing-assistance-classification
```

### 2. Créer un environnement virtuel

Sous Windows :

```bash
python -m venv .venv
.venv\Scripts\activate
```

Sous macOS ou Linux :

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Installer les dépendances

```bash
pip install -r requirements.txt
```

## Utilisation

1. Créer un dossier `data/` à la racine du projet.
2. Ajouter les quatre fichiers CSV bruts dans ce dossier.
3. Exécuter `01-data-preparation.ipynb` pour générer les fichiers nettoyés.
4. Exécuter `02-modelisation.ipynb` pour créer les features et entraîner les modèles.

Les fichiers nettoyés suivants seront générés dans `data/` :

```text
requests_train_clean.csv
requests_test_clean.csv
individuals_train_clean.csv
individuals_test_clean.csv
```

## Technologies utilisées

- Python
- pandas et NumPy
- Matplotlib et Seaborn
- scikit-learn
- CatBoost
- Jupyter Notebook


## Auteur

**Cyrine Nighaoui**  
Master Informatique — Machine Learning 
