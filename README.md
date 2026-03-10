## README 

**Introduction**

Ce projet s'inscrit dans le cadre de ma candidature à la formation Data Analyst proposée par OpenClassrooms, et financée par France Travail, dans le contexte de mon projet de reconversion professionnelle, accompagné et validé par un conseiller France Travail.

Le dataset utilisé contient le registre des transactions d'une entreprise fictive dans le secteur de la vente au détail.

L'objectif est d'identifier des dynamiques commerciales et des comportements clients afin de produire des insights exploitables pour la prise de décision.

Cette étude est organisée en deux étapes : 

* La première partie (Notebook 1) sera dédiée au nettoyage et transformation des données.

* La deuxième partie (Notebook 2) se concentrera sur l'analyse exploratoire de ces données nettoyées et sur la compréhension des enjeux business.
________
**Notebook 1** - Préparation des données

Avant l’analyse, un travail de nettoyage et de transformation des données a été réalisé.

Cette étape a consisté à :
* contrôler la qualité des données (doublons, valeurs manquantes, types de variables) 
* vérifier la cohérence entre les tables
* créer plusieurs variables dérivées utiles à l’analyse (Age, Age_Group, Price_Bucket, variables temporelles).

Une variable monétaire Total_Net a également été calculée au niveau transactionnel afin de mesurer le chiffre d’affaires net par ligne de vente, en intégrant le prix du produit (depuis la table Produits), la quantité et le discount appliqué.

Les données ont ensuite été structurées selon une logique analytique fact/dimensions, avec deux tables principales :

* fact_sales — granularité : 1 ligne = 1 produit par commande
* fact_sales_order — granularité : 1 ligne = 1 commande

![Data Modeling](/slides/data_modeling.png)

Ce dataset préparé constitue la base utilisée dans le Notebook 2 pour l’analyse.
___________
**Notebook 2** - Analyse exploratoire et insights business

**Contexte/Scope**

Une forte disparité temporelle est observée dans les données, avec un changement important d’échelle du business à partir de 2023.

Afin d’éviter toute interprétation biaisée, le périmètre de l’analyse est donc défini sur la période 2023–2026.

![Distribution des commandes dans le temps](/slides/charts/orders_distribution.png)

**Aperçu KPIs**

Période : 02/2023-02/2026
Volume de commandes : 11 889
Nombre de clients actifs : 4 568
Chiffre d'affaires Net : 15 911 429€
Panier Moyen : 1 338€
Panier Médian (panier "typique") : 607€

**Premiers Constats**

La distribution du chiffre d’affaires est fortement asymétrique (panier moyen nettement supérieur au panier médian), ce qui indique la présence de commandes de très forte valeur.

![Tendances mensuelles sur la période](/slides/charts/monthly_trends_per_year.png)

**Question analytique**

Qu’est-ce qui explique la croissance du chiffre d'affaires après 2023 ?

**Hypothèses**

1. Acquisition des nouveaux clients.
2. Augmentation de la fréquence d'achats des clients existants.
3. Concentration des achats sur certains segments ou produits.

**Principaux résultats**

1. Acquisition clients
* vague d'acquisition importante en 2023 : 
53.8% de nouveaux clients contribuant à 64% du chiffre d'affaires (constitue la base des clients).
![Carte de chaleur d'acquisition](/Project/slides/charts/acquisition.png)

2. Structure du comportement d'achat
* segment Occasional dominant : représentant 69.5% du chiffre d'affaires.
![Distribution des clients vs CA par Fréquence](/Project/slides/charts/frequency_segments.png)

3. La fréquence d'achat des clients existants contribue au chiffre d'affaires, mais son impact reste modéré (~24 %).
![Corrélation entre variation de fréquence et variation du CA](/Project/slides/charts/frequency_revenue_corr.png)

4. Concentration client
*  6.9 % des clients génèrent 31 % du chiffre d’affaires, ce qui indique la présence d’un groupe restreint de gros acheteurs.
![Concentration des gros acheteurs](/Project/slides/charts/high_value_concentration.png)

5. Structure produit
* les produits de la gamme Premium/High représentent environ 75% du chiffre d'affaires. 
* la catégorie-prix Premium constitue seule le facteur majeur de concentration du revenu (skew): environ 38% du CA annuel.
![Distribution annuelle du CA par Prix-Catégories](/Project/slides/charts/price_buckets_yearly_distribution.png)

6. Rétention
* churn élevé des clients Occasional, en particulier de la cohorte 2023, observé.
![Impact des Occasional churned sur le chiffre d'affaire par cohorte](/Project/slides/charts/occasional_churned.png)

**Insights business**

* Mettre en place des stratégies d'acquisition de nouveaux clients et des actions ciblées de fidélisation, afin de convertir ces acheteurs en clients réguliers.
* Réactiver les clients existants, notamment du segment Occasional, et renforcer leur fidélisation (remises ciblées, programme de fidélité).
* Réduire la dépendance aux produits Premium et High en favorisant une diversification du panier (remises, promotions, soldes).

**Conclusion**

La croissance du chiffre d'affaires observé après 2023 est portée principalement par la vague initiale de nouveaux clients, mais la forte concentration sur un petit groupe de gros acheteurs, une forte dépendance à de produits haute gamme et le churn élevé des clients Occasional représentent des leviers critiques pour stabiliser le chiffre d'affaires et un risque à la croissance future.

**Compétences mobilisées**

1. Qualité et structuration des données : nettoyage, contrôle des valeurs manquantes, doublons, types de variables et modélisation (fact/dimensions).

2. Feature engineering et calcul de KPI : création de variables dérivées et indicateurs analytiques pour clients, produits et temporalité.

3. Analyse client et segmentation : RFM, cohortes, acquisition, rétention, distribution et concentration du chiffre d’affaires.

4. Visualisation et storytelling : graphiques synthétiques pour interprétation métier et communication des insights.

5. Insight business : interprétation des résultats, traduction des analyses en recommandations concrètes, mesurer l’impact des segments clients et des gammes de produits sur le chiffre d’affaires.