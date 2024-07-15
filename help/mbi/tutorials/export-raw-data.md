---
title: Exporter les données brutes
description: Découvrez comment exporter des enregistrements de votre  [!DNL Commerce Intelligence] Data Warehouse pour mieux voir ce qui alimente votre tableau de bord.
exl-id: 26decdaf-2b2c-4ca2-b3d5-0386892662e8
role: Admin, Data Architect, Data Engineer, Leader, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---

# Exporter les données brutes

Grâce aux exportations de données brutes, vous pouvez exporter des enregistrements de votre Data Warehouse afin d’examiner de plus près ce qui alimente votre tableau de bord. En outre, les exportations de données brutes peuvent vous aider à [identifier les incohérences de données](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html).

Les exportations de données brutes permettent d’accéder à des colonnes et dimensions supplémentaires générées par la normalisation et la pré-agrégation des mesures pertinentes. Par exemple, `User's first order date` est une dimension que vous pouvez exporter pour chaque utilisateur de [!DNL Commerce Intelligence], mais qui peut ne pas être disponible dans votre base de données.

Ce tutoriel porte sur les aspects suivants :

* [Sélection des données à exporter](#select)
* [Téléchargement de l&#39;export (](#download)
* [Accès aux exportations historiques](#historical)

## Étape 1 : sélection des données à exporter {#select}

Vous pouvez exporter des données brutes de deux manières différentes dans [!DNL Commerce Intelligence] :

1. au niveau du graphique
1. au niveau du tableau

### Exportation au niveau de la table dans votre onglet [!UICONTROL Manage Data]

Si vous souhaitez exporter la table à partir de l’onglet [!UICONTROL Manage Data], vous avez besoin des autorisations [Admin](../administrator/user-management/user-management.md).

1. Cliquez sur **[!UICONTROL Manage Data** > ** Exporter des données **> **Exportation de données brutes]**.
1. Un `Export List` des exportations de données récemment créées s’il en existe un. Cliquez sur **[!UICONTROL Add Export]** pour créer une exportation.
1. La boîte de dialogue `New Raw Data Export` s’affiche. Vous pouvez personnaliser votre export en sélectionnant ou en désélectionnant des colonnes et des filtres :

   * `Table` - Le champ `Table` sélectionne la table à partir de laquelle les données sont exportées. Par défaut, le tableau dans lequel vous avez accédé s’affiche.
   * `Export Name` - Dans ce champ, saisissez le nom de l’exportation. Par exemple : `Philadelphia - Daily Revenue`.
   * `Available Columns` - Ce champ répertorie les colonnes (dimensions) de votre base de données qui peuvent être incluses dans l’exportation. Pour ajouter une colonne, cliquez sur son nom.
   * `Selected Columns` - Ce champ répertorie les colonnes (dimensions) actuellement incluses dans l’exportation. Pour supprimer une colonne, cliquez sur son nom.
   * `Filter` - Cette section répertorie les filtres actuellement appliqués à l’exportation. Ces filtres peuvent être modifiés ; de nouveaux filtres peuvent également être ajoutés pour exporter un jeu de données spécifique.
   * Lorsque vous avez terminé, cliquez sur **[!UICONTROL Export Data]**.

### Exportation au niveau du graphique à partir du tableau de bord

1. Cliquez sur l’icône d’engrenage dans le coin supérieur droit d’un graphique.

1. Sélectionnez `Raw Export` dans la liste déroulante pour afficher la boîte de dialogue `Raw Export`.

1. Personnalisez l’exportation en choisissant les `table`, `columns` et `filters` à inclure ou exclure. Reportez-vous à la section précédente pour plus d&#39;informations sur les champs de ce module.

   >[!NOTE]
   >
   >Le tableau qui s’affiche dans le champ `Table` est, par défaut, le tableau qui alimente le graphique.

1. Lorsque vous avez terminé, cliquez sur **[!UICONTROL Export Data]**.

Examinez l’ensemble du processus au niveau du graphique.

![](../assets/Chart-level_export.gif)

## Etape 2 : téléchargement de l&#39;export {#download}

L’exportation commencera son traitement immédiatement après avoir terminé vos sélections dans la boîte de dialogue `Raw Data Export`. Comme certaines exportations peuvent être de grande taille, elles sont limitées à 10 millions de lignes et peuvent prendre un certain temps à s’exécuter.

Pour vérifier si votre exportation est prête, cliquez sur **[!UICONTROL Raw Data Exports]** dans le coin supérieur droit de l’écran. Cliquez sur **[!UICONTROL Download]** pour télécharger un fichier compressé `.csv` de votre exportation.

![](../assets/Downloading_export.gif)

## Etape 3 : accès aux exportations historiques {#historical}

Pour afficher vos exportations antérieures, cliquez sur **[!UICONTROL Raw Data Export]** dans le coin supérieur droit de l’écran. Les rapports en attente et terminés sont accessibles pendant sept jours au maximum.
