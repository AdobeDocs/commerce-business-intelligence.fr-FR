---
title: Gestion des utilisateurs et des autorisations Adobe Commerce
description: Découvrez comment gérer vos utilisateurs de Commerce Intelligence.
exl-id: 2a5eeabb-3c13-4ca1-b845-ed255b389c9f
role: Admin, User
feature: User Management
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# Gestion des autorisations utilisateur

[!DNL Adobe Commerce Intelligence] est conçu pour être une source unique de vérité dans votre organisation. Chaque utilisateur dispose de son propre ensemble de tableaux de bord, qu’il peut [partager avec d’autres utilisateurs](../../data-user/dashboards/share-dashboard-with-users.md).

## Niveaux d’autorisation des utilisateurs

Dans [!DNL Commerce Intelligence], trois niveaux d’autorisation généraux s’appliquent aux utilisateurs. Ils sont sélectionnés lors de la création d’un compte :

* `Admin`
* `Standard`
* `Read-Only`

Ces autorisations permettent aux utilisateurs d’effectuer certaines actions ou d’accéder à des parties spécifiques de [!DNL Commerce Intelligence]. Voici un tableau de ce que chaque niveau d’autorisation peut faire dans [!DNL Commerce Intelligence]:

|   | `Admin` | `Standard` | `Read Only` |
| -----|-----|-----|----|
| **Créer/gérer des utilisateurs** | ✔ |   |   |
| **Création de résumés d’emails** | ✔ | ✔ |   |
| **Créer/modifier/partager des tableaux de bord** | ✔ | ✔ |   |
| **Affichage des tableaux de bord** | ✔ | ✔ | ✔ |
| **Créer/modifier/supprimer des rapports visuels** | ✔ | ✔* |   |
| **Créer/modifier/supprimer des rapports SQL** | ✔ |  |   |
| **Clonage des tableaux de bord** | ✔ |   |   |
| **Ajouter/gérer des intégrations** | ✔ |   |   |
| **Accès à Data Warehouse Manager** | ✔ |   |   |
| **Tables et colonnes de synchronisation/désynchronisation** | ✔ |   |   |
| **Créer/modifier des mesures** | ✔ |   |   |
| **Créer/modifier des jeux de filtres** | ✔ |   |   |
| **Créer/modifier des colonnes calculées** | ✔ |   |   |
| **Créer une liste de rapports dépendants** | ✔ |   |   |
| **Résumé du système d’accès** | ✔ |   |   |
| **Accès aux paramètres de fuseau horaire** | ✔ |   |   |
| **Facturation d’accès** | ✔ | ✔** |   |
| **Contacter le support technique** | ✔ | ✔ | ✔ |

{style="table-layout:auto"}

>[!NOTE]
>
>_Vous pouvez limiter une **[!UICONTROL Standard]**de l’utilisateur [accès à des mesures spécifiques](../../administrator/user-management/restrict-metric-access.md)._
>
>**[!UICONTROL Standard] _Les utilisateurs peuvent accéder à la Facturation avec un paramètre d’autorisation supplémentaire._
>
>**[!UICONTROL Read-Only]** Les utilisateurs peuvent uniquement _view_ les tableaux de bord qui ont été partagés avec eux ; ils ne peuvent rien créer ni modifier dans [!DNL Commerce Intelligence], ils ne peuvent pas non plus rechercher et ajouter de nouveaux tableaux de bord à leur compte. Adobe vous recommande de partager un ensemble spécifique de tableaux de bord avec **[!UICONTROL Read-Only]** utilisateurs que vous ou un autre membre de votre équipe maintenez. Ne clonez pas un ensemble de tableaux de bord à leur place.

## Autorisations supplémentaires : Facturation et support technique {#billingtech}

Outre les niveaux d’autorisation généraux, deux autres désignations d’utilisateur existent également : `Billing` et `Technical`. Ces désignations doivent être utilisées avec les niveaux d’autorisation généraux.

### Facturation

`Billing` les utilisateurs ont accès à la page de facturation et peuvent modifier les informations de paiement. Ils peuvent également être contactés par Adobe pour des questions de facturation.

`Admin` Les utilisateurs ont accès au `Billing` par défaut, mais `Standard` les utilisateurs peuvent également accéder à s’ils disposent de la variable `Billing` case à cocher sélectionnée sur leur profil.

![facturation](../../assets/billing.png)<!--{: width="550" height="363"}-->

### Technique

`Technical` Les utilisateurs ne disposent d’aucune autorisation spécifique : ce paramètre marque simplement un contact technique au sein de votre organisation. Ces utilisateurs peuvent être contactés par Adobe pour des questions techniques.

`Admin` les utilisateurs peuvent ajouter de nouveaux utilisateurs à leur compte en cliquant sur **[!UICONTROL Account Settings]** > **[!UICONTROL Create Users]** et suivez les invites. Une fois l’utilisateur créé dans [!DNL Commerce Intelligence], la personne chanceuse que vous invitez recevra des instructions par courrier électronique sur la manière d’effectuer le processus de configuration du compte.

À tout moment, `Admins` peuvent afficher tous les utilisateurs de leur compte en cliquant sur **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**. Cette page affiche les autorisations de l’utilisateur, ainsi que les mesures et les tableaux de bord auxquels il peut accéder.
