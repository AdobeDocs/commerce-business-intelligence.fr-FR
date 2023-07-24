---
title: Création de rapports sur un calendrier de vente au détail
description: Découvrez comment configurer la structure pour utiliser un calendrier de vente au détail 4-5-4 dans votre [!DNL Commerce Intelligence] compte .
exl-id: 3754151c-4b0f-4238-87f2-134b8409e32b
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 0%

---

# Création de rapports dans un calendrier de vente au détail

Cette rubrique explique comment configurer la structure pour utiliser une [4-5-4 calendrier de vente au détail](https://nrf.com/resources/4-5-4-calendar) dans votre [!DNL Adobe Commerce Intelligence] compte . Le créateur de rapports visuel fournit des périodes, des intervalles et des paramètres indépendants incroyablement flexibles. Cependant, tous ces paramètres fonctionnent avec le calendrier mensuel traditionnel en place.

De nombreux clients modifiant leur calendrier pour utiliser des dates de vente au détail ou de comptabilité, les étapes ci-dessous illustrent l’utilisation de vos données et la création de rapports à l’aide de dates de vente au détail. Bien que les instructions ci-dessous fassent référence au calendrier de vente au détail 4-5-4, vous pouvez les modifier pour n’importe quel calendrier spécifique utilisé par votre équipe, qu’il s’agisse d’un calendrier financier ou personnalisé.

Avant de commencer, consultez [Téléchargement du fichier](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) et assurez-vous que vous avez allongé l’intervalle `.csv` fichier . Cela permet de s’assurer que les dates couvrent toutes vos données historiques et de transmettre les dates ultérieurement.

Cette analyse contient [colonnes calculées avancées](../data-warehouse-mgr/adv-calc-columns.md).

## Prise en main

Vous pouvez [télécharger](../../assets/454-calendar.csv) a `.csv` version du calendrier de vente au détail 4-5-4 pour les années 2014 à 2017. Vous devrez peut-être ajuster ce fichier en fonction de votre calendrier de vente au détail interne et étendre la période pour prendre en charge votre période historique et actuelle. Après avoir téléchargé le fichier, utilisez le téléchargeur de fichiers pour créer un tableau Calendrier de vente au détail dans votre [!DNL Commerce Intelligence] Data Warehouse. Si vous utilisez une version inchangée du calendrier de vente au détail 4-5-4, assurez-vous que la structure et les types de données des champs de ce tableau correspondent aux éléments suivants :

| Nom de la colonne | Type de données de colonne | Clé Principal |
| --- | --- | --- |
| `Date Retail` | `Date & Time` | `Yes` |
| `Year Retail` | `Whole Number` | `No` |
| `Quarter Retail` | `Whole Number` | `No` |
| `Month Number Retail` | `Whole Number` | `No` |
| `Week Retail` | `Whole Number` | `No` |
| `Month Name Retail` | `Text` (Jusqu’à 255 caractères) | `No` |
| `Week Number of Month Retail` | `Whole Number` | `No` |

{style="table-layout:auto"}

## Colonnes à créer

* **sales\_order** table
   * `INPUT` `created\_at` (aaaa-mm-jj 00:00:00)
      * [!UICONTROL Column type]: – `Same table > Calculation`
      * [!UICONTROL Inputs]: – `created\_at`
      * [!UICONTROL Datatype]: – `Datetime`
      * [!UICONTROL Calculation]: - ` case when A is null then null else to\_char(A, 'YYYY-MM-DD 00:00:00') end`

* **Calendrier de vente au détail** table de chargement des fichiers
   * **Date courante**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]: `Date Retail`
      * 
        [!UICONTROL Type de données]: `Datetime`
      * [!UICONTROL Calculation]: `case when A is null then null else to\_char(now(), 'YYYY-MM-DD 00:00:00') end`

        >[!NOTE]
        >
        >Le `now()` La fonction ci-dessus est spécifique à PostgreSQL. Bien que [!DNL Commerce Intelligence] Les entrepôts de données sont hébergés sur PostgreSQL, certains peuvent l’être sur Redshift. Si le calcul ci-dessus renvoie une erreur, vous devrez peut-être utiliser la fonction Redshift `getdate()` au lieu de `now()`.

   * **Current retail year** (Doit être créé par l’analyste de support)
      * [!UICONTROL Column type]: E`vent Counter`
      * [!UICONTROL Local Key]: `Current date`
      * [!UICONTROL Remote Key]: `Retail calendar.Date Retail`
      * 
        [!UICONTROL Operation]: `Max`
      * [!UICONTROL Operation value]: `Year Retail`
   * **Inclus dans l’année de vente en cours ? (Oui/Non)**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
        [!UICONTROL Type de données]: `String`
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when A = B then 'Yes' else 'No' end`
   * **Inclus dans l’année de vente précédente ? (Oui/Non)**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
        [!UICONTROL Type de données]: String
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when (A = (B-1)) then 'Yes' else 'No' end`

