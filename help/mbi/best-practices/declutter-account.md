---
title: Découpage de votre compte  [!DNL Commerce Intelligence]
description: Découvrez comment nettoyer votre compte  [!DNL Commerce Intelligence] .
exl-id: 5fcdac2d-41ca-4011-b646-a699d9ecc6e4
role: Admin, User
feature: Accounts
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 0%

---

# Nettoyer votre compte [!DNL Adobe Commerce Intelligence]

Que vous soyez avec [!DNL Commerce Intelligence] depuis six mois ou six ans, la maintenance d’un compte ordonné est essentielle pour que votre organisation tire le meilleur parti de la plateforme. Au fil du temps, il est naturel que des utilisateurs, des tableaux de bord, des rapports, des mesures et des colonnes ne soient plus nécessaires. Peut-être avez-vous créé un rapport à usage unique et l’avez-vous oublié ou un utilisateur qui a quitté votre société n’a jamais eu son compte désactivé.

Grâce à l’attribution de [ noms normalisés et clairs pour tous les éléments ](../best-practices/naming-elements.md) de votre compte [!DNL Commerce Intelligence], les étapes de contrôle du compte ci-dessous vous permettent de réduire les analyses encombrantes et inutiles pour vos utilisateurs. [cycles de mise à jour potentiellement plus rapides](../best-practices/reduce-update-cycle-time.md) constitue un autre avantage.

## Étape 1 : identification des utilisateurs non actifs

La première étape du nettoyage de votre compte consiste à désactiver les comptes de vos utilisateurs non actifs, tels que les personnes qui ont quitté l’entreprise ou qui n’utilisent plus [!DNL Commerce Intelligence] dans leurs rôles actuels.

Pour ce faire, cliquez sur le nom de votre société dans la barre de navigation supérieure droite, puis sélectionnez **[!UICONTROL Manage Users]**. Sélectionnez ensuite l’utilisateur à désactiver et cliquez sur **[!UICONTROL Deactivate User]**.

>[!NOTE]
>
>Pour ce faire, vous avez besoin des [autorisations d’administrateur](../administrator/user-management/user-management.md).

