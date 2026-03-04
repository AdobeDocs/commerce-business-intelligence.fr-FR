---
title: Reporting sur un calendrier de vente au détail
description: Découvrez comment configurer la structure pour utiliser un calendrier de vente au détail 4 [!DNL Commerce Intelligence] 5-4 dans votre compte.
exl-id: 3754151c-4b0f-4238-87f2-134b8409e32b
role: Admin, Developer, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: 5e80ff8f8ec76996b88a22b115be696b110581be
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 0%

---

# Reporting sur un calendrier de vente au détail

Cette rubrique explique comment configurer la structure pour utiliser un calendrier de vente au détail [4-5-4](https://nrf.com/resources/4-5-4-calendar) dans votre compte [!DNL Adobe Commerce Intelligence]. Le Report Builder visuel offre des périodes, des intervalles et des paramètres indépendants incroyablement flexibles. Cependant, tous ces paramètres fonctionnent avec le calendrier mensuel traditionnel en place.

Comme de nombreux clients modifient leur calendrier pour utiliser des dates de vente au détail ou de comptabilité, les étapes ci-dessous illustrent comment utiliser vos données et créer des rapports à l’aide de dates de vente au détail. Bien que les instructions ci-dessous fassent référence au calendrier de vente au détail 4-5-4, vous pouvez les modifier pour tout calendrier spécifique utilisé par votre équipe, qu’il s’agisse d’un calendrier financier ou d’une simple période personnalisée.

Avant de commencer, vous devez consulter [le téléchargeur de fichiers](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) et vous assurer que vous avez bien allongé le fichier `.csv`. Cela permet de s’assurer que les dates couvrent toutes vos données historiques et repoussent les dates dans le futur.

Cette analyse contient [colonnes calculées avancées](../data-warehouse-mgr/adv-calc-columns.md).

## Prise en main

Vous pouvez [télécharger](../../assets/454-calendar.csv) une version `.csv` du calendrier de vente au détail 4-5-4 pour les années 2014 à 2017. Vous devrez peut-être ajuster ce fichier en fonction de votre calendrier de vente au détail interne et étendre la période pour prendre en charge votre période actuelle et historique. Une fois le fichier téléchargé, utilisez le téléchargeur de fichiers pour créer un tableau de calendrier de vente au détail dans votre Data Warehouse [!DNL Commerce Intelligence]. Si vous utilisez une version non modifiée du calendrier de vente au détail 4-5-4, assurez-vous que la structure et les types de données des champs de ce tableau correspondent aux éléments suivants :

| Nom de la colonne | Type de données de colonne | Clé de Principal |
| --- | --- | --- |
| `Date Retail` | `Date & Time` | `Yes` |
| `Year Retail` | `Whole Number` | `No` |
| `Quarter Retail` | `Whole Number` | `No` |
| `Month Number Retail` | `Whole Number` | `No` |
| `Week Retail` | `Whole Number` | `No` |
| `Month Name Retail` | `Text` (jusqu&#39;à 255 caractères) | `No` |
| `Week Number of Month Retail` | `Whole Number` | `No` |

{style="table-layout:auto"}

## Colonnes à créer

* table **sales\_order**
   * `INPUT` `created\_at` (aaaa-mm-jj 00:00:00)
      * [!UICONTROL Column type] : - `Same table > Calculation`
      * [!UICONTROL Inputs] : - `created\_at`
      * [!UICONTROL Datatype] : - `Datetime`
      * [!UICONTROL Calculation] : - ` case when A is null then null else to\_char(A, 'YYYY-MM-DD 00:00:00') end`

* **Calendrier de vente au détail** table de chargement de fichier
   * **Date actuelle**
      * [!UICONTROL Column type] : `Same table > Calculation`
      * [!UICONTROL Inputs] : `Date Retail`
      * 
        [!UICONTROL, type de données]: `Datetime`
      * [!UICONTROL Calculation] : `case when A is null then null else to\_char(now(), 'YYYY-MM-DD 00:00:00') end`

        >[!NOTE]
        >
        >La fonction `now()` ci-dessus est spécifique à PostgreSQL. Bien que la plupart des entrepôts de données [!DNL Commerce Intelligence] soient hébergés sur PostgreSQL, certains peuvent être hébergés sur Redshift. Si le calcul ci-dessus renvoie une erreur, vous devrez peut-être utiliser la fonction Redshift `getdate()` au lieu de `now()`.

   * **Année de vente au détail actuelle** (doit être créé par l’analyste de support)
      * [!UICONTROL Column type] : E`vent Counter`
      * [!UICONTROL Local Key] : `Current date`
      * [!UICONTROL Remote Key] : `Retail calendar.Date Retail`
      * 
        [!UICONTROL Operation]: `Max`
      * [!UICONTROL Operation value] : `Year Retail`
   * **Inclus dans l&#39;année de vente au détail en cours ? (Oui/Non)**
      * [!UICONTROL Column type] : `Same table > Calculation`
      * [!UICONTROL Inputs] :
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
        [!UICONTROL, type de données]: `String`
      * [!UICONTROL Calculation] : `case when A is null or B is null then null when A = B then 'Yes' else 'No' end`
   * **Inclus dans l&#39;année de vente précédente ? (Oui/Non)**
      * [!UICONTROL Column type] : `Same table > Calculation`
      * [!UICONTROL Inputs] :
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
        [!UICONTROL, type de données]: String
      * [!UICONTROL Calculation] : `case when A is null or B is null then null when (A = (B-1)) then 'Yes' else 'No' end`

* table **sales\_order**
   * **Créé\_à (année de vente au détail)**
      * [!UICONTROL Column type] : `One to Many > JOINED\_COLUMN`
      * Chemin -
         * [!UICONTROL Many] : `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One] : `Retail Calendar.Date Retail`
      * Sélectionner un [!UICONTROL table] : `Retail Calendar`
      * Sélectionner un [!UICONTROL column] : `Year Retail`
   * **Créé\_à (semaine de vente au détail)**
      * [!UICONTROL Column type] : `One to Many > JOINED\_COLUMN`
      * Chemin -
         * [!UICONTROL Many] : commande_vente.\[ENTRÉE\] créé\_à (aaaa-mm-jj 00:00:00
         * [!UICONTROL One] : Calendrier de vente au détail.Date de vente au détail
      * Sélectionner un [!UICONTROL table] : `Retail Calendar`
      * Sélectionner un [!UICONTROL column] : `Week Retail`
   * **Créé\_à (mois de vente au détail)**
      * [!UICONTROL Column type] : `One to Many > JOINED\_COLUMN`
      * Chemin
         * [!UICONTROL Many] : `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One] : `Retail Calendar.Date Retail`
      * Sélectionner un [!UICONTROL table] : `Retail Calendar`
      * Sélectionner un [!UICONTROL column] : `Month Number Retail`
   * **Inclure dans l&#39;année de vente précédente ? (Oui/Non)**
      * [!UICONTROL Column type] : `One to Many > JOINED\_COLUMN`
      * Chemin -
         * [!UICONTROL Many] : `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One] : `Calendar.Date Retail` de détail
      * Sélectionner un [!UICONTROL table] : `Retail Calendar`
      * Sélectionner un [!UICONTROL column] : `Include in previous retail year? (Yes/No)`
   * **Inclure dans l&#39;année de vente au détail en cours ? (Oui/Non)**
      * [!UICONTROL Column type] : `One to Many > JOINED\_COLUMN`
      * Chemin -
         * [!UICONTROL Many] : `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One] : `Calendar.Date Retail` de détail
      * Sélectionner un [!UICONTROL table] : `Retail Calendar`
      * Sélectionner un [!UICONTROL column] : `Include in current retail year? (Yes/No)`

