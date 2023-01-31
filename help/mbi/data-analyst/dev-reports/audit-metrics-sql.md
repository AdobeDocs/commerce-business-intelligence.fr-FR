---
title: Utilisation du Report Builder SQL
description: Découvrez comment contrôler les données et les mesures à l’aide du Report Builder SQL afin de comparer les résultats aux données de votre base de données locale.
exl-id: d1d9e099-4138-43e6-aaec-6f15ebc5c4d4
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---

# `SQL Report Builder`

Le `SQL Report Builder` est principalement utilisé pour créer de nouveaux rapports et effectuer une itération sur les analyses, mais il peut également être utilisé pour contrôler efficacement les données et les mesures. Les informations suivantes expliquent comment contrôler les données et les mesures à l’aide de la variable `SQL Report Builder` afin de comparer les résultats avec les données de votre base de données locale.

## Requête sur une mesure

Pour commencer, ouvrez le `SQL Report Builder` en accédant à **[!UICONTROL Report Builder > SQL Report Builder > Create Report]**. Vous pouvez utiliser la barre latérale dans l’éditeur SQL pour insérer directement une mesure dans votre requête en survolant la mesure et en cliquant sur **[!UICONTROL Insert]**. La définition de requête de cette mesure sera alors ajoutée à l’éditeur. La définition comprend les composants suivants :

- Le **opération de mesure** exécutée, comme indiqué par SUM() dans l’exemple ci-dessous.
- Le **table on** qui est la mesure créée, indiquée par la clause FROM.
- Quelconque **filtres (et ensembles de filtres)** qui ont été ajoutés à la mesure, comme indiqué par la clause WHERE dans l’exemple ci-dessous.
- Le composant du **timestamp** (année, mois) sur laquelle les données doivent être classées, comme indiqué par la clause ORDER BY dans l’exemple ci-dessous.

Si vous souhaitez avoir une vue plus claire de la requête, vous pouvez reformater son affichage dans le champ de requête. Lorsque vous êtes prêt, sélectionnez `Run Query`. Les résultats seront renseignés sous la forme d’un tableau dans le panneau du rapport sous la requête.

![](../../assets/run-query-results.gif)

## Limiter la requête

Si vous essayez d’identifier une incohérence ou un ensemble de données spécifique, vous devez limiter la requête à un échantillon spécifique pour vérifier votre base de données locale. Pour ce faire, modifiez la requête afin qu’elle corresponde aux restrictions souhaitées. Dans l’exemple suivant, nous limitons la requête aux seules recettes à partir du 1er janvier 2013 ou d’une date ultérieure. Une fois la requête mise à jour, sélectionnez **[!UICONTROL Run Query]** pour mettre à jour les résultats.

![](../../assets/restricting-query.gif)

## Enregistrement et export

Lorsque le rapport répond à vos besoins, enregistrez-le dans un tableau de bord en lui attribuant un nom distinct, en cliquant sur **[!UICONTROL Save]**, puis sélectionnez le type de rapport à enregistrer et le tableau de bord. Lors du contrôle des mesures, nous vous recommandons d’enregistrer le rapport sous la forme d’un `Table` et l’enregistrer dans un tableau de bord de test.

Une fois le rapport enregistré, accédez à ce tableau de bord en sélectionnant `Go to Dashboard`. De là, vous pouvez exporter les données en recherchant le rapport et en sélectionnant **[!UICONTROL Options gear > Full `.csv`Exporter]** ou **[!UICONTROL Full Excel Export]**.

![](../../assets/export-dboard-data.gif)

## Requêtes personnalisées

Vous pouvez également écrire des requêtes personnalisées et exporter les résultats à comparer à votre base de données locale. En procédant comme suit : [directives relatives à l’optimisation des requêtes](../../best-practices/optimizing-your-sql-queries.md), écrivez une requête dans l’éditeur SQL. Vous pouvez utiliser les boutons situés en haut de la barre latérale pour basculer entre les listes de tableaux et de mesures disponibles dans la variable `SQL Report Builder` et ajoutez-les à votre requête. Lorsque votre requête personnalisée correspond à vos besoins, vous pouvez enregistrer le rapport et exporter ces données à partir du tableau de bord.

### Toujours sur la sellette ?

Si vous constatez une incohérence après le contrôle de vos données, consultez la rubrique [Contacter l’assistance : Incohérences entre les données](https://support.magento.com/hc/en-us/articles/360016505312) article relatif à l’assistance pour plus d’informations sur les prochaines étapes.
