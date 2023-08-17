---
title: Exporter les données brutes
description: Découvrez comment exporter des enregistrements de votre [!DNL Commerce Intelligence] Data Warehouse pour mieux voir ce qui alimente votre tableau de bord.
exl-id: 26decdaf-2b2c-4ca2-b3d5-0386892662e8
role: Admin, Data Architect, Data Engineer, Leader, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# Exporter les données brutes

Grâce aux exportations de données brutes, vous pouvez exporter des enregistrements de votre Data Warehouse afin d’examiner de plus près ce qui alimente votre tableau de bord. En outre, les exportations de données brutes peuvent vous aider [Identifier les incohérences entre les données](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html).

Les exportations de données brutes permettent d’accéder à des colonnes et dimensions supplémentaires générées par la normalisation et la pré-agrégation des mesures pertinentes. Par exemple : `User's first order date` est une dimension que vous pouvez exporter pour chaque utilisateur dans . [!DNL Commerce Intelligence], bien qu’il puisse ne pas être disponible dans votre base de données.

Ce tutoriel porte sur les aspects suivants :

* [Sélection des données à exporter](#select)
* [Téléchargement de l&#39;export (](#download)
* [Accès aux exportations historiques](#historical)

## Étape 1 : sélection des données à exporter {#select}

Vous pouvez exporter des données brutes de deux manières différentes dans [!DNL Commerce Intelligence]:

1. au niveau du graphique
1. au niveau du tableau

### Exportation au niveau du tableau dans votre [!UICONTROL Manage Data] Onglet

Si vous souhaitez exporter le tableau à partir de [!UICONTROL Manage Data] , vous devez [Administration](../administrator/user-management/user-management.md) autorisations.

1. Cliquez sur **[!UICONTROL Manage Data** > ** Exporter les données **> **Exportation de données brutes]**.
1. Vous voyez une `Export List` des exportations de données récemment créées, le cas échéant. Cliquez sur **[!UICONTROL Add Export]** pour créer un export.
1. La variable `New Raw Data Export` s’affiche. Vous pouvez personnaliser votre export en sélectionnant ou en désélectionnant des colonnes et des filtres :

   * `Table` - La variable `Table` sélectionne la table à partir de laquelle les données sont exportées. Par défaut, le tableau dans lequel vous avez accédé s’affiche.
   * `Export Name` - Dans ce champ, saisissez le nom de l&#39;export. Par exemple: `Philadelphia - Daily Revenue`.
   * `Available Columns` - Ce champ répertorie les colonnes (dimensions) de votre base de données qui peuvent être incluses dans l’exportation. Pour ajouter une colonne, cliquez sur son nom.
   * `Selected Columns` - Ce champ répertorie les colonnes (dimensions) actuellement incluses dans l’exportation. Pour supprimer une colonne, cliquez sur son nom.
   * `Filter` - Cette section répertorie les filtres actuellement appliqués à l&#39;export. Ces filtres peuvent être modifiés ; de nouveaux filtres peuvent également être ajoutés pour exporter un jeu de données spécifique.
   * Lorsque vous avez terminé, cliquez sur **[!UICONTROL Export Data]**.

### Exportation au niveau du graphique à partir du tableau de bord

1. Cliquez sur l’icône d’engrenage dans le coin supérieur droit d’un graphique.

1. Sélectionner `Raw Export` dans la liste déroulante pour afficher la variable `Raw Export` boîte de dialogue.

1. Personnalisez l’exportation en sélectionnant le `table`, `columns`, et `filters` à inclure ou à exclure. Reportez-vous à la section précédente pour plus d&#39;informations sur les champs de ce module.

   >[!NOTE]
   >
   >Le tableau qui s’affiche dans la variable `Table` est, par défaut, le tableau qui alimente le graphique.

1. Lorsque vous avez terminé, cliquez sur **[!UICONTROL Export Data]**.

Examinez l’ensemble du processus au niveau du graphique.

![](../assets/Chart-level_export.gif)

## Etape 2 : téléchargement de l&#39;export {#download}

L’exportation commence à être traitée immédiatement après avoir terminé vos sélections dans la `Raw Data Export` boîte de dialogue. Comme certaines exportations peuvent être de grande taille, elles sont limitées à 10 millions de lignes et peuvent prendre un certain temps à s’exécuter.

Pour vérifier si votre exportation est prête, cliquez sur **[!UICONTROL Raw Data Exports]** dans le coin supérieur droit de l’écran. Cliquez sur **[!UICONTROL Download]** pour télécharger un fichier compressé `.csv` du fichier de votre exportation.

![](../assets/Downloading_export.gif)

## Etape 3 : accès aux exportations historiques {#historical}

Pour afficher vos exportations antérieures, cliquez sur **[!UICONTROL Raw Data Export]** dans le coin supérieur droit de l’écran. Les rapports en attente et terminés sont accessibles pendant sept jours au maximum.