## Mesures

Remarque : aucune nouvelle mesure n’est nécessaire pour cette analyse. Veillez toutefois à [ajouter les nouvelles colonnes que vous avez créées dans la table sales\_order en tant que dimensions](../data-warehouse-mgr/manage-data-dimensions-metrics.md) pour toutes les mesures de la table sales\_order avant de poursuivre les rapports.

## Rapports

* **Commandes hebdomadaires - calendrier de vente au détail (YoY)**
   * `A` de mesure : `2017`
      * [!UICONTROL Metric] : nombre de commandes
      * [!UICONTROL Filter] :
         * Créé\_à (année de vente au détail) = 2017
   * `B` de mesure : `2016`
      * [!UICONTROL Metric] : nombre de commandes
      * [!UICONTROL Filter] :
         * Créé\_à (année de vente au détail) = 2016
   * `C` de mesure : `2015`
      * [!UICONTROL Metric] : `Number of orders`
      * [!UICONTROL Filter] :
         * `Created\_at (retail Year) = 2015`
   * [!UICONTROL Time period] : `All time`
   * 
     [!UICONTROL Interval]: `None`
   * 
     [!UICONTROL Group by]: `Created\_at` (retail week)
   * 
     [!UICONTROL Chart type]: `Line`
      * Désactiver `multiple Y-axes`

