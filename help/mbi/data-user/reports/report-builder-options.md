---
title: Sélection d’un créateur de rapports
description: Découvrez comment choisir votre créateur de rapports.
exl-id: ec4204ef-975e-45c3-b09e-fb97ffc2c497
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---

# Sélection d’un créateur de rapports

>[!NOTE]
>>Nécessite [Autorisations d’administrateur](../../administrator/user-management/user-management.md).

Maintenant que vous disposez d’options supplémentaires pour la création d’analyses, il peut parfois être difficile de savoir exactement quelle version du créateur de rapports correspond à vos besoins. Cette rubrique vous guide tout au long du choix du meilleur moyen de créer votre analyse.

## Quand dois-je utiliser le [!DNL SQL Report Builder] ? {#whensql}

Examinez quelques-unes des raisons les plus courantes pour lesquelles vous utiliseriez [!DNL SQL Report Builder] sur [!DNL traditional Report Builder].

### Si vous souhaitez utiliser des fonctions spécifiques à [!DNL SQL]...

L’intérêt de [!DNL SQL Report Builder] réside en partie dans le fait qu’il vous permet d’utiliser des fonctions qui ne sont actuellement pas disponibles dans le Gestionnaire de Data Warehouse. Dans le passé, un analyste a peut-être dû intervenir pour vous aider à réaliser pleinement votre vision.

[!DNL SQL Report Builder] prend en charge des fonctions telles que [`LISTAGG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LISTAGG.html) et [`GETDATE`](https://docs.aws.amazon.com/redshift/latest/dg/r_GETDATE.html), que vous ne pouviez pas utiliser auparavant. Vous pouvez accéder à [`full list`](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html), mais certaines autres fonctions spécifiques à SQL incluent :

* [`Bitwise aggregate` fonctions](https://docs.aws.amazon.com/redshift/latest/dg/c_bitwise_aggregate_functions.html)
* [`CASE expression`](https://docs.aws.amazon.com/redshift/latest/dg/r_CASE_function.html)
* [`JSON_EXTRACT_PATH_TEXT`](https://docs.aws.amazon.com/redshift/latest/dg/JSON_EXTRACT_PATH_TEXT.html)
* [`LOG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LOG.html)
* [`MONTHS_BETWEEN`](https://docs.aws.amazon.com/redshift/latest/dg/r_MONTHS_BETWEEN_function.html)
* [`REPLACE`](https://docs.aws.amazon.com/redshift/latest/dg/r_REPLACE.html)
* [`SQRT`](https://docs.aws.amazon.com/redshift/latest/dg/r_SQRT.html)
* [`concatenation` opérateur](https://docs.aws.amazon.com/redshift/latest/dg/r_concat_op.html)

### Si vous voulez faire des tests...

Si vous souhaitez essayer différentes techniques et stratégies pour déterminer ce qui fonctionne le mieux pour votre analyse, vous pouvez utiliser le [!DNL SQL Report Builder]. La création de colonnes dans Data Warehouse Manager prend du temps et les colonnes que vous créez à l’aide du DWM dépendent des cycles de mise à jour.

Au mieux, vous devez patienter un cycle de mise à jour avant de pouvoir utiliser votre colonne. Si vous réalisez que vous avez commis une erreur lors de la création de la colonne, vous devez attendre jusqu’à *deux* cycles : un pour remplir initialement la colonne et un autre cycle pour que les révisions se propagent.

### Si vous utilisez une seule fois une nouvelle colonne...

Comme indiqué dans la section ci-dessus, la création d’une colonne dans le Gestionnaire de Data Warehouse prend du temps. Si vous ne prévoyez d’utiliser qu’une colonne que vous créez dans un rapport, Adobe vous suggère d’utiliser le [!DNL SQL Report Builder]. Cela évite d’avoir à attendre la fin d’un cycle de mise à jour, ce qui vous permet de reprendre le travail plus rapidement.

### Si vous utilisez des données qui ont une relation de type &quot;un à plusieurs&quot;...

Parfois, la structure de vos données peut faire du [!DNL SQL Report Builder] un choix plus efficace et logique pour créer votre analyse. La création de colonnes pour les relations un-à-un est simple dans le Gestionnaire de Data Warehouse, mais les choses peuvent devenir un peu déroutantes lorsque vous avez affaire à des relations un-à-plusieurs.

Supposons qu’un seul produit soit considéré comme faisant partie de plusieurs catégories de produits et que vous souhaitiez afficher les recettes associées à chaque catégorie de chaque produit. Tenter de créer cette relation à l’aide du DWM peut être fastidieux et difficile, mais écrire une requête [!DNL SQL] peut être un peu plus simple :

![](../../assets/When_should_I_use_the_RB_2.png)

## Quand dois-je utiliser le Report Builder traditionnel ? {#whentraditionalrb}

Bien que le [!DNL SQL Report Builder] vous donne plus de contrôle et d’accès aux fonctionnalités précédemment indisponibles, il peut ne pas toujours être le bon choix. Adobe suggère que vous preniez également en compte les éléments suivants lorsque vous décidez de l’aspect du créateur de rapports à utiliser.

### Si vous créez un rapport simple...

Si ce que vous souhaitez créer est simple, l’utilisation du Report Builder traditionnel peut être beaucoup plus rapide que l’écriture d’une requête [!DNL SQL] complète. Cela permet de savoir si les colonnes dont vous avez besoin pour créer l’analyse se trouvent déjà dans le Gestionnaire de Data Warehouse.

### Si vous partagez votre travail avec d’autres utilisateurs...

Les utilisateurs de votre entreprise utilisent-ils/consultent-ils cette analyse ? Selon avec qui vous partagez votre travail, il est parfois préférable de rester fidèle au Report Builder Visuel. Les utilisateurs peuvent consulter rapidement la définition dans [!DNL Visual Report Builder] au lieu de lire une requête [!DNL SQL] potentiellement longue.

Si certaines personnes ont besoin du rapport, mais ne connaissent pas [!DNL SQL], Adobe suggère d&#39;utiliser la version originale du Report Builder. Cela leur facilite la tâche.

## Remplissage {#wrapup}

Les [!DNL SQL Report Builder] et [!DNL Visual Report Builder] conviennent à un large éventail de cas d’utilisation. Cela dépend généralement des besoins analytiques et des personnes qui utilisent l’analyse.