* **sales\_order** table
   * **Created\_at (année de vente au détail)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Path -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * Sélectionnez une [!UICONTROL table]: `Retail Calendar`
      * Sélectionnez une [!UICONTROL column]: `Year Retail`
   * **Created\_at (semaine de vente au détail)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Path -
         * [!UICONTROL Many]: sales\_order.\[INPUT\] created\_at (aaaa-mm-jj 00:00:00
         * [!UICONTROL One]: Calendrier de vente au détail.Date Retail
      * Sélectionnez une [!UICONTROL table]: `Retail Calendar`
      * Sélectionnez une [!UICONTROL column]: `Week Retail`
   * **Created\_at (mois de vente au détail)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Chemin
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * Sélectionnez une [!UICONTROL table]: `Retail Calendar`
      * Sélectionnez une [!UICONTROL column]: `Month Number Retail`
   * **Inclure dans l’année de vente précédente ? (Oui/Non)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Path -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: Vente au détail `Calendar.Date Retail`
      * Sélectionnez une [!UICONTROL table]: `Retail Calendar`
      * Sélectionnez une [!UICONTROL column]: `Include in previous retail year? (Yes/No)`
   * **Inclure dans l’année de vente actuelle ? (Oui/Non)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Path -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: Vente au détail `Calendar.Date Retail`
      * Sélectionnez une [!UICONTROL table]: `Retail Calendar`
      * Sélectionnez une [!UICONTROL column]: `Include in current retail year? (Yes/No)`

## Mesures

Remarque : Aucune nouvelle mesure n’est nécessaire pour cette analyse. Veillez toutefois à [ajoutez les nouvelles colonnes que vous avez créées dans la table sales\_order en tant que dimensions.](../data-warehouse-mgr/manage-data-dimensions-metrics.md) pour toutes les mesures de la table sales\_order avant de poursuivre les rapports.

## Rapports

* **Commandes hebdomadaires - calendrier de vente au détail (YoY)**
   * Mesure `A`: `2017`
      * [!UICONTROL Metric]: Nombre de commandes
      * [!UICONTROL Filter]:
         * Created\_at (année de vente) = 2017
   * Mesure `B`: `2016`
      * [!UICONTROL Metric]: Nombre de commandes
      * [!UICONTROL Filter]:
         * Created\_at (année de vente) = 2016
   * Mesure `C`: `2015`
      * [!UICONTROL Metric]: `Number of orders`
      * [!UICONTROL Filter]:
         * `Created\_at (retail Year) = 2015`
   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Interval]: `None`
   * 
     [!UICONTROL Group by]: `Created\_at` (retail week)
   * 
     [!UICONTROL Chart type]: `Line`
      * Désactiver `multiple Y-axes`

* **Aperçu du calendrier de vente au détail (année de vente au détail actuelle par mois)**
   * Mesure `A`: `Revenue`
      * 
        [!UICONTROL Mesure]: `Revenue`
      * [!UICONTROL Filter]:
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * Mesure `B`: `Orders`
      * [!UICONTROL Metric]: `Number of orders`
      * [!UICONTROL Filter]:
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * Mesure `C`: `Avg order value`
      * [!UICONTROL Metric]: `Avg order value`
      * [!UICONTROL Filter]:
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Interval]: `None`
   * 
     [!UICONTROL Group by]: `Created\_at` (retail month)
   * 
     [!UICONTROL Chart type]: `Line`

* **Présentation du calendrier de vente au détail (année de vente au détail précédente par mois)**
   * Mesure `A`: `Revenue`
      * 
        [!UICONTROL Mesure]: `Revenue`
      * [!UICONTROL Filter]:
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * Mesure `B`: `Orders`
      * [!UICONTROL Metric]: Nombre de commandes
      * [!UICONTROL Filter]:
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * Mesure `C`: `Avg order value`
      * [!UICONTROL Metric]: `Avg order value`
      * [!UICONTROL Filter]:
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Interval]: `None`
   * 
     [!UICONTROL Group by]: `Created\_at` (retail month)
   * 
     [!UICONTROL Chart type]: `Line`

## Étapes suivantes

La section ci-dessus décrit comment configurer un calendrier de vente au détail pour qu’il soit compatible avec toute mesure créée sur votre `sales\_order` (par exemple, `Revenue` ou `Orders`). Vous pouvez également l’étendre afin de prendre en charge le calendrier de vente au détail pour les mesures créées sur n’importe quel tableau. La seule condition requise est que ce tableau comporte un champ date-time valide qui peut être utilisé pour la jointure à la table Calendrier de vente au détail.

Par exemple, pour afficher les mesures au niveau du client sur un calendrier de vente au détail 4-5-4, créez une `Same Table` dans le `customer\_entity` tableau, similaire à `\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)` décrits ci-dessus. Vous pouvez ensuite utiliser cette colonne pour reproduire la variable `One to Many` calculs JOINED\_COLUMN (comme `Created_at (retail year)`) et `Include in previous retail year? (Yes/No)` en rejoignant la `customer\_entity` au `Retail Calendar` table.

N&#39;oubliez pas de [ajouter toutes les nouvelles colonnes en tant que dimensions aux mesures ;](../data-warehouse-mgr/manage-data-dimensions-metrics.md) avant de créer de nouveaux rapports.