* **Présentation du calendrier de vente au détail (année de vente au détail en cours, par mois)**
   * `A` de mesure : `Revenue`
      * 
        [!UICONTROL Metric]: `Revenue`
      * [!UICONTROL Filter] :
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * `B` de mesure : `Orders`
      * [!UICONTROL Metric] : `Number of orders`
      * [!UICONTROL Filter] :
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * `C` de mesure : `Avg order value`
      * [!UICONTROL Metric] : `Avg order value`
      * [!UICONTROL Filter] :
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * [!UICONTROL Time period] : `All time`
   * 
     [!UICONTROL Interval]: `None`
   * 
     [!UICONTROL Group by]: `Created\_at` (retail month)
   * 
     [!UICONTROL Chart type]: `Line`

* **Présentation du calendrier de vente au détail (année de vente au détail précédente, par mois)**
   * `A` de mesure : `Revenue`
      * 
        [!UICONTROL Metric]: `Revenue`
      * [!UICONTROL Filter] :
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * `B` de mesure : `Orders`
      * [!UICONTROL Metric] : nombre de commandes
      * [!UICONTROL Filter] :
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * `C` de mesure : `Avg order value`
      * [!UICONTROL Metric] : `Avg order value`
      * [!UICONTROL Filter] :
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * [!UICONTROL Time period] : `All time`
   * 
     [!UICONTROL Interval]: `None`
   * 
     [!UICONTROL Group by]: `Created\_at` (retail month)
   * 
     [!UICONTROL Chart type]: `Line`

## Étapes suivantes

Ce qui précède décrit comment configurer un calendrier de vente au détail pour qu’il soit compatible avec toute mesure créée sur votre table de `sales\_order` (telle que `Revenue` ou `Orders`). Vous pouvez également étendre cette fonctionnalité afin de prendre en charge le calendrier de vente au détail des mesures créées sur n’importe quel tableau. La seule exigence est que cette table dispose d&#39;un champ datetime valide qui peut être utilisé pour se joindre à la table Calendrier de la vente au détail.

Par exemple, pour afficher les mesures au niveau du client sur un calendrier de vente au détail 4-5-4, créez un calcul de `Same Table` dans le tableau de `customer\_entity`, similaire à `\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)` décrit ci-dessus. Vous pouvez ensuite utiliser cette colonne pour reproduire les calculs `One to Many` JOINED\_COLUMN (comme `Created_at (retail year)`) et `Include in previous retail year? (Yes/No)` en joignant la table `customer\_entity` à la table `Retail Calendar`.

N’oubliez pas de [ajouter toutes les nouvelles colonnes en tant que dimensions aux mesures](../data-warehouse-mgr/manage-data-dimensions-metrics.md) avant de créer de nouveaux rapports.
