# Machine Learning for Climate Risks  
## Analyse et prédiction des indices de sécheresse à partir de données spatiales et hydrométéorologiques

### Présentation du projet

Ce projet académique vise à **modéliser et prédire le SWI uniforme**, un indice d’humidité des sols utilisé comme référence réglementaire pour l’évaluation du risque sécheresse et l’éligibilité au dispositif **CATNAT** en France.  
L’objectif est double :  
- améliorer la **prédiction spatio-temporelle** du SWI uniforme,  
- détecter des **épisodes de sécheresse modérée et extrême** à partir de seuils statistiques.

Le projet combine des méthodes de **machine learning**, d’**analyse spatiale** et de **géostatistique**, appliquées à des données environnementales massives et hétérogènes.

---

### Données

Les données utilisées couvrent la période **1990–2025** et proviennent de plusieurs sources :
- variables hydrométéorologiques issues de SAFRAN (précipitations, évaporation, drainage, etc.),
- indices hydriques (SWI journalier et SWI uniforme mensuel),
- informations spatiales (coordonnées, limites communales IGN),
- caractéristiques des sols (argiles, propriétés physiques).

Les différentes sources ont été harmonisées spatialement (projection Lambert II étendu), agrégées et consolidées dans un **fichier Parquet unique**, servant de base à l’analyse exploratoire et à la modélisation :contentReference[oaicite:0]{index=0}.

---

### Méthodologie

Le workflow du projet est structuré en quatre grandes étapes :

1. **Analyse exploratoire spatio-temporelle**  
   Étude de la variabilité du SWI, des gradients régionaux et de la relation entre SWI brut et SWI uniforme.

2. **Modélisation du SWI uniforme**  
   Mise en place d’un benchmark de modèles (baselines, régression linéaire, Random Forest, Gradient Boosting), entraînés par grandes régions climatiques puis à l’échelle nationale.  
   Le **Gradient Boosting** est retenu comme modèle de référence pour ses performances et sa robustesse.

3. **Analyse spatiale des résidus**  
   Les résidus du modèle présentent une **autocorrélation spatiale significative**, mise en évidence par le **test de Moran** et l’analyse du **variogramme**, indiquant des biais locaux persistants.

4. **Approche hybride ML + modèle spatial**  
   Une approche innovante est proposée, combinant :
   - un modèle de machine learning pour capturer les relations globales,
   - une **correction spatiale par krigeage des résidus** afin de réduire l’autocorrélation spatiale des erreurs.

---

### Détection des sécheresses (CATNAT)

À partir du SWI uniforme prédit, des **seuils statistiques basés sur des quantiles historiques** (Q25 et Q05) sont définis par commune et par trimestre.  
Ces seuils permettent d’identifier :
- des épisodes de sécheresse modérée,
- des épisodes de sécheresse extrême,

en cohérence avec les logiques réglementaires du régime CATNAT.

---

### Résultats principaux

- Les modèles d’ensemble, en particulier le **Gradient Boosting**, offrent d’excellentes performances prédictives (R² > 0.97).
- Les résidus présentent une structure spatiale non aléatoire, confirmée statistiquement.
- L’approche hybride **ML + correction spatiale** permet :
  - une réduction nette de l’autocorrélation spatiale des erreurs,
  - des résidus plus proches d’un bruit spatialement indépendant,
  - une amélioration de la fiabilité locale des prédictions.
- La détection des sécheresses par quantiles montre une très bonne capacité à identifier les événements observés.

---

### Perspectives

Le projet met en évidence l’intérêt d’intégrer explicitement la dimension spatiale dans les modèles prédictifs de risques climatiques.  
Des pistes d’amélioration incluent :
- des modèles globaux enrichis par des variables de contexte spatial,
- des approches de **clustering spatial** pour définir des régimes hydrologiques homogènes,
- une extension de l’analyse sur des périodes plus longues.

---

### Auteurs

Projet académique réalisé par :  
- **Charlotte Cegarra**  
- **Sandrine Agugliaro**  

Année universitaire **2025–2026**

---

Ce dépôt correspond à un **travail académique exploratoire**. Les résultats ne constituent pas une application opérationnelle directe, mais une base méthodologique pour l’analyse et la modélisation des risques climatiques.
