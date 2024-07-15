---
title: Utilisation du Report Builder SQL
description: Découvrez comment contrôler les données et les mesures à l’aide du Report Builder SQL afin de comparer les résultats aux données de votre base de données locale.
exl-id: d1d9e099-4138-43e6-aaec-6f15ebc5c4d4
role: Admin, Data Architect, Data Engineer, User
feature: Reports, Data Warehouse Manager, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---

# [!DNL SQL Report Builder]

L’ [!DNL SQL Report Builder] est principalement utilisé pour créer de nouveaux rapports et effectuer une itération sur les analyses, mais il peut également être utilisé pour contrôler efficacement les données et les mesures. Les informations suivantes expliquent comment contrôler les données et les mesures à l’aide de [!DNL SQL Report Builder] afin que vous puissiez comparer les résultats aux données de votre base de données locale.

## Requête sur une mesure

Pour commencer, ouvrez le [!DNL SQL Report Builder] en accédant à **[!UICONTROL Report Builder > SQL Report Builder > Create Report]**. Vous pouvez utiliser la barre latérale dans l’éditeur [!DNL SQL] pour insérer une mesure directement dans votre requête en survolant la mesure et en cliquant sur **[!UICONTROL Insert]**. La définition de requête de cette mesure est alors ajoutée à l’éditeur. La définition comprend les composants suivants :

- L’ **opération de mesure** en cours d’exécution, comme l’indique `SUM()` dans l’exemple ci-dessous.
- **table sur** dont la mesure est créée, indiquée par la clause `FROM`.
- Tout **filtre (et ensembles de filtres)** qui a été ajouté à la mesure, indiqué par la clause `WHERE` dans l’exemple ci-dessous.
- Composant de l’ **horodatage** (année, mois) sur lequel les données doivent être classées, indiqué par la clause `ORDER BY` dans l’exemple ci-dessous.

Pour avoir une vue plus claire de la requête, vous pouvez reformater son affichage dans le champ de requête. Une fois prêt, sélectionnez `Run Query`. Les résultats sont renseignés sous la forme d’un tableau dans le panneau du rapport sous la requête.

![](../../assets/run-query-results.gif)

## Limiter la requête

Si vous essayez d’identifier une incohérence ou un ensemble de données spécifique, vous devez limiter la requête à un échantillon spécifique pour vérifier votre base de données locale. Pour ce faire, modifiez la requête afin qu’elle corresponde aux restrictions souhaitées. Dans l’exemple suivant, vous limitez la requête à inclure uniquement les recettes à partir du 1er janvier 2013 ou d’une date ultérieure. Après avoir mis à jour la requête, sélectionnez à nouveau **[!UICONTROL Run Query]** pour mettre à jour les résultats.

![](../../assets/restricting-query.gif)

## Enregistrement et export

Lorsque le rapport répond à vos besoins, attribuez-lui un nom distinct, cliquez sur **[!UICONTROL Save]**, puis sélectionnez le type de rapport à enregistrer et le tableau de bord. Lors du contrôle des mesures, Adobe recommande d’enregistrer le rapport en tant que `Table` et de l’enregistrer dans un tableau de bord de test.

Une fois le rapport enregistré, accédez à ce tableau de bord en sélectionnant `Go to Dashboard`. De là, vous pouvez exporter les données en recherchant le rapport et en sélectionnant **[!UICONTROL Options gear > Full `.csv`Exporter]** ou **[!UICONTROL Full Excel Export]**.

![](../../assets/export-dboard-data.gif)

## Requêtes personnalisées

Vous pouvez également écrire des requêtes personnalisées et exporter les résultats à comparer à votre base de données locale. En suivant les [instructions pour l’optimisation des requêtes](../../best-practices/optimizing-your-sql-queries.md), écrivez une requête dans l’éditeur SQL. Vous pouvez utiliser les boutons situés en haut de la barre latérale pour basculer entre les listes de tableaux et de mesures disponibles dans [!DNL SQL Report Builder] et les ajouter à votre requête. Lorsque votre requête personnalisée correspond à vos besoins, vous pouvez enregistrer le rapport et exporter ces données à partir du tableau de bord.

>[!NOTE]
>
>Si vous constatez une incohérence après le contrôle de vos données, consultez la rubrique d’assistance [Contacter l’assistance : écarts de données](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-data-discrepancies.html) pour plus d’informations sur les prochaines actions à entreprendre.
