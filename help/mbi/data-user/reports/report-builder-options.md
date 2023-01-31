---
title: Sélection d’un créateur de rapports
description: Découvrez comment choisir votre créateur de rapports.
exl-id: ec4204ef-975e-45c3-b09e-fb97ffc2c497
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 0%

---

# Sélection d’un créateur de rapports

>[!NOTE]
>>Nécessite [Autorisations d’administrateur](../../administrator/user-management/user-management.md).


Nous aimons tous avoir des options. Mais face à des choix, certains d&#39;entre nous rechigneront et se figeront peut-être à l&#39;idée de devoir s&#39;engager dans une décision. Les options sont excellentes, mais elles peuvent aussi être écrasantes et déroutantes.

Maintenant que vous disposez d’options supplémentaires pour la création d’analyses, il peut parfois être difficile de savoir exactement quel type de créateur de rapports répond à vos besoins. Si vous avez besoin de conseils sur le choix de la meilleure manière de créer votre analyse, cet article est à votre disposition.

## Quand dois-je utiliser la variable `SQL Report Builder`? {#whensql}

Jetez un coup d’oeil à quelques-unes des raisons les plus courantes pour lesquelles vous utiliseriez le Report Builder SQL plutôt que le Report Builder traditionnel.

### Si vous souhaitez utiliser des fonctions spécifiques à SQL...

Une partie de la beauté de la `SQL Report Builder` Cela vous permet d’utiliser des fonctions qui ne sont actuellement pas disponibles dans Data Warehouse Manager. Dans le passé, un analyste a peut-être dû intervenir pour vous aider à réaliser pleinement votre vision.

Le Report Builder SQL prend en charge des fonctions telles que [`LISTAGG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LISTAGG.html) et [`GETDATE`](https://docs.aws.amazon.com/redshift/latest/dg/r_GETDATE.html), que vous ne pouviez pas utiliser auparavant. Vous pouvez accéder au [`full list`](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html), mais d’autres fonctions spécifiques à SQL incluent :

* [`Bitwise aggregate` fonctions](https://docs.aws.amazon.com/redshift/latest/dg/c_bitwise_aggregate_functions.html)
* [`CASE expression`](https://docs.aws.amazon.com/redshift/latest/dg/r_CASE_function.html)
* [`JSON_EXTRACT_PATH_TEXT`](https://docs.aws.amazon.com/redshift/latest/dg/JSON_EXTRACT_PATH_TEXT.html)
* [`LOG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LOG.html)
* [`MONTHS_BETWEEN`](https://docs.aws.amazon.com/redshift/latest/dg/r_MONTHS_BETWEEN_function.html)
* [`REPLACE`](https://docs.aws.amazon.com/redshift/latest/dg/r_REPLACE.html)
* [`SQRT`](https://docs.aws.amazon.com/redshift/latest/dg/r_SQRT.html)
* [`concatenation` operator](https://docs.aws.amazon.com/redshift/latest/dg/r_concat_op.html)

### Si vous voulez faire des tests...

Si vous souhaitez essayer différentes techniques et stratégies pour déterminer ce qui fonctionne le mieux pour votre analyse, vous pouvez utiliser la variable `SQL Report Builder`. La création de colonnes dans Data Warehouse Manager prend du temps et les colonnes que vous créez à l’aide de la gestion des actifs numériques dépendent des cycles de mise à jour.

Au mieux, vous devez patienter un cycle de mise à jour avant de pouvoir utiliser votre colonne. Si vous réalisez que vous avez commis une erreur lors de la création de la colonne, vous devrez attendre *two* cycles : une pour remplir initialement la colonne, et un autre cycle pour propager les révisions.

### Si vous n’utilisez qu’une seule fois une nouvelle colonne...

Comme nous l’avons mentionné dans la section ci-dessus, la création d’une nouvelle colonne dans le Gestionnaire de Data Warehouse prend du temps. Si vous prévoyez d’utiliser uniquement une colonne que vous créez dans un rapport, nous vous conseillons d’utiliser la variable `SQL Report Builder`. Cela évite d’avoir à attendre la fin d’un cycle de mise à jour, ce qui vous permet de reprendre le travail plus rapidement.

### Si vous travaillez avec des données qui ont une relation de type &quot;un à plusieurs&quot;...

Dans certains cas, la structure de vos données peut créer la variable `SQL Report Builder` un choix plus efficace et logique pour construire votre analyse. La création de colonnes pour les relations un-à-un est assez simple dans le Gestionnaire de Data Warehouse, mais les choses peuvent devenir un peu déroutantes lorsque vous avez affaire à des relations un-à-plusieurs.

Supposons qu’un seul produit soit considéré comme faisant partie de plusieurs catégories de produits et que vous souhaitiez afficher les recettes associées à chaque catégorie de chaque produit. Tenter de créer cette relation à l’aide du DWM peut être fastidieux et difficile, mais écrire une requête SQL peut être un peu plus simple :

![](../../assets/When_should_I_use_the_RB_2.png)

## Quand dois-je utiliser le Report Builder traditionnel ? {#whentraditionalrb}

Lorsque la variable `SQL Report Builder` vous donne plus de contrôle et d’accès aux fonctionnalités qui n’étaient pas disponibles auparavant. Il peut ne pas toujours s’agir d’un bon choix. Nous vous suggérons également de tenir compte des points suivants lorsque vous décidez de l’aspect du créateur de rapports à utiliser.

### Si vous créez un rapport simple...

Si ce que vous souhaitez créer est simple, l’utilisation du Report Builder traditionnel peut être beaucoup plus rapide que l’écriture d’une requête SQL complète. Cela vous aidera également si les colonnes dont vous avez besoin pour créer l’analyse se trouvent déjà dans le Gestionnaire de Data Warehouse.

### Si vous partagerez votre travail avec d&#39;autres utilisateurs...

Les utilisateurs de votre entreprise utiliseront-ils/visualiseront-ils cette analyse ? Selon avec qui vous partagez votre travail, il peut être préférable, dans certains cas, de rester fidèle au Report Builder Visuel. Les utilisateurs peuvent consulter rapidement la définition dans le Report Builder visuel plutôt que de lire une requête SQL potentiellement longue.

Si certaines personnes ont besoin du rapport mais ne connaissent pas SQL, nous vous recommandons d’utiliser la version originale du Report Builder. Cela leur facilitera les choses.

## Remplissage {#wrapup}

Les deux `SQL Report Builder` et `Visual Report Builder` sont adaptés à un large éventail de cas d’utilisation. Cela dépend généralement de vos besoins analytiques et de qui utilisera l’analyse.
