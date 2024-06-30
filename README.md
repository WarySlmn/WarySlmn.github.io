# Data portfolio

# Portfolio de données : Excel à Power BI

![excel-to-powerbi-animated-diagram](assets/images/kaggle_to_powerbi.gif)

# Table des matières

- [Objectif](#objectif)
- [Source de données](#source-de-données)
- [Étapes](#étapes)
- [Conception](#conception)
  - [Outils](#outils)
- [Développement](#développement)
  - [Pseudocode](#pseudocode)
  - [Exploration des données](#exploration-des-données)
  - [Nettoyage des données](#nettoyage-des-données)
  - [Transformation des données](#transformation-des-données)
  - [Création de la vue SQL](#création-de-la-vue-sql)
- [Tests](#tests)
  - [Tests de qualité des données](#tests-de-qualité-des-données)
- [Visualisation](#visualisation)
  - [Résultats](#résultats)
  - [Mesures DAX](#mesures-dax)
- [Analyse](#analyse)
  - [Résultats](#résultats-de-lanalyse)
  - [Validation](#validation)
  - [Découverte](#découverte)
- [Recommandations](#recommandations)
  - [ROI potentiel](#roi-potentiel)
  - [Cours d'actions potentiels](#cours-dactions-potentiels)
- [Conclusion](#conclusion)

# Objectif

Le chef du marketing souhaite identifier les meilleurs YouTubers en 2024 au Royaume-Uni afin de décider avec quels YouTubers il serait préférable de mener des campagnes marketing tout au long de l'année.

- Quelle est la solution idéale ?

Créer un tableau de bord fournissant des informations sur les meilleurs YouTubers au Royaume-Uni en 2024, incluant :
- Le nombre d'abonnés
- Le nombre total de vues
- Le nombre total de vidéos
- Les métriques d'engagement

Cela aidera l'équipe marketing à prendre des décisions éclairées sur les YouTubers avec lesquels collaborer pour leurs campagnes marketing.

## Histoire utilisateur

En tant que chef du marketing, je veux utiliser un tableau de bord qui analyse les données des chaînes YouTube au Royaume-Uni. Ce tableau de bord devrait me permettre d'identifier les chaînes les plus performantes en fonction de métriques telles que la base d'abonnés et les vues moyennes. Avec ces informations, je peux prendre des décisions plus informées sur les YouTubers avec lesquels collaborer, et ainsi maximiser l'efficacité de chaque campagne marketing.


# Source de données

- Quelles données sont nécessaires pour atteindre notre objectif ?

Nous avons besoin des données sur les meilleurs YouTubers au Royaume-Uni en 2024, incluant :
- Les noms des chaînes
- Le nombre total d'abonnés
- Le nombre total de vues
- Le nombre total de vidéos publiées

- D'où proviennent les données ?

Les données sont extraites de Kaggle (un extrait Excel), [voir ici pour les télécharger.](https://www.kaggle.com/datasets/bhavyadhingra00020/top-100-social-media-influencers-2024-countrywise?resource=download)


# Étapes
- Développement
- Tests
- Analyse


# Conception

## Composants du tableau de bord requis

- Que devrait contenir le tableau de bord en fonction des exigences fournies ?

Pour comprendre ce qu'il devrait contenir, nous devons déterminer quelles questions le tableau de bord doit répondre :

1. Qui sont les 10 meilleurs YouTubers avec le plus d'abonnés ?
2. Quelles sont les 3 chaînes ayant téléchargé le plus de vidéos ?
3. Quelles sont les 3 chaînes ayant le plus de vues ?
4. Quelles sont les 3 chaînes ayant la plus haute moyenne de vues par vidéo ?
5. Quelles sont les 3 chaînes ayant le ratio de vues par abonné le plus élevé ?
6. Quelles sont les 3 chaînes ayant le taux d'engagement d'abonnés le plus élevé par vidéo téléchargée ?

Pour l'instant, ce sont quelques-unes des questions auxquelles nous devons répondre, cela peut changer à mesure que nous progressons dans notre analyse.



## Outils

| Outil        | But                              |
|--------------|----------------------------------|
| Excel        | Exploration des données           |
| SQL Server   | Nettoyage, tests et analyse des données |
| Power BI     | Visualisation des données via des tableaux de bord interactifs |
| GitHub       | Hébergement de la documentation du projet et gestion de version |


# Développement

## Pseudocode

- Quelle est l'approche générale pour créer cette solution du début à la fin ?

1. Obtenir les données
2. Explorer les données dans Excel
3. Charger les données dans SQL Server
4. Nettoyer les données avec SQL
5. Tester les données avec SQL
6. Visualiser les données dans Power BI
7. Générer les résultats basés sur les insights
8. Rédiger la documentation + commentaire
9. Publier les données sur GitHub Pages


## Notes d'exploration des données

C'est à cette étape que vous avez une vue d'ensemble des données, des erreurs, des incohérences, des bogues, des caractères étranges et corrompus, etc.


- Quelles sont vos observations initiales avec ce jeu de données ? Qu'est-ce qui a attiré votre attention jusqu'à présent ?

1. Il y a au moins 4 colonnes qui contiennent les données dont nous avons besoin pour cette analyse, ce qui indique que nous avons tout ce dont nous avons besoin dans le fichier sans avoir besoin de contacter le client pour plus de données.
2. La première colonne contient l'identifiant de la chaîne avec ce qui semble être des identifiants de chaîne, qui sont séparés par un symbole @ - nous devons extraire les noms des chaînes à partir de cela.
3. Certaines cellules et noms d'en-tête sont dans une langue différente - nous devons confirmer si ces colonnes sont nécessaires, et le cas échéant, nous devons les aborder.
4. Nous avons plus de données que nécessaire, donc certaines de ces colonnes doivent être supprimées.


## Nettoyage des données

- À quoi devrait ressembler les données propres ? (Qu'est-ce qu'elles devraient contenir ? Quelles contraintes devons-nous leur appliquer ?)

L'objectif est de raffiner notre jeu de données pour nous assurer qu'il est structuré et prêt pour l'analyse.

Les données nettoyées doivent respecter les critères et contraintes suivants :

- Seules les colonnes pertinentes doivent être conservées.
- Tous les types de données doivent être adaptés au contenu de chaque colonne.
- Aucune colonne ne doit contenir de valeurs nulles, indiquant des données complètes pour tous les enregistrements.

Voici un tableau décrivant les contraintes sur notre jeu de données nettoyé :

| Propriété      | Description                            |
|----------------|----------------------------------------|
| Nombre de lignes | 100                                    |
| Nombre de colonnes | 4                                    |

Et voici une représentation tabulaire du schéma attendu pour les données propres :

| Nom de la colonne | Type de données | Nullable |
|-------------------|-----------------|----------|
| channel_name      | VARCHAR         | NON      |
| total_subscribers | INTEGER         | NON      |
| total_views       | INTEGER         | NON      |
| total_videos      | INTEGER         | NON      |


- Quelles étapes sont nécessaires pour nettoyer et mettre en forme les données dans le format désiré ?

1. Supprimer les colonnes inutiles en ne sélectionnant que celles dont vous avez besoin.
2. Extraire les noms de chaîne YouTube de la première colonne.
3. Renommer les colonnes en utilisant des alias.


### Transformation des données


```sql
/*
# 1. Sélectionnez les colonnes requises
# 2. Extrayez

 les noms de chaîne YouTube de la première colonne.
# 3. Renommez les colonnes en utilisant des alias.
*/

SELECT
  PARSENAME(REPLACE(SPLIT_PART(channel, '@', 1), ',', ' ')) AS channel_name,
  total_subscribers,
  total_views,
  total_videos
FROM
  youtube_channels
```

### Création de la vue SQL

```sql
# 1. Créer une vue pour stocker les données transformées
# 2. Convertir le nom de la chaîne extrait en VARCHAR(100)
# 3. Sélectionner les colonnes requises de la table SQL top_uk_youtubers_2024
*/

-- 1.
CREATE VIEW view_uk_youtubers_2024 AS

-- 2.
SELECT
    CAST(SUBSTRING(NOMBRE, 1, CHARINDEX('@', NOMBRE) -1) AS VARCHAR(100)) AS channel_name, -- 2. 
    total_subscribers,
    total_views,
    total_videos

-- 3.
FROM
    top_uk_youtubers_2024
```

## Test
. Quels contrôles de qualité des données et de validation allez-vous créer ?
Voici les tests de qualité des données effectués :

### Vérification du nombre de lignes
```sql
/*
# Compter le nombre total d'enregistrements (ou de lignes) dans la vue SQL
*/

SELECT
    COUNT(*) AS no_of_rows
FROM
    view_uk_youtubers_2024;
```

### Vérification du nombre de colonnes
```sql
/*
# Compter le nombre total de colonnes (ou de champs) dans la vue SQL
*/

SELECT
    COUNT(*) AS column_count
FROM
    INFORMATION_SCHEMA.COLUMNS
WHERE
    TABLE_NAME = 'view_uk_youtubers_2024';
```
### Vérification des types de données
```sql
/*
#Vérifier les types de données de chaque colonne de la vue en consultant la vue INFORMATION_SCHEMA
*/

SELECT
    COLUMN_NAME,
    DATA_TYPE
FROM
    INFORMATION_SCHEMA.COLUMNS
WHERE
    TABLE_NAME = 'view_uk_youtubers_2024';
```
### Vérification des doublons
```sql
/*
# 1. Vérifier les lignes en double dans la vue
# 2. Grouper par le nom de la chaîne
# 3. Filtrer pour les groupes ayant plus d'une ligne
*/

SELECT
    channel_name,
    COUNT(*) AS duplicate_count
FROM
    view_uk_youtubers_2024
    
  
GROUP BY
    channel_name
HAVING
    COUNT(*) > 1;

      ```
# Visualisation

À quoi ressemble le tableau de bord ?
![GIF of Power BI Dashboard](assets/images/top_uk_youtubers_2024.gif)

Cela montre les meilleurs YouTubers au Royaume-Uni en 2024 jusqu'à présent.

# Mesures DAX
1. Total des abonnés (M)
Total des abonnés (M) = 
VAR million = 1000000
VAR sumOfSubscribers = SUM(view_uk_youtubers_2024[total_subscribers])
VAR totalSubscribers = DIVIDE(sumOfSubscribers, million)

RETURN totalSubscribers

 2. Total des vues (B)


Total des vues (B) = 
VAR billion = 1000000000
VAR sumOfTotalViews = SUM(view_uk_youtubers_2024[total_views])
VAR totalViews = ROUND(sumOfTotalViews / billion, 2)

RETURN totalViews

3. Total des vidéos
Total des vidéos = 
VAR totalVideos = SUM(view_uk_youtubers_2024[total_videos])

RETURN totalVideos

4. Moyenne des vues par vidéo (M)
Moyenne des vues par vidéo (M) = 
VAR sumOfTotalViews = SUM(view_uk_youtubers_2024[total_views])
VAR sumOfTotalVideos = SUM(view_uk_youtubers_2024[total_videos])
VAR avgViewsPerVideo = DIVIDE(sumOfTotalViews, sumOfTotalVideos, BLANK())
VAR finalAvgViewsPerVideo = DIVIDE(avgViewsPerVideo, 1000000, BLANK())

RETURN finalAvgViewsPerVideo
 
5. Taux d'engagement des abonnés
Taux d'engagement des abonnés = 
VAR sumOfTotalSubscribers = SUM(view_uk_youtubers_2024[total_subscribers])
VAR sumOfTotalVideos = SUM(view_uk_youtubers_2024[total_videos])
VAR subscriberEngRate = DIVIDE(sumOfTotalSubscribers, sumOfTotalVideos, BLANK())

RETURN subscriberEngRate

Ces mesures DAX fournissent des calculs agrégés basés sur les données des YouTubers au Royaume-Uni en 2024, permettant une analyse approfondie de leurs performances.

## Analyse

### Résultats

- Qu'avons-nous trouvé ?

Pour cette analyse, nous allons nous concentrer sur les questions ci-dessous pour obtenir les informations nécessaires pour notre client en marketing :

Voici les principales questions auxquelles nous devons répondre pour notre client en marketing :

1. **Qui sont les 10 principaux YouTubers ayant le plus d'abonnés ?**

| Classement | Nom de la chaîne      | Abonnés (M) |
|------------|-----------------------|-------------|
| 1          | NoCopyrightSounds     | 33.70       |
| 2          | DanTDM                | 28.80       |
| 3          | Dan Rhodes            | 26.50       |
| 4          | Miss Katy             | 24.50       |
| 5          | Mister Max            | 24.40       |
| 6          | KSI                   | 24.10       |
| 7          | Jelly                 | 23.50       |
| 8          | Dua Lipa              | 23.30       |
| 9          | Sidemen               | 21.00       |
| 10         | Ali-A                 | 18.90       |


2. **Quelles sont les 3 chaînes ayant téléchargé le plus de vidéos ?**

| Classement | Nom de la chaîne      | Vidéos téléchargées |
|------------|-----------------------|---------------------|
| 1          |  24 News HD           | 169862              |
| 2          | Sky News              | 48896               |
| 3          | BBC News              | 41003               |

  
3. **Quelles sont les 3 chaînes ayant le plus de vues ?**

| Classement | Nom de la chaîne      | Total des vues (B) |
|------------|-----------------------|--------------------|
| 1          | DanTDM                | 19.85              |
| 2          | Dan Rhodes            | 18.83              |
| 3          | Mister Max            | 16.09              |


4. **Quelles sont les 3 chaînes ayant le plus grand nombre de vues par vidéo en moyenne ?**

| Nom de la chaîne | Moyenne des vues par vidéo (M) |
|------------------|-------------------------------|
| Mark Ronson      | 329.37                        |
| Jessie J         | 60.37                         |
| Dua Lipa         | 48.29                         |


5. **Quelles sont les 3 chaînes ayant le ratio le plus élevé de vues par abonné ?**

| Classement | Nom de la chaîne       | Vues par abonné             |
|------------|------------------------|-----------------------------|
| 1          | GRM Daily              | 1194                    |
| 2          | Nickelodeon            | 1061                    |
| 3          | Disney Junior UK       | 1,031.97                    |


6. **Quelles sont les 3 chaînes ayant le taux d'engagement des abonnés le plus élevé par vidéo téléchargée ?**

| Classement | Nom de la chaîne      | Taux d'engagement des abonnés  |
|------------|-----------------------|--------------------------------|
| 1          | Mark Ronson           | 344500                         |
| 2          | Jessie J              | 110416                         |
| 3          | Dua Lipa              | 86446                         | 


Cette analyse fournit des informations clés sur les performances des chaînes YouTube en 2024, ce qui est crucial pour la stratégie marketing de notre client.

## Validation

### 1. YouTubers avec le plus grand nombre d’abonnés

#### Décomposition des calculs

Idée de campagne = placement de produit

1. **NoCopyrightSounds**
   - Nombre moyen de vues par vidéo = 6,61 millions
   - Coût du produit = 5 $
   - Nombre potentiel d’unités vendues par vidéo = 6,61 millions x taux de conversion de 2 % = 138 400 unités vendues
   - Revenu potentiel par vidéo = 661000 x 5 $ = 3305 000 $
   - Coût de la campagne (frais uniques) = 50 000 $
   - **Bénéfice net = 692 000 $ - 50 000 $ = 63255 000 $**

2. **DanTDM**
   - Nombre moyen de vues par vidéo = 5,35 millions
   - Coût du produit = 5 $
   - Nombre potentiel d’unités vendues par vidéo = 5,35 millions x taux de conversion de 2 % = 107 000 unités vendues
  - Revenu potentiel par vidéo = 107 000 x 5 $ = 5350 000 $
   - Coût de la campagne (frais uniques) = 50 000 $
   - **Bénéfice net = 5350 000 $ - 50 000 $ = 5300 000 $**

3. **Dan Rhodes**
   - Nombre moyen de vues par vidéo = 11,31 millions
   - Coût du produit = 5 $
   - Nombre potentiel d’unités vendues par vidéo = 11,15 millions x taux de conversion de 2 % = 2262 000 unités vendues
   - Revenu potentiel par vidéo = 2262 000 x 5 $ = 11310 000 $
   - Coût de la campagne (frais uniques) = 50 000 $
   - **Bénéfice net = 1 115 000 $ - 50 000 $ = 1081000 $**

#### Output

![Most subsc](assets/images/youtube_abonée.png)


**Meilleure option de cette catégorie : Dan Rhodes**

#### SQL query
```sql
-- 1. Définir les variables 
-- 2. Créer une CTE qui arrondit la moyenne des vues par vidéo 
-- 3. Sélectionner la colonne dont vous avez besoin et créer des colonnes calculées à partir des colonnes existantes 
-- 4. Filtrer les résultats par chaînes Youtube
-- 5. Trier les résultats par bénéfices nets (du plus élevé au plus bas)

-- 1. 
DECLARE @tauxConversion FLOAT = 0.02;		-- Le taux de conversion @ 2%
DECLARE @coutProduit FLOAT = 5.0;			-- Le coût du produit @ $5
DECLARE @coutCampagne FLOAT = 50000.0;		-- Le coût de la campagne @ $50,000	

-- 2.  
WITH ChanelData AS (
    SELECT 
        Chanel_name,
        total_views,
        total_videos,
        ROUND((CAST(total_views AS FLOAT) / total_videos), -4) AS vues_moyennes_arrondies_par_video
    FROM 
        youtube_db.dbo.view_uk_youtubers_uk2024
)

-- 3. 
SELECT 
    Chanel_name,
	 vues_moyennes_arrondies_par_video,
    (vues_moyennes_arrondies_par_video * @tauxConversion) AS unites_potentielles_vendues_par_video,
    (vues_moyennes_arrondies_par_video * @tauxConversion * @coutProduit) AS revenu_potentiel_par_video,
    ((vues_moyennes_arrondies_par_video * @tauxConversion * @coutProduit) - @coutCampagne) AS benefice_net
FROM 
    ChanelData

-- 4. 
WHERE 
Chanel_name in ('NoCopyrightSounds', 'DanTDM', 'Dan Rhodes')    

-- 5.  
ORDER BY
    benefice_net DESC
```


### 2. YouTubers ayant publié le plus de vidéos

#### Décomposition des calculs

Pour cette catégorie, nous évaluerons les avantages d'une campagne basée sur le nombre de vidéos publiées, en considérant que chaque vidéo augmente la probabilité de visibilité pour les produits et services proposés. 

1. **24 News HD**
   - Nombre de vidéos publiées = 169862
   - Nombre moyen de vues par vidéo = 0,2  million
   - Coût du produit = 5 $
   - Nombre potentiel d'unités vendues par vidéo = 0,2 million x taux de conversion de 2 % = 4 000 unités vendu
   - Revenu potentiel par vidéo = 4 000 x 5 $ = 20 000 $
   - Revenu potentiel total pour toutes les vidéos = 55 000 $ x 169862 = 8 493 100 000 $
   - Coût total de la campagne (frais uniques) = 55 000 $
   - **Bénéfice net = 20 000 - 55 000 $ = - 53 000 (potentiel perte) $**

2. **Sky News**
   - Nombre de vidéos publiées = 4 8896
   - Nombre moyen de vues par vidéo = 0,09 million
   - Coût du produit = 5 $
   - Nombre potentiel d'unités vendues par vidéo = 0,09 million x taux de conversion de 2 % = 18000 unités vendues
   - Revenu potentiel par vidéo = 18 000 x 5 $ = 90 000 $
   - Revenu potentiel total pour toutes les vidéos = 90 000 $ x 48896 = 244 480 $
   - Coût total de la campagne (frais uniques) = 55 000 $
   - **Bénéfice net =  244 480 $ -55 000 $ = - 46000(potentiel perte)**

3. **BBC News عربي**
   - Nombre de vidéos publiées = 41003
   - Nombre moyen de vues par vidéo = 0,12 million
   - Coût du produit = 5 $
   - Nombre potentiel d'unités vendues par vidéo = 0,12 million x taux de conversion de 2 % = 24 000 unités vendues
   - Revenu potentiel par vidéo = 24 000 x 5 $ = 120 000 $
   - Revenu potentiel total pour toutes les vidéos = 120 000 $ x 41003 = 205015 $
   - Coût total de la campagne (frais uniques) = 55 000 $
   - **Bénéfice net = 120 000 $  - 55 000 $ = -43000( potentiel perte)**

**Meilleure option de cette catégorie : aucun**

#### SQL query 
```sql
/* 
# 1. Define variables
# 2. Create a CTE that rounds the average views per video
# 3. Select the columns you need and create calculated columns from existing ones
# 4. Filter results by YouTube channels
# 5. Sort results by net profits (from highest to lowest)
*/


-- 1.
DECLARE @conversionRate FLOAT = 0.02;           -- The conversion rate @ 2%
DECLARE @productCost FLOAT = 5.0;               -- The product cost @ $5
DECLARE @campaignCostPerVideo FLOAT = 5000.0;   -- The campaign cost per video @ $5,000
DECLARE @numberOfVideos INT = 11;               -- The number of videos (11)


-- 2.
WITH ChannelData AS (
    SELECT
        channel_name,
        total_views,
        total_videos,
        ROUND((CAST(total_views AS FLOAT) / total_videos), -4) AS rounded_avg_views_per_video
    FROM
        youtube_db.dbo.view_uk_youtubers_2024
)


-- 3.
SELECT
    channel_name,
    rounded_avg_views_per_video,
    (rounded_avg_views_per_video * @conversionRate) AS potential_units_sold_per_video,
    (rounded_avg_views_per_video * @conversionRate * @productCost) AS potential_revenue_per_video,
    ((rounded_avg_views_per_video * @conversionRate * @productCost) - (@campaignCostPerVideo * @numberOfVideos)) AS net_profit
FROM
    ChannelData


-- 4.
WHERE
    Chanel_name in ('24 News HD', 'Sky News', 'BBC News عربي')  


-- 5.
ORDER BY
    net_profit DESC;
```
#### Output

![Most videos](assets/images/youtubers_with_the_most_videos.png)

### 3. Youtubers avec le plus de vues

#### Décomposition des calculs

**Idée de campagne** : marketing d'influence

a. **DanTDM**

- **Vues moyennes par vidéo** : 5,35 millions
- **Coût du produit** : 5 $
- **Unités potentielles vendues par vidéo** : 5,35 millions x taux de conversion de 2 % = 1070 000 unités vendues
- **Revenu potentiel par vidéo** : 1070 000 x 5 $ = 5350 000 $
- **Coût de la campagne (contrat de 3 mois)** : 130 000 $
- **Bénéfice net** : 5350 000 $ - 130 000 $ = **405 000 $**

b. **Dan Rhodes**

- **Vues moyennes par vidéo** : 11,31 millions
- **Coût du produit** : 5 $
- **Unités potentielles vendues par vidéo** : 11,31 millions x taux de conversion de 2 % = 2262 000 unités vendues
- **Revenu potentiel par vidéo** : 2262 000 x 5 $ = 11310 000 $
- **Coût de la campagne (contrat de 3 mois)** : 130 000 $
- **Bénéfice net** : 11310 000 $ - 130 000 $ = **1001 000 $**

c. **Mister Max**

- **Vues moyennes par vidéo** : 14,03 millions
- **Coût du produit** : 5 $
- **Unités potentielles vendues par vidéo** : 14,03 millions x taux de conversion de 2 % = 280 600 unités vendues
- **Revenu potentiel par vidéo** :  280 600x 5 $ = 1 403 000 $
- **Coût de la campagne (contrat de 3 mois)** : 130 000 $
- **Bénéfice net** : 1 403 000 $ - 130 000 $ = **1 273 000 $**

**Meilleure option de la catégorie** : Mister Max


#### SQL query 
```sql
/*
# 1. Define variables
# 2. Create a CTE that rounds the average views per video
# 3. Select the columns you need and create calculated columns from existing ones
# 4. Filter results by YouTube channels
# 5. Sort results by net profits (from highest to lowest)
*/



-- 1.
DECLARE @conversionRate FLOAT = 0.02;        -- The conversion rate @ 2%
DECLARE @productCost MONEY = 5.0;            -- The product cost @ $5
DECLARE @campaignCost MONEY = 130000.0;      -- The campaign cost @ $130,000



-- 2.
WITH ChannelData AS (
    SELECT
        channel_name,
        total_views,
        total_videos,
        ROUND(CAST(total_views AS FLOAT) / total_videos, -4) AS avg_views_per_video
    FROM
        youtube_db.dbo.view_uk_youtubers_2024
)


-- 3.
SELECT
    channel_name,
    avg_views_per_video,
    (avg_views_per_video * @conversionRate) AS potential_units_sold_per_video,
    (avg_views_per_video * @conversionRate * @productCost) AS potential_revenue_per_video,
    (avg_views_per_video * @conversionRate * @productCost) - @campaignCost AS net_profit
FROM
    ChannelData


-- 4.
WHERE
    channel_name IN ('Mister Max', 'DanTDM', 'Dan Rhodes')


-- 5.
ORDER BY
    net_profit DESC;

```

#### Output

![Most views](assets/images/youtubers_with_the_most_views.png)

## Decouverte
- Qu'avons-nous appris ?

Nous avons découvert que :

1. **NoCopyrightSounds**, **Dan Rhodes** et **DanTDM** sont les chaînes ayant le plus d'abonnés au Royaume-Uni.
2. **24 News HD**, **Sky News** et **BBC News عربي** sont les chaînes ayant publié le plus de vidéos.
3. **DanTDM**, **Dan Rhodes** et **Mister Max** sont les chaînes ayant le plus de vues.
4. Les chaînes de divertissement sont utiles pour atteindre un public plus large, car les chaînes qui publient régulièrement sur leurs plateformes et génèrent le plus d'engagement sont axées sur le divertissement et la musique.

## Recommandations

- Que recommandez-vous en fonction des informations recueillies ?

1. **Dan Rhodes** est la meilleure chaîne YouTube avec laquelle collaborer pour maximiser la visibilité, car elle possède le plus grand nombre d'abonnés YouTube au Royaume-Uni.
2. Bien que  **24 News HD**, **Sky News** et **BBC News عربي**  publient régulièrement sur YouTube, il ne pourrait pas être judicieux de faire une collaboration avec elles. compte tenu des limites budgétaires actuelles, car le retour sur investissement potentiel est nettement inférieur à celui des autres chaînes.
3. **Mister Max** est le meilleur YouTuber avec lequel collaborer si nous souhaitons maximiser la portée, mais collaborer avec **DanTDM** et **Dan Rhodes** peut être une meilleure option à long terme, étant donné qu'ils ont tous deux une grande base d'abonnés et obtiennent un nombre de vues très élevé en moyenne.
4. Les trois meilleures chaînes pour établir des collaborations sont **NoCopyrightSounds**, **DanTDM** et **Dan Rhodes**, car elles attirent constamment le plus d'engagement sur leurs chaînes.

   ### ROI Potentiel
- Quel retour sur investissement (ROI) pouvons-nous attendre si nous prenons cette direction ?

1. La mise en place d'un accord de collaboration avec **Dan Rhodes** permettrait au client de réaliser un bénéfice net de **1081000 $** par vidéo.
2. Un contrat de marketing d'influence avec **Mister Max** pourrait générer un bénéfice net de **1 273 000 $** pour le client.
3. Si nous optons pour une campagne de placement de produit avec **DanTDM**, cela pourrait générer pour le client environ **485 000 $** par vidéo. Si nous choisissons plutôt une campagne de marketing d'influence, cela permettrait au client de réaliser un bénéfice net unique de **405 000 $**.
4. **NoCopyrightSounds** pourrait également permettre au client de réaliser un bénéfice de **611 000 $** par vidéo, ce qui mérite d'être pris en considération.

5. ### Plan d'action
- Quelles actions devrions-nous entreprendre et pourquoi ?

Selon notre analyse, nous croyons que le meilleur canal pour conclure un partenariat à long terme afin de promouvoir les produits du client est la chaîne Dan Rhodes.

Nous aurons des discussions avec le client en marketing pour prévoir ce qu'il attend également de cette collaboration. Une fois que nous constaterons que nous atteignons les étapes prévues, nous avancerons avec des partenariats potentiels avec les chaînes DanTDM, Mister Max et NoCopyrightSounds à l'avenir.

- Quelles étapes suivre pour mettre en œuvre efficacement les décisions recommandées ?

1. Contacter les équipes derrière chacune de ces chaînes, en commençant par Dan Rhodes.
2. Négocier les contrats dans les budgets alloués à chaque campagne marketing.
3. Lancer les campagnes et suivre leurs performances par rapport aux KPI.
4. Examiner le déroulement des campagnes, recueillir des informations et optimiser en fonction des commentaires des clients convertis et des audiences de chaque chaîne.