>[!WARNING]
>
>La désactivation d’un utilisateur supprime les graphiques, les tableaux de bord et autres ressources créés par cet utilisateur. Si vous souhaitez conserver ces ressources, contactez l’équipe [!DNL Commerce Intelligence] [support](../guide-overview.md#Submitting-a-Support-Ticket) avant de désactiver l’utilisateur. L’assistance peut vous aider à transférer ces ressources à un autre utilisateur.

### Réactivation d’un utilisateur

Pour réactiver un utilisateur, réinvitez-le en recréant son compte avec la même adresse électronique que celle qui a été désactivée. De plus, son accès et les données qu’il possède sont restaurés lors de la connexion.

## Étape 2 : suppression des tableaux de bord et des rapports inutilisés

L’étape suivante du contrôle de votre compte consiste à supprimer les tableaux de bord et les rapports inutilisés.

>[!NOTE]
>
>Pour ce faire, vous avez besoin de `Admin` ou de `Standard` [ ](../administrator/user-management/user-management.md) autorisations utilisateur.

Chaque utilisateur disposant d’un accès `Admin` ou `Standard` peut créer des rapports et des tableaux de bord. Pour cette raison, toute personne disposant de ces autorisations doit suivre les étapes ci-dessous pour identifier et supprimer les rapports inutilisés.

### Vérification des tableaux de bord et des rapports

Avant de supprimer quoi que ce soit, vous devez consulter vos rapports et tableaux de bord pour évaluer l’utilisation actuelle. Bien que vous puissiez utiliser la fonction **[!UICONTROL find unused reports]** décrite ci-dessous, toute révision initiale rend vos efforts de nettoyage beaucoup plus productifs.

### Suppression de tableaux de bord et de rapports

Après avoir accédé à vos tableaux de bord et rapports, vous pouvez commencer à nettoyer votre compte.

**Pour supprimer un rapport d’un tableau de bord**

1. Localisez le rapport à supprimer sur le tableau de bord.
1. Sélectionnez **[!UICONTROL Options]** dans le coin supérieur droit du rapport.
1. Cliquez sur **[!UICONTROL Remove From Dashboard]**.

**Pour supprimer un tableau de bord entier**

1. Sélectionnez **[!UICONTROL Manage Data]**, puis **[!UICONTROL Dashboards**].
1. Cliquez sur le tableau de bord que vous souhaitez supprimer.
1. Cliquez sur **[!UICONTROL Delete Dashboard]**.

Vous pouvez également sélectionner **[!UICONTROL Dashboard Options]**, puis **[!UICONTROL Delete]** dans le tableau de bord lui-même.

![](../../mbi/assets/Delete_from_dashboard.png)

>[!NOTE]
>
>La suppression d’un tableau de bord ne supprime pas les rapports qu’il contient. Vous devez donc effectuer une nouvelle étape pour supprimer les rapports.

**Pour Supprimer Des Rapports Inutilisés**

1. Sélectionnez **[!UICONTROL Manage Data]**, puis **[!UICONTROL Reports]**.
1. Cochez la case **Afficher uniquement les rapports inutilisés** située sous la liste des mesures. Cette opération crée une liste des rapports qui ne sont pas utilisés dans un tableau de bord ou un résumé d’email.
1. Sélectionnez les rapports à supprimer. Vous pouvez tout sélectionner en cochant la case située au-dessus de la liste des rapports.
1. Cliquez sur **[!UICONTROL Delete Selected]**.

Voici un aperçu du processus de suppression des rapports inutilisés :

![](../../mbi/assets/unused_reports.png)

## Étape 3 : suppression des mesures inutilisées

Après avoir nettoyé la liste des utilisateurs, les tableaux de bord et les rapports, vous pouvez passer au contrôle de votre liste de mesures. Cela vous permet d’identifier tout élément qui pourrait être obsolète (par exemple, une nouvelle mesure a été créée avec une définition différente) ou qui n’a pas été utilisé.

1. Pour générer une liste des rapports dépendants pour une mesure, accédez à **[!DNL Manage Data]**, puis sélectionnez Click **[!UICONTROL Metrics]**.
1. Cliquez sur **[!UICONTROL Edit]** en regard d’une mesure.
1. Au bas de la page, une section intitulée **[!UICONTROL Dependent Charts]** s’affiche. Cliquez sur le lien pour générer une liste de rapports dépendants pour cette mesure.
1. Une fois la vérification terminée par le système, [!DNL Commerce Intelligence] affiche la liste des tableaux de bord, des rapports et des utilisateurs qui utilisent cette mesure.

![](../../mbi/assets/report_dependecies.png)

Si vous décidez que la mesure n’est plus nécessaire, revenez à la page **[!UICONTROL Metrics]** en cliquant sur **[!UICONTROL Back to Metric List]** pour trouver la mesure à supprimer. Cliquez sur **[!UICONTROL Delete]**.

## Étape 4 : évaluation des colonnes synchronisées

La dernière étape consiste à évaluer les colonnes en cours de synchronisation dans votre Data Warehouse. Non seulement la désynchronisation des colonnes peut désencombrer votre compte, mais elle peut aussi potentiellement réduire le temps de mise à jour.

Si vous souhaitez poursuivre, contactez [!DNL Commerce Intelligence] [Support](../guide-overview.md#Submitting-a-Support-Ticket). L’équipe d’assistance peut créer un rapport qui inclut toutes les colonnes qui ne sont utilisées dans aucun tableau de bord pour aucun utilisateur et qui ne sont pas utilisées dans les résumés d’emails, à l’exception des rapports SQL. Vous pouvez ensuite utiliser ce rapport comme guide pour sélectionner les colonnes à désynchroniser via le Gestionnaire de Data Warehouse.

>[!NOTE]
>
>Vous pourrez toujours recommencer à synchroniser ces colonnes à l’avenir. La désynchronisation d’une colonne supprime toutes les données de votre Data Warehouse ; cela signifie uniquement que cette colonne n’est pas contrôlée pour les nouvelles valeurs ou les valeurs mises à jour pendant le cycle de mise à jour.

**Pour désynchroniser une colonne (ou colonnes)**

1. Accédez à **[!DNL Manage Data]**, puis **[!UICONTROL Data Warehouse]**.
1. Dans la liste **[!UICONTROL Synced Tables]**, accédez à la table contenant la colonne.
1. Cochez une ou plusieurs cases en regard d’une ou de plusieurs colonnes que vous souhaitez désynchroniser.
   >[!NOTE]
   >
   >Vous ne pouvez pas désynchroniser une colonne Clé de Principal sans déposer le tableau entier.

1. Cliquez sur **[!UICONTROL Remove]** pour désynchroniser une ou plusieurs colonnes.

Voici un aperçu de l’ensemble du processus :

![](../../mbi/assets/drop_column.png)

## Remplissage

Votre compte [!DNL Commerce Intelligence] doit maintenant être plus ordonné et plus facile à parcourir pour vous et votre équipe.
