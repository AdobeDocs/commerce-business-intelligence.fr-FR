---
title: Différences entre SQL et Data Warehouse Manager
description: Découvrez les différences entre SQL et Data Warehouse Manager.
exl-id: 31dd7a04-5c03-4399-b67e-f51703eb9fea
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# Différences entre SQL et Data Warehouse Manager

Il existe deux différences clés entre les colonnes créées dans la variable [Report Builder SQL](../dev-reports/sql-rpt-bldr.md) et ceux créés à l’aide de la fonction [Gestionnaire de Data Warehouse](../data-warehouse-mgr/creating-calculated-columns.md): l’une est la dépendance aux cycles de mise à jour, l’autre est la manière dont les colonnes sont enregistrées dans votre compte.

## Colonnes dans la variable `SQL Report Builder`

Les colonnes ne dépendent pas des cycles de mise à jour. Il n’est donc plus nécessaire d’attendre qu’une colonne soit terminée avant de pouvoir effectuer une itération sur votre colonne. Si vous commettez une erreur, il suffit de quelques touches pour la corriger - plus d’attendre que deux mises à jour soient terminées avant de pouvoir reprendre le travail.

>[!IMPORTANT]
>
>Les colonnes que vous créez à l’aide de l’éditeur SQL ne sont pas enregistrées dans votre Data Warehouse. Vous avez toujours accès à la requête contenant la colonne, mais si vous souhaitez utiliser la colonne dans plusieurs rapports, vous devez la recréer dans la requête pour chaque rapport. Cela signifie que les colonnes créées à l’aide de l’éditeur SQL ne peuvent pas être utilisées dans les `Report Builder`.

## Colonnes dans le Gestionnaire de Data Warehouse

Les colonnes dépendent des cycles de mise à jour. Un cycle complet doit donc être terminé avant d’être modifié. Ces colonnes sont enregistrées dans le Gestionnaire de Data Warehouse et peuvent être utilisées dans les `Report Builder` ou `SQL Report Builder`.
