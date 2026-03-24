---
title: Utilisation de SQL Report Builder
description: Découvrez comment auditer les données et les mesures à l’aide de SQL Report Builder afin de comparer les résultats avec les données de votre base de données locale.
exl-id: d1d9e099-4138-43e6-aaec-6f15ebc5c4d4
role: Admin, Developer, User
feature: Reports, Data Warehouse Manager, SQL Report Builder
TQID: https://experienceleague.adobe.com/7Yx7Kpir-xjz5TPuajN7CFsLjWAbY0AT3bKtBabA5Wk
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 507
ht-degree: 0%

---

# [!DNL SQL Report Builder]

Le [!DNL SQL Report Builder] est principalement utilisé pour créer de nouveaux rapports et itérer sur des analyses, mais il peut également être utilisé pour auditer efficacement les données et les mesures. Les informations suivantes expliquent comment auditer les données et les mesures à l’aide du [!DNL SQL Report Builder] afin de comparer les résultats avec les données de votre base de données locale.

## Interrogation d’une mesure

Pour commencer, ouvrez le [!DNL SQL Report Builder] en accédant à **[!UICONTROL Report Builder > SQL Report Builder > Create Report]**. Vous pouvez utiliser la barre latérale dans l’éditeur de [!DNL SQL] pour insérer une mesure directement dans votre requête en pointant sur la mesure et en cliquant sur **[!UICONTROL Insert]**. Cette action ajoute la définition de requête de cette mesure à l’éditeur. La définition comprend les éléments suivants :

- Opération **métrique** en cours d’exécution, indiquée par `SUM()` dans l’exemple ci-dessous.
- Le **tableau sur lequel la mesure est créée** indiqué par la clause `FROM`.
- Tous les **filtres (et ensembles de filtres)** qui ont été ajoutés à la mesure, indiqués par la clause `WHERE` dans l’exemple ci-dessous.
- Composant de la **date et heure** (année, mois) sur lequel les données doivent être commandées, indiqué par la clause `ORDER BY` dans l’exemple ci-dessous.

Pour avoir une vue plus claire de la requête, vous pouvez reformater son affichage dans le champ de requête. Une fois prêt, sélectionnez `Run Query`. Les résultats sont renseignés sous la forme d’un tableau dans le panneau de rapport sous la requête.

![Démonstration animée de l’exécution d’une requête SQL et de l’affichage des résultats](../../assets/run-query-results.gif)

## Restreindre la requête

Si vous tentez d’identifier une incohérence ou un ensemble de données spécifique, limitez la requête à un échantillon spécifique pour vérifier les performances de votre base de données locale. Vous pouvez le faire en modifiant la requête pour qu’elle corresponde aux restrictions souhaitées. Dans l’exemple suivant, vous limitez la requête pour inclure uniquement le chiffre d’affaires du 1er janvier 2013 ou ultérieur. Après avoir mis à jour la requête, sélectionnez à nouveau **[!UICONTROL Run Query]** pour mettre à jour les résultats.

![Démonstration animée de la restriction de la requête avec des filtres](../../assets/restricting-query.gif)

## Enregistrement et exportation

Lorsque le rapport répond à vos besoins, attribuez-lui un nom distinct, cliquez sur **[!UICONTROL Save]**, puis sélectionnez le type de rapport à enregistrer et le tableau de bord. Lors de l’audit des mesures, Adobe recommande d’enregistrer le rapport en tant que `Table` et de l’enregistrer dans un tableau de bord de test.

Une fois le rapport enregistré, accédez à ce tableau de bord en sélectionnant `Go to Dashboard`. De là, vous pouvez exporter les données en recherchant le rapport et en sélectionnant **[!UICONTROL Options gear > Full `.csv`Exporter]** ou **[!UICONTROL Full Excel Export]**.

![Démonstration animée de l’exportation des données du tableau de bord](../../assets/export-dboard-data.gif)

## Requêtes personnalisées

Vous pouvez également écrire des requêtes personnalisées et exporter les résultats pour les comparer à votre base de données locale. En suivant les [instructions pour l’optimisation des requêtes](../../best-practices/optimizing-your-sql-queries.md), écrivez une requête dans l’éditeur SQL. Vous pouvez utiliser les boutons situés en haut de la barre latérale pour basculer entre les listes de tableaux et de mesures disponibles dans le [!DNL SQL Report Builder] et les ajouter à votre requête. Lorsque votre requête personnalisée répond à vos besoins, vous pouvez enregistrer le rapport et exporter ces données à partir du tableau de bord.

>[!NOTE]
>
>Si vous constatez une incohérence après avoir vérifié vos données, reportez-vous à la rubrique de support [Contacter le support : incohérences des données](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-data-discrepancies.html) pour plus d’informations sur les actions à entreprendre ensuite.
