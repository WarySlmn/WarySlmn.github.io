# Data portfolio

# Portfolio de données : Excel à Power BI

![excel-to-powerbi-animated-diagram](assets/images/kaggle_to_powerbi.gif)

# Table des matières

- [Objectif](#objectif)
- [Source de données](#source-de-données)
- [Étapes](#étapes)
- [Conception](#conception)
  - [Maquette](#maquette)
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

# Vérification du nombre de lignes
```sql
/*
# Compter le nombre total d'enregistrements (ou de lignes) dans la vue SQL
*/

SELECT
    COUNT(*) AS no_of_rows
FROM
    view_uk_youtubers_2024;
```

# Vérification du nombre de colonnes
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
