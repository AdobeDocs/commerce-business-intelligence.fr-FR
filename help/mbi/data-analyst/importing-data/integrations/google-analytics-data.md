---
title: Données Google Analytics attendues
description: Découvrez comment interagir avec vos mesures Google Analytics.
exl-id: db9fdaaa-47a9-4095-b1f8-9b6c74c25b7c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# Valeur attendue [!DNL Google Analytics] data

Après avoir connecté une [!DNL Google Analytics] intégration, vous pouvez interagir avec votre [!DNL Google Analytics] mesures *immédiatement dans la variable`Visual Report Builder`*. Lorsque vous saisissez la variable `Visual Report Builder`, si vous cliquez sur **[!UICONTROL Add a Metric]**, une série de mesures de votre [!DNL Google Analytics] s’affiche dans une liste déroulante sous les mesures de votre Data Warehouse.

La variable [!DNL Google Analytics] l’intégration *live* — cela signifie que la variable `Report Builder` demande des données depuis [!DNL Google Analytics] *immédiatement* lorsque vous ajoutez une mesure à votre rapport. Cela signifie également que les mesures auxquelles vous pouvez accéder sont définies exactement comme elles se trouvent dans [!DNL Google Analytics], et que ces valeurs ne sont pas *entreposé* dans votre [!DNL Commerce Intelligence] compte : s’affichait visuellement uniquement dans vos rapports.

+++Mesures et Dimensions prises en charge (Google Analytics 3 ou Universal Analytics)

>[!NOTE]
>
>Le 1er juillet 2023, Analytics universel standard ([!DNL Google Analytics] 3) Les propriétés ne traiteront plus les données. Vous pourrez consulter vos rapports Analytics universels pour une période postérieure au 1er juillet 2023. Toutefois, les nouvelles données ne seront introduites que dans [!DNL Google Analytics] 4 propriétés.

