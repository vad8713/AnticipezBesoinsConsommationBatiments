# 🏢 Anticipez les besoins en consommation des bâtiments

Prédiction de la consommation énergétique totale et des émissions de gaz à effet de serre (GES) de bâtiments non résidentiels à partir de leurs caractéristiques structurelles, sans recourir à des relevés de consommation coûteux.

## 📌 Contexte

Une ville souhaite atteindre la neutralité carbone en 2050 et doit, pour cela, mieux cibler ses efforts de rénovation énergétique. Des relevés de consommation existent déjà pour les bâtiments non résidentiels, mais leur collecte est coûteuse. L'objectif est de démontrer qu'il est possible de **prédire ces valeurs à partir des seules caractéristiques du bâtiment** (surface, usage, année de construction, localisation, etc.), afin de se passer de nouvelles campagnes de mesure.

## 🎯 Objectifs

- Explorer et nettoyer un jeu de données de bâtiments (types, surfaces, localisation, usages, consommations).
- Identifier et sélectionner les variables pertinentes pour la modélisation.
- Prédire deux cibles :
  - la consommation énergétique totale (`SiteEnergyUse(kBtu)`) ;
  - les émissions totales de GES (`TotalGHGEmissions`).
- Évaluer l'apport du score **ENERGY STAR** dans la qualité des prédictions.
- Comparer plusieurs familles de modèles de régression et interpréter les résultats.

## 🗂️ Données

Le projet s'appuie sur le jeu de données public **Building Energy Benchmarking** de la ville de Seattle (consommations et caractéristiques des bâtiments non résidentiels). Les données ne sont pas incluses dans ce dépôt ; elles sont attendues au format CSV en entrée du premier notebook.

## 📁 Structure du projet

| Fichier | Description |
|---|---|
| `consommation_1_notebook_exploratoire.ipynb` | Exploration, nettoyage et sélection des variables (valeurs manquantes, doublons, corrélations, usages non pertinents, analyse de la localisation). |
| `consommation_2_notebook_prediction.ipynb` | Modélisation de la cible **Energie**, avec et sans le score ENERGY STAR. |
| `consommation_3_notebook_prediction.ipynb` | Modélisation de la cible **Émissions de GES (TotalGHGEmissions)**, avec et sans le score ENERGY STAR. |

## 🧰 Technologies utilisées

- **Python**, **Pandas**, **NumPy**
- **Matplotlib**, **Seaborn**, **missingno** (visualisation, valeurs manquantes)
- **Scikit-learn** : `StandardScaler`, `OneHotEncoder`, `KNNImputer`
- Modèles de régression : `LinearRegression`, `Ridge`/`RidgeCV`, `Lasso`/`LassoCV`, `DecisionTreeRegressor`, `RandomForestRegressor`, `GradientBoostingRegressor`
- **SHAP** pour l'interprétabilité des modèles
- `GridSearchCV` / validation croisée manuelle pour l'optimisation des hyperparamètres

## 🔍 Démarche

1. **Nettoyage** : suppression des colonnes non pertinentes, à faible variance, trop corrélées ou avec plus de 50 % de valeurs manquantes ; exclusion des bâtiments à usage familial.
2. **Sélection des variables** : étude des corrélations (heatmap), analyse de la localisation (répartition géographique par district).
3. **Modélisation** : centrage-réduction des données, entraînement de plusieurs modèles linéaires et non linéaires, recherche des meilleurs hyperparamètres.
4. **Évaluation** : comparaison des modèles via RMSE / R², avec et sans le score ENERGY STAR comme variable explicative.
5. **Interprétation** : analyse des variables les plus influentes avec SHAP.

## 👤 Auteur

David Depouez — Projet réalisé dans le cadre de la formation *Ingénieur Machine Learning (OpenClassrooms, RNCP niv. 7)*.
