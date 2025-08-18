---
title: Analyse de la valeur de durée de vie prévue (LTV) pour Pro
description: Découvrez comment configurer un tableau de bord qui vous aide à comprendre la croissance de la valeur de la durée de vie du client et la valeur de durée de vie attendue de vos clients.
exl-id: e353b92a-ff3b-466b-b519-4f86d054c0bc
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Analyse de la valeur de durée de vie attendue

Cette rubrique explique comment configurer un tableau de bord qui vous aide à comprendre la croissance de la valeur de la durée de vie du client et la valeur de vie attendue de vos clients.

![](../../assets/exp-lifetim-value-anyalysis.png)

Cette analyse n&#39;est disponible que pour les clients de compte Pro sur la nouvelle architecture. Si votre compte a accès à la fonctionnalité `Persistent Views` sous la barre latérale `Manage Data`, vous êtes sur la nouvelle architecture et pouvez suivre les instructions répertoriées ici pour créer cette analyse vous-même.

Avant de commencer, vous devez vous familiariser avec le [créateur de rapports de cohorte](../dev-reports/cohort-rpt-bldr.md).

## Colonnes calculées

Colonnes à créer dans la table **commandes** si vous utilisez des mois de **30 jours** :

* [!UICONTROL Column name] : `Months between first order and this order`
* [!UICONTROL Column type] : `Same Table`
* &#x200B;
  [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input] : A = `Seconds between customer's first order date and this order`
* &#x200B;
  [!UICONTROL Datatype]: `Integer`
* **Définition:**`case when A is null then null when A <= 0 then '1'::int else (ceil(A)/2629800)::int end`

* [!UICONTROL Column name] : `Months since order`
* [!UICONTROL Column type] : `Same Table`
* &#x200B;
  [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input] : A = `created_at`
* &#x200B;
  [!UICONTROL Datatype]: `Integer`
* Définition : `case when created_at is null then null else (ceil((extract(epoch from current_timestamp) - extract(epoch from created_at))/2629800))::int end`

Colonnes à créer sur le tableau **`orders`** si vous utilisez **mois de calendrier** :

* [!UICONTROL Column name] : `Calendar months between first order and this order`
* [!UICONTROL Column type] : `Same Table`
* &#x200B;
  [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column inputs] :
   * `A` = `created_at`
   * `B` = `Customer's first order date`

* &#x200B;
  [!UICONTROL Datatype]: `Integer`
* Définition : `case when (A::date is null) or (B::date is null) then null else ((date_part('year',A::date) - date_part('year',B::date))*12 + date_part('month',A::date) - date_part('month',B::date))::int end`

* [!UICONTROL Column name] : `Calendar months since order`
* [!UICONTROL Column type] : `Same Table`
* &#x200B;
  [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input] : `A` = `created_at`
* &#x200B;
  [!UICONTROL Datatype]: `Integer`
* **Définition:**`case when A is null then null else ((date_part('year',current_timestamp::date) - date_part('year',A::date))*12 + date_part('month',current_timestamp::date) - date_part('month',A::date))::int end`

* [!UICONTROL Column name] : `Is in current month? (Yes/No)`
* [!UICONTROL Column type] : `Same Table`
* &#x200B;
  [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input] : A = `created_at`
* &#x200B;
  [!UICONTROL Datatype]: `String`
* Définition : `case when A is null then null when (date_trunc('month', current_timestamp::date))::varchar = (date_trunc('month', A::date))::varchar then 'Yes' else 'No' end`

## Mesures

### Instructions relatives aux mesures

Mesures à créer

* **Clients distincts par date de première commande**
   * Si vous activez les commandes d’invités, utilisez `customer_email`

* Dans le tableau **`orders`**
* Cette mesure effectue un **Comptage des valeurs distinctes**
* Dans la colonne **`customer_id`**
* Classé par l’horodatage **`Customer's first order date`**

>[!NOTE]
>
>Veillez à [ajouter toutes les nouvelles colonnes en tant que dimensions aux mesures](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) avant de créer de nouveaux rapports.

## Rapports

### Instructions du rapport

**Chiffre d’affaires attendu par client par mois**

* `A` de mesure : `Revenue (hide)`
   * `Calendar months between first order and this order` `<= X` (choisissez un nombre raisonnable pour X, par exemple 24 mois)
   * `Is in current month?` = `No`

* &#x200B;
  [!UICONTROL Metric]: `Revenue`
* [!UICONTROL Filter] :

* `B` de mesure : `All time customers (hide)`
   * `Is in current month?` = `No`

* [!UICONTROL Metric] : `New customers by first order date`
* [!UICONTROL Filter] :

* `C` de mesure : `All time customers by month since first order (hide)`
   * `Calendar months since order` `<= X`
   * `Is in current month?` = `No`

* [!UICONTROL Metric] : `New customers by first order date`
* [!UICONTROL Filter] :

* [!UICONTROL Formula] : `Expected revenue`
* [!UICONTROL Formula] : `A / (B - C)`
* &#x200B;
  [!UICONTROL Format]: `Currency`

Autres détails du graphique

* [!UICONTROL Time period] : `All time`
* Intervalle de temps : `None`
* [!UICONTROL Group by] : `Calendar months between first order and this order` - tout afficher
* Remplacez la `group by` de la mesure `All time customers` par Indépendant à l’aide de l’icône en forme de crayon située en regard de la `group by`
* Modifiez les champs de `Show top/bottom` comme suit :
   * [!UICONTROL Revenue] : `Top 24 sorted by Calendar months between first order and this order`
   * [!UICONTROL All time customers] : `Top 24 sorted by All time customers`
   * [!UICONTROL All time customers by month since first order] : `Top 24 sorted by All time customers by month since first order`

**Chiffre d’affaires moyen par mois, par cohorte**

* `A` de mesure : `Revenue`
* &#x200B;
  [!UICONTROL Metric view]: `Cohort`
* [!UICONTROL Cohort date] : `Customer's first order date`
* [!UICONTROL Perspective] : `Average value per cohort member`

**Chiffre d’affaires moyen cumulé par mois, par cohorte**

* `A` de mesure : `Revenue`
* &#x200B;
  [!UICONTROL Metric view]: `Cohort`
* [!UICONTROL Cohort date] : `Customer's first order date`
* [!UICONTROL Perspective] : `Cumulative average value per cohort member`

Après avoir compilé tous les rapports, vous pouvez les organiser selon vos besoins dans le tableau de bord. Le résultat peut ressembler à l’image en haut de la page.

Si vous avez des questions lors de la création de cette analyse ou si vous souhaitez simplement contacter l’équipe des services professionnels, [contactez l’assistance ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