[!DNL Google Analytics] intégrations dans [!DNL Commerce Intelligence] utilisez la méthode [!DNL Google Analytics] [API Core Reporting](https://developers.google.com/analytics/devguides/reporting/core/v3/)et prennent en charge les mesures et dimensions suivantes.

>[!NOTE]
>
>Pour éviter des résultats inattendus ou absurdes, vérifiez que les dimensions que vous utilisez sont compatibles avec une ou plusieurs mesures que vous utilisez dans la variable `Report Builder`. Vous pouvez vérifier [here](https://ga-dev-tools.google/dimensions-metrics-explorer/).

## Mesures prises en charge

| [!DNL Commerce Intelligence] Nom d’affichage | [!DNL Google Analytics] Nom/Formule |
| --- | --- |
| `Page Views` | `ga:pageviews` |
| `Total Time Spent On Page` | `ga:timeOnPage` |
| `Bounces (One Page Visits)` | `ga:bounces` |
| `Entrances` | `ga:entrances` |
| `Exits` | `ga:exits` |
| `Unique Pageviews` | `ga:uniquePageviews` |
| `Ad Clicks` | `ga:adClicks` |
| `Ad Cost` | `ga:adCost` |
| `Cost per Click (CPC)` | `ga:CPC` |
| `Cost per Thousand Impressions (CPM)` | `ga:CPM` |
| `Click-Through Rate (CTR)` | `ga:CTR` |
| `Impressions` | `ga:impressions` |
| `Product Revenue` | `ga:itemRevenue` |
| `Products Purchased` | `ga:itemQuantity` |
| `Revenue` | `ga:transactionRevenue` |
| `Transactions` | `ga:transactions` |
| `Shipping Revenue` | `ga:transactionShipping` |
| `Tax Revenue` | `ga:transactionTax` |
| `Unique Purchases` | `ga:uniquePurchases` |
| `Pageviews After Internal Search` | `ga:searchDepth` |
| `Visit Duration After Internal Search` | `ga:searchDuration` |
| `Exits After Internal Search` | `ga:searchExits` |
| `Internal Search Refinements` | `ga:searchRefinements` |
| `Unique Users Using Internal Search` | `ga:searchUniques` |
| `Bounce Rate` | `ga:visitBounceRate` |
| `Average Time on Page` | `ga:avgTimeOnPage` |
| `Average Session Length` | `ga:avgSessionDuration` |
| `All Goals Conversion Rate` | `ga:goalConversionRateAll` |
| `Total Events` | `ga:totalEvents` |
| `Unique Events` | `ga:uniqueEvents` |
| `Event Value` | `ga:eventValue` |
| `Average Domain Lookup Time` | `ga:avgDomainLookupTime` |
| `Average Page Download Time` | `ga:avgPageDownloadTime` |
| `Average Page Load Time` | `ga:avgPageLoadTime` |
| `Transactions Per Visit` | `ga:transactionsPerVisit` |
| `Sessions` | `ga:sessions` |
| `Users` | `ga:users` |
| `New Users | ga:newUsers` |
| `Sessions Where Internal Search Used` | `ga:searchSessions` |
| `Goal X Starts` | `ga:goal...Starts` |
| `Goal X Completions` | `ga:goal...Completions` |
| `Goal X Conversion Rate` | `ga:goal...ConversionRate` |
| `Goal X Total Value` | `ga:goal...Value` |
| `All Goal Starts` | `ga:goalStartsAll` |
| `All Goal Completions` | `ga:goalCompletionsAll` |
| `All Goals Conversion Rate` | `ga:goalConversionRateAll` |
| `Total Goal Value` | `ga:goal1ValueAll` |

{style="table-layout:auto"}

## Dimensions prises en charge

| [!DNL Commerce Intelligence] Nom d’affichage | [!DNL Google Analytics] Nom/Formule | Groupable ? |
| --- | --- | --- |
| `Ad Content` | `ga:adContent` | `Yes` |
| `Ad Group` | `ga:adGroup` | `Yes` |
| `Matched Search Query` | `ga:adMatchedQuery` | `Yes` |
| `Placement Domain` | `ga:adPlacementDomain` | `Yes` |
| `Placement URL` | `ga:adPlacementUrl` | `Yes` |
| `Affiliation` | `ga:affiliation` | `Yes` |
| `Browser` | `ga:browser` | `Yes` |
| `Browser Version` | `ga:browserVersion` | `Yes` |
| `Campaign` | `ga:campaign` | `Yes` |
| `Continent` | `ga:continent` | `Yes` |
| `Custom Variable 2` | `ga:customVarValue2` | `Yes` |
| `Custom Variable 3` | `ga:customVarValue3` | `Yes` |
| `Custom Variable 5` | `ga:customVarValue5` | `Yes` |
| `Date` | `ga:date` | `No` |
| `Day` | `ga:day` | `No` |
| `Days Since Last Session` | `ga:daysSinceLastSession` | `Yes` |
| `Days Since Referring Campagin` | `ga:daysToTransaction` | `Yes` |
| `Device Category` | `ga:deviceCategory` | `Yes` |
| `Custom Dimension 10` | `ga:dimension10` | `Yes` |
| `Custom Dimension 12` | `ga:dimension12` | `Yes` |
| `Custom Dimension 13` | `ga:dimension13` | `Yes` |
| `Custom Dimension 18` | `ga:dimension18` | `Yes` |
| `Custom Dimension 2` | `ga:dimension2` | `Yes` |
| `Custom Dimension 20` | `ga:dimension20` | `Yes` |
| `Custom Dimension 3` | `ga:dimension3` | `Yes` |
| `Custom Dimension 4` | `ga:dimension4` | `Yes` |
| `Custom Dimension 5` | `ga:dimension5` | `Yes` |
| `Custom Dimension 8` | `ga:dimension8` | `Yes` |
| `Custom Dimension 9` | `ga:dimension9` | `Yes` |
| `Event Action` | `ga:eventAction` | `Yes` |
| `Event Category` | `ga:eventCategory` | `Yes` |
| `Event Label` | `ga:eventLabel` | `Yes` |
| `Exit Page Path` | `ga:exitPagePath` | `Yes` |
| `Flash Version Supported` | `ga:flashVersion` | `Yes` |
| `Hour` | `ga:hour` | `No` |
| `In-Market Segment` | `ga:interestInMarketCategory` | `Yes` |
| `Language` | `ga:language` | `Yes` |
| `Longitude` | `ga:longitude` | `No` |
| `Medium` | `ga:medium` | `Yes` |
| `Metro` | `ga:metro` | `Yes` |
| `Mobile Device Branding` | `ga:mobileDeviceBranding` | `Yes` |
| `Mobile Device Info` | `ga:mobileDeviceInfo` | `Yes` |
| `Month` | `ga:month` | `No` |
| `Operating System` | `ga:operatingSystem` | `Yes` |
| `Operating System Version` | `ga:operatingSystemVersion` | `Yes` |
| `Pages Viewed per Session` | `ga:pageDepth` | `Yes` |
| `Page Path` | `ga:pagePath` | `Yes` |
| `Product Category` | `ga:productCategory` | `Yes` |
| `Product Name` | `ga:productName` | `Yes` |
| `Referral URL` | `ga:referralPath` | `No` |
| `Region (State)` | `ga:region` | `Yes` |
| `Screen Colors` | `ga:screenColors` | `Yes` |
| `Screen Resolution` | `ga:screenResolution` | `Yes` |
| `Internal Search Category` | `ga:searchCategory` | `Yes` |
| `Internal Search Refined Keyword(s)` | `ga:searchKeywordRefinement` | `Yes` |
| `Internal Search Used?` | `ga:searchUsed` | `Yes` |
| `Second Page Path` | `ga:secondPagePath` | `Yes` |
| `Source` | `ga:source` | `Yes` |
| `Sub-Continent` | `ga:subContinent` | `Yes` |
| `Transaction ID` | `ga:transactionId` | `Yes` |
| `Custom (User Defined) Value` | `ga:userDefinedValue` | `Yes` |
| `Year` | `ga:year` | `No` |

{style="table-layout:auto"}

+++

+++Mesures et Dimensions prises en charge (Google Analytics 4)

[!DNL Google Analytics] intégrations dans [!DNL Commerce Intelligence] utilisez la méthode [!DNL Google Analytics] [API de données v1 (GA4)](https://developers.google.com/analytics/devguides/reporting/data/v1).

>[!NOTE]
>
> Commerce Intelligence ne prend pas en charge les dimensions suivantes : `cohort`, `cohortNthDay`, `cohortNthMonth`, et `cohortNthWeek`.
>
>Pour éviter des résultats inattendus ou absurdes, vérifiez que les dimensions que vous utilisez sont compatibles avec une ou plusieurs mesures que vous utilisez dans la variable `Visual Report Builder`. Vous pouvez vérifier les [Explorateur de Dimensions et de mesures GA4](https://ga-dev-tools.google/ga4/dimensions-metrics-explorer/).

+++
