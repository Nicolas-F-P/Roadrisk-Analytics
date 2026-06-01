# Projet 3 - RoadRisk Analytics

### Dashboard Excel & Power BI sur les accidents corporels de la route en France

![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Excel](https://img.shields.io/badge/Excel-Analyse%20%26%20Power%20Query-217346?style=for-the-badge&logo=microsoftexcel&logoColor=white)
![Power Query](https://img.shields.io/badge/Power%20Query-Nettoyage%20des%20donn%C3%A9es-2E86C1?style=for-the-badge)
![DAX](https://img.shields.io/badge/DAX-KPI%20%26%20Measures-742774?style=for-the-badge)
![Portfolio](https://img.shields.io/badge/Projet-Portfolio%20Data%20Analyst-2E86C1?style=for-the-badge)


## Sommaire

- [Présentation du projet](#présentation-du-projet)
- [Objectifs métier](#objectifs-métier)
- [Dataset utilisé](#dataset-utilisé)
- [Outils utilisés](#outils-utilisés)
- [Structure du projet](#structure-du-projet)
- [Préparation des données](#préparation-des-données)
- [Modèle de données](#modèle-de-données)
- [Dashboard Excel](#dashboard-excel)
- [Dashboard Power BI](#dashboard-power-bi)
- [Mesures DAX principales](#mesures-dax-principales)
- [KPI principaux](#kpi-principaux)
- [Insights principaux](#insights-principaux)
- [Recommandations métier](#recommandations-métier)
- [Compétences démontrées](#compétences-démontrées)
- [Limites et pistes d’amélioration](#limites-et-pistes-damélioration)
- [Conclusion](#conclusion)


## Présentation du projet

Ce projet analyse les accidents corporels de la route en France à partir des données ouvertes BAAC 2024.

L’objectif est de construire une analyse complète permettant d’identifier les profils, périodes, zones et conditions les plus associées aux victimes d’accidents de la route.

Le projet couvre notamment :

- le bilan global des accidents corporels ;
- les victimes et victimes graves ;
- les profils d’usagers touchés ;
- les classes d’âge les plus représentées ;
- les conditions d’accident : route, météo, luminosité, état de surface ;
- la répartition géographique par département ;
- les recommandations de prévention.

Le projet a été réalisé avec une double approche :

1. **Excel / Power Query** pour le nettoyage, la préparation et un premier dashboard.
2. **Power BI / DAX** pour un rapport interactif multi-pages orienté analyse et recommandations.


## Objectifs métier

L’analyse cherche à répondre à plusieurs questions concrètes :

| Question métier | Objectif analytique |
|---|---|
| Quel est le bilan global des accidents corporels en 2024 ? | Mesurer le volume d’accidents, d’usagers et de victimes |
| Quels profils d’usagers sont les plus touchés ? | Identifier les types d’usagers et classes d’âge les plus représentés |
| Quelles conditions concentrent le plus de victimes graves ? | Analyser les routes, la météo, la luminosité et l’état de surface |
| Quels départements concentrent le plus de victimes ? | Préparer une lecture géographique des zones à surveiller |
| Quelles actions de prévention peuvent être proposées ? | Transformer les résultats en recommandations métier |


## Dataset utilisé

Le projet utilise les données publiques BAAC 2024 relatives aux accidents corporels de la circulation.

Source officielle :

> https://www.data.gouv.fr/datasets/bases-de-donnees-annuelles-des-accidents-corporels-de-la-circulation-routiere-annees-de-2005-a-2024/

Les fichiers utilisés sont :

| Fichier | Rôle dans l’analyse |
|---|---|
| `caract_2024.csv` | Informations principales sur l’accident : date, heure, météo, luminosité, commune, département, coordonnées |
| `lieux_2024.csv` | Informations sur le lieu : type de route, surface, vitesse maximale autorisée, infrastructure |
| `vehicules_2024.csv` | Informations sur les véhicules impliqués |
| `usagers_2024.csv` | Informations sur les personnes impliquées : gravité, sexe, âge, catégorie d’usager |

Une documentation officielle a également été utilisée pour comprendre les codes présents dans les fichiers sources.


## Outils utilisés

| Outil | Utilisation |
|---|---|
| **Excel** | Analyse exploratoire, tableaux croisés dynamiques, premier dashboard |
| **Power Query** | Import, nettoyage, transformation et enrichissement des fichiers CSV |
| **Power Pivot / Modèle de données Excel** | Relations entre tables et tests d’analyse |
| **Power BI Desktop** | Création du rapport interactif multi-pages |
| **DAX** | Création des mesures KPI |
| **CSV** | Format source des données |
| **GitHub** | Présentation et documentation du projet |


## Structure du projet

```text
Projet_03_RoadRisk_Analytics
│
├── data
│   ├── raw
│   │   ├── caract_2024.csv
│   │   ├── lieux_2024.csv
│   │   ├── vehicules_2024.csv
│   │   └── usagers_2024.csv
│   │
│   ├── clean
│   │   └── fichiers exportés ou nettoyés si besoin
│   │
│   └── references
│       └── description-des-bases-de-donnees-annuelles.pdf
│
├── excel
│   └── RoadRisk_Analytics_Excel.xlsx
│
├── powerbi
│   └── RoadRisk_Analytics.pbix
│
├── images
│   ├── excel
│   │   └── dashboard_excel.png
│   │
│   ├── powerbi
│   │   ├── 01_vue_ensemble.png
│   │   ├── 02_analyse_victimes.png
│   │   ├── 03_conditions_accident.png
│   │   ├── 04_analyse_geographique.png
│   │   └── 05_synthese_recommandations.png
│   │
│   └── data_model
│       ├── power_query_requetes.png
│       └── modele_relationnel_excel.png
│
├── docs
│   └── rapport_recruteur.pdf
│
└── README.md
```


## Préparation des données

Les données sources contiennent de nombreux codes numériques peu lisibles directement.

Exemple :

| Colonne brute | Exemple de code | Transformation créée |
|---|---:|---|
| `grav` | `2` | `Tué` |
| `catu` | `1` | `Conducteur` |
| `sexe` | `2` | `Féminin` |
| `lum` | `1` | `Plein jour` |
| `agg` | `2` | `En agglomération` |
| `catr` | `3` | `Route départementale` |

Les principales transformations réalisées avec Power Query :

- import des 4 fichiers CSV ;
- conservation des tables brutes `RAW` ;
- création de tables nettoyées `CLEAN` ;
- correction des types de données ;
- remplacement des erreurs par des valeurs nulles lorsque nécessaire ;
- création de colonnes lisibles à partir des codes sources ;
- création de colonnes d’analyse : âge, classe d’âge, tranche horaire, indicateurs binaires ;
- fusion des tables pour créer une table d’analyse finale utilisable dans Power BI.

### Requêtes principales

| Requête | Rôle |
|---|---|
| `RAW_Caracteristiques_2024` | Données accident brutes |
| `RAW_Lieux_2024` | Données lieux brutes |
| `RAW_Vehicules_2024` | Données véhicules brutes |
| `RAW_Usagers_2024` | Données usagers brutes |
| `CLEAN_Caracteristiques_2024` | Accidents nettoyés et enrichis |
| `CLEAN_Lieux_2024` | Lieux nettoyés et enrichis |
| `CLEAN_Vehicules_2024` | Véhicules nettoyés et catégorisés |
| `CLEAN_Usagers_2024` | Usagers nettoyés et enrichis |
| `DIM_Accident_2024` | Table d’accidents uniques |
| `DIM_Lieux_Principal_2024` | Table simplifiée du lieu principal |
| `FACT_Usagers_Analyse_2024` | Table finale d’analyse, une ligne par usager |


## Modèle de données

Le modèle initial repose sur l’identifiant commun :

```text
Num_Acc
```

Cet identifiant relie les informations des accidents, lieux, véhicules et usagers.

```text
DIM_Accident_2024
    │ Num_Acc
    ├── CLEAN_Usagers_2024
    ├── CLEAN_Lieux_2024
    └── CLEAN_Vehicules_2024
```

Pour simplifier l’analyse dans Power BI, une table finale a été créée :

```text
FACT_Usagers_Analyse_2024
```

Elle regroupe les informations utiles issues :

```text
CLEAN_Usagers_2024
+ DIM_Accident_2024
+ DIM_Lieux_Principal_2024
```

Cette table suit la logique :

```text
1 ligne = 1 usager impliqué dans un accident
```

Elle permet d’analyser facilement les victimes, les victimes graves, les profils d’usagers, les conditions d’accident et la géographie.


## Dashboard Excel

Un premier dashboard a été réalisé dans Excel à partir de Power Query et de tableaux croisés dynamiques.

Objectifs du dashboard Excel :

- valider les indicateurs principaux ;
- tester les regroupements de données ;
- créer une première lecture visuelle ;
- mettre en avant les compétences Excel avancées.

Indicateurs présents :

- nombre d’accidents ;
- usagers impliqués ;
- victimes ;
- victimes graves ;
- tués ;
- blessés hospitalisés ;
- taux de gravité.

Analyses présentes :

- victimes par tranche horaire ;
- victimes par classe d’âge ;
- victimes graves par type de route ;
- répartition de la gravité par type d’usager.

![Dashboard Excel](images/excel/dashboard_excel.png)


## Dashboard Power BI

Le rapport Power BI est composé de 5 pages principales.

### 1. Vue d’ensemble

Objectif : présenter le bilan global des accidents corporels de la route en 2024.

Indicateurs présents :

- accidents ;
- usagers impliqués ;
- victimes ;
- victimes graves ;
- taux de gravité.

Visualisations principales :

- victimes par tranche horaire ;
- victimes par classe d’âge ;
- victimes graves par type de route ;
- répartition de la gravité par type d’usager.

![Vue d’ensemble](images/powerbi/01_vue_ensemble.png)


### 2. Analyse des victimes

Objectif : comprendre les profils d’usagers les plus touchés.

Indicateurs présents :

- victimes ;
- victimes graves ;
- tués ;
- taux de gravité.

Visualisations principales :

- victimes par type d’usager ;
- victimes par sexe ;
- victimes graves par classe d’âge ;
- répartition de la gravité par type d’usager.

![Analyse des victimes](images/powerbi/02_analyse_victimes.png)


### 3. Conditions d’accident

Objectif : identifier les contextes associés aux victimes graves.

Indicateurs présents :

- victimes graves ;
- tués ;
- taux de gravité.

Visualisations principales :

- victimes graves par type de route ;
- victimes graves par luminosité ;
- victimes graves par météo ;
- victimes graves par état de surface.

![Conditions d’accident](images/powerbi/03_conditions_accident.png)


### 4. Analyse géographique

Objectif : visualiser la répartition territoriale des victimes.

Indicateurs présents :

- victimes ;
- victimes graves ;
- taux de gravité.

Visualisations principales :

- carte des accidents avec victimes graves ;
- poids des départements dans les victimes ;
- top départements par nombre de victimes ;
- synthèse par département.

![Analyse géographique](images/powerbi/04_analyse_geographique.png)


### 5. Synthèse & recommandations

Objectif : transformer l’analyse en constats, recommandations et limites.

Contenu principal :

- constats clés ;
- recommandations métier ;
- limites de l’analyse ;
- conclusion.

![Synthèse & recommandations](images/powerbi/05_synthese_recommandations.png)


## Mesures DAX principales

Les mesures suivantes ont été créées dans Power BI.

### Accidents

```DAX
Accidents = DISTINCTCOUNT('tbl_FACT_Usagers_Analyse_2024'[Num_Acc])
```

Cette mesure compte le nombre d’accidents uniques.

### Usagers impliqués

```DAX
Usagers impliqués = COUNTROWS('tbl_FACT_Usagers_Analyse_2024')
```

Cette mesure compte le nombre total d’usagers impliqués.

### Victimes

```DAX
Victimes = SUM('tbl_FACT_Usagers_Analyse_2024'[Est_Victime])
```

Cette mesure additionne les usagers blessés ou tués.

### Victimes graves

```DAX
Victimes graves = SUM('tbl_FACT_Usagers_Analyse_2024'[Est_Usager_Grave])
```

Cette mesure additionne les usagers tués ou blessés hospitalisés.

### Tués

```DAX
Tués = SUM('tbl_FACT_Usagers_Analyse_2024'[Est_Tue])
```

### Blessés hospitalisés

```DAX
Blessés hospitalisés = SUM('tbl_FACT_Usagers_Analyse_2024'[Est_Blesse_Hospitalise])
```

### Taux de gravité

```DAX
Taux de gravité = DIVIDE([Victimes graves], [Victimes])
```

Cette mesure calcule la part des victimes graves parmi l’ensemble des victimes.


## KPI principaux

| Indicateur | Résultat observé |
|---|---:|
| Accidents | ≈ 54,4K |
| Usagers impliqués | ≈ 125,2K |
| Victimes | ≈ 72,3K |
| Victimes graves | ≈ 22,6K |
| Tués | ≈ 3,4K |
| Blessés hospitalisés | ≈ 19,1K |
| Taux de gravité | ≈ 31,2 % |

> Les valeurs peuvent légèrement varier selon les filtres appliqués dans Power BI.


## Insights principaux

### Vue d’ensemble

- La base 2024 recense plus de 54 000 accidents corporels.
- Plus de 125 000 usagers sont impliqués.
- Environ 72 000 usagers sont victimes d’un accident.
- Près d’un tiers des victimes sont des victimes graves.

### Analyse des victimes

- Les conducteurs représentent la majorité des victimes.
- Les classes d’âge adultes, notamment 25-44 ans et 45-64 ans, sont fortement représentées.
- L’analyse par type d’usager permet de comparer les profils les plus exposés et les niveaux de gravité associés.

### Conditions d’accident

- Les routes départementales et les voies communales regroupent le plus grand nombre de victimes graves.
- Les conditions météo et de chaussée normales apparaissent majoritaires.
- Cette lecture doit être nuancée, car ces conditions correspondent aussi aux situations de circulation les plus fréquentes.

### Analyse géographique

- Certains départements concentrent davantage de victimes.
- Ces écarts peuvent refléter la densité de population, le volume de circulation et les caractéristiques locales du réseau routier.
- La carte permet d’identifier visuellement les zones à surveiller.


## Recommandations métier

À partir de l’analyse, plusieurs actions peuvent être proposées :

1. **Prioriser les actions de prévention sur les routes départementales et communales**, qui concentrent le plus grand nombre de victimes graves.
2. **Cibler les campagnes de sensibilisation sur les conducteurs adultes**, notamment les 25-64 ans.
3. **Renforcer les messages de prévention sur les trajets de l’après-midi et de fin de journée**, périodes fortement représentées parmi les victimes.
4. **Surveiller les zones à forte concentration de victimes**, afin d’orienter les actions locales.
5. **Compléter l’analyse avec des données de trafic**, pour mieux distinguer volume d’accidents et niveau réel de risque.


## Compétences démontrées

Ce projet met en avant plusieurs compétences attendues chez un Data Analyst junior :

| Compétence | Mise en pratique dans le projet |
|---|---|
| Excel avancé | Power Query, tableaux croisés dynamiques, dashboard Excel |
| Power Query | Nettoyage, typage, remplacement d’erreurs, fusion de tables |
| Power BI | Dashboard multi-pages, filtres, cartes KPI, visualisations interactives |
| DAX | Création de mesures KPI et taux de gravité |
| Modélisation | Organisation en tables RAW, CLEAN, DIM et FACT |
| Data cleaning | Recodage des variables et gestion des valeurs manquantes |
| Data visualization | Choix de graphiques adaptés aux questions métier |
| Analyse métier | Transformation des résultats en constats et recommandations |
| Communication | Synthèse finale et limites de l’analyse |


## Limites et pistes d’amélioration

Ce projet peut être enrichi avec plusieurs améliorations :

- intégrer des données de trafic routier pour calculer des taux de risque plus précis ;
- ajouter une table de correspondance entre codes département et noms de départements ;
- créer une analyse temporelle plus détaillée par jour de semaine ou par mois ;
- approfondir l’analyse des véhicules impliqués ;
- analyser plus précisément les équipements de sécurité ;
- améliorer la carte avec des zones géographiques plus détaillées ;
- publier le dashboard via Power BI Service si nécessaire.


## Conclusion

Ce projet montre comment exploiter des données publiques réelles pour produire une analyse structurée, lisible et orientée décision.

Il combine une préparation des données avancée avec Excel et Power Query, une restitution visuelle avec Power BI, et une lecture métier à travers des constats, recommandations et limites.

L’objectif final est de fournir un support d’aide à la décision permettant de mieux comprendre les profils, périodes, zones et conditions associés aux accidents corporels de la route.


**Projet réalisé dans le cadre d’un portfolio Data Analyst**
