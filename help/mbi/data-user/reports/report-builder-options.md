---
title: Sélection d’un créateur de rapports
description: Découvrez comment choisir votre créateur de rapports.
exl-id: ec4204ef-975e-45c3-b09e-fb97ffc2c497
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 0%

---

# Sélection d’un créateur de rapports

>[!NOTE]
>>Nécessite [Autorisations d’administrateur](../../administrator/user-management/user-management.md).

Maintenant que vous disposez d’options supplémentaires pour la création d’analyses, il peut parfois être difficile de savoir exactement quelle version du créateur de rapports correspond à vos besoins. Cette rubrique vous guide tout au long du choix du meilleur moyen de créer votre analyse.

## Quand dois-je utiliser la variable [!DNL SQL Report Builder]? {#whensql}

Examinez quelques-unes des raisons les plus courantes pour lesquelles vous utiliseriez la variable [!DNL SQL Report Builder] via [!DNL traditional Report Builder].

### Si vous souhaitez utiliser [!DNL SQL]Fonctions spécifiques...

Une partie de la beauté de la [!DNL SQL Report Builder] Cela vous permet d’utiliser des fonctions qui ne sont actuellement pas disponibles dans Data Warehouse Manager. Dans le passé, un analyste a peut-être dû intervenir pour vous aider à réaliser pleinement votre vision.

Le [!DNL SQL Report Builder] prend en charge des fonctions comme [`LISTAGG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LISTAGG.html) et [`GETDATE`](https://docs.aws.amazon.com/redshift/latest/dg/r_GETDATE.html), que vous ne pouviez pas utiliser auparavant. Vous pouvez accéder au [`full list`](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html), mais d’autres fonctions spécifiques à SQL incluent :

* [`Bitwise aggregate` fonctions](https://docs.aws.amazon.com/redshift/latest/dg/c_bitwise_aggregate_functions.html)
* [`CASE expression`](https://docs.aws.amazon.com/redshift/latest/dg/r_CASE_function.html)
* [`JSON_EXTRACT_PATH_TEXT`](https://docs.aws.amazon.com/redshift/latest/dg/JSON_EXTRACT_PATH_TEXT.html)
* [`LOG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LOG.html)
* [`MONTHS_BETWEEN`](https://docs.aws.amazon.com/redshift/latest/dg/r_MONTHS_BETWEEN_function.html)
* [`REPLACE`](https://docs.aws.amazon.com/redshift/latest/dg/r_REPLACE.html)
* [`SQRT`](https://docs.aws.amazon.com/redshift/latest/dg/r_SQRT.html)
* [`concatenation` operator](https://docs.aws.amazon.com/redshift/latest/dg/r_concat_op.html)

### Si vous voulez faire des tests...

Si vous souhaitez essayer différentes techniques et stratégies pour déterminer ce qui fonctionne le mieux pour votre analyse, vous pouvez utiliser la variable [!DNL SQL Report Builder]. La création de colonnes dans Data Warehouse Manager prend du temps et les colonnes que vous créez à l’aide du DWM dépendent des cycles de mise à jour.

Au mieux, vous devez patienter un cycle de mise à jour avant de pouvoir utiliser votre colonne. Si vous réalisez que vous avez commis une erreur lors de la création de la colonne, vous devez attendre *two* cycles : une pour remplir initialement la colonne, et un autre cycle pour propager les révisions.

### Si vous n’utilisez qu’une seule fois une nouvelle colonne...

Comme indiqué dans la section ci-dessus, la création d’une colonne dans le Gestionnaire de Data Warehouse prend du temps. Si vous prévoyez d’utiliser uniquement une colonne que vous créez dans un rapport, Adobe suggère d’utiliser la variable [!DNL SQL Report Builder]. Cela évite d’avoir à attendre la fin d’un cycle de mise à jour, ce qui vous permet de reprendre le travail plus rapidement.

### Si vous travaillez avec des données qui ont une relation de type &quot;un à plusieurs&quot;...

Parfois, la structure de vos données peut créer la variable [!DNL SQL Report Builder] un choix plus efficace et logique pour construire votre analyse. La création de colonnes pour les relations un-à-un est simple dans le Gestionnaire de Data Warehouse, mais les choses peuvent devenir un peu déroutantes lorsque vous avez affaire à des relations un-à-plusieurs.

Supposons qu’un seul produit soit considéré comme faisant partie de plusieurs catégories de produits et que vous souhaitiez afficher les recettes associées à chaque catégorie de chaque produit. Tenter de créer cette relation à l’aide de la gestion des actifs numériques peut être fastidieux et difficile, mais écrire une [!DNL SQL] requête peut être un peu plus simple :

![](../../assets/When_should_I_use_the_RB_2.png)

## Quand dois-je utiliser le Report Builder traditionnel ? {#whentraditionalrb}

Lorsque la variable [!DNL SQL Report Builder] vous donne plus de contrôle et d’accès aux fonctionnalités qui n’étaient pas disponibles auparavant. Il peut ne pas toujours s’agir d’un bon choix. Adobe suggère que vous preniez également en compte les éléments suivants lorsque vous décidez de l’aspect du créateur de rapports à utiliser.

### Si vous créez un rapport simple...

Si ce que vous voulez créer est simple, l&#39;utilisation du Report Builder traditionnel peut être beaucoup plus rapide que d&#39;écrire une [!DNL SQL] requête. Cela permet de savoir si les colonnes dont vous avez besoin pour créer l’analyse se trouvent déjà dans le Gestionnaire de Data Warehouse.

### Si vous partagez votre travail avec d’autres utilisateurs...

Les utilisateurs de votre entreprise utilisent-ils/consultent-ils cette analyse ? Selon avec qui vous partagez votre travail, il est parfois préférable de rester fidèle au Report Builder Visuel. Les utilisateurs peuvent rapidement consulter la définition dans la variable [!DNL Visual Report Builder] par rapport à la lecture potentiellement longue [!DNL SQL] requête.

Si certaines personnes ont besoin du rapport mais ne connaissent pas bien [!DNL SQL], Adobe suggère d&#39;utiliser la saveur originale du Report Builder. Cela leur facilite la tâche.

## Remplissage {#wrapup}

Les deux [!DNL SQL Report Builder] et [!DNL Visual Report Builder] sont adaptés à un large éventail de cas d’utilisation. Cela dépend généralement des besoins analytiques et des personnes qui utilisent l’analyse.
