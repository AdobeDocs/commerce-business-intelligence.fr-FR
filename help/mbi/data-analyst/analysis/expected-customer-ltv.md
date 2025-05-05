---
title: Analyse de la valeur de durée de vie attendue (LTV) pour Pro
description: Découvrez comment configurer un tableau de bord qui vous aide à comprendre la croissance des valeurs de durée de vie des clients et la valeur de durée de vie attendue de vos clients.
exl-id: e353b92a-ff3b-466b-b519-4f86d054c0bc
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Analyse de la valeur de durée de vie attendue

Cette rubrique explique comment configurer un tableau de bord qui vous aide à comprendre la croissance des valeurs de durée de vie des clients et la valeur de durée de vie attendue de vos clients.

![](../../assets/exp-lifetim-value-anyalysis.png)

Cette analyse est uniquement disponible pour les clients de compte Pro sur la nouvelle architecture. Si votre compte a accès à la fonctionnalité `Persistent Views` sous la barre latérale `Manage Data`, vous utilisez la nouvelle architecture et pouvez suivre les instructions répertoriées ici pour générer vous-même cette analyse.

Avant de commencer, vous souhaitez vous familiariser avec le [créateur de rapports de cohortes.](../dev-reports/cohort-rpt-bldr.md)

## Colonnes calculées

Colonnes à créer sur la table **commandes** si vous utilisez **30 jours de mois** :

* [!UICONTROL Column name] : `Months between first order and this order`
* [!UICONTROL Column type] : `Same Table`
* &#x200B;
  [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input] : A = `Seconds between customer's first order date and this order`
* &#x200B;
  [!UICONTROL Datatype]: `Integer`
* **Définition :**`case when A is null then null when A <= 0 then '1'::int else (ceil(A)/2629800)::int end`

* [!UICONTROL Column name] : `Months since order`
* [!UICONTROL Column type] : `Same Table`
* &#x200B;
  [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input] : A = `created_at`
* &#x200B;
  [!UICONTROL Datatype]: `Integer`
* Définition : `case when created_at is null then null else (ceil((extract(epoch from current_timestamp) - extract(epoch from created_at))/2629800))::int end`

Colonnes à créer sur la table **`orders`** en cas d&#39;utilisation de **calendar** mois :

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
* **Définition :**`case when A is null then null else ((date_part('year',current_timestamp::date) - date_part('year',A::date))*12 + date_part('month',current_timestamp::date) - date_part('month',A::date))::int end`

* [!UICONTROL Column name] : `Is in current month? (Yes/No)`
* [!UICONTROL Column type] : `Same Table`
* &#x200B;
  [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input] : A = `created_at`
* &#x200B;
  [!UICONTROL Datatype]: `String`
* Définition : `case when A is null then null when (date_trunc('month', current_timestamp::date))::varchar = (date_trunc('month', A::date))::varchar then 'Yes' else 'No' end`

## Mesures

### Instructions de mesure

Mesures à créer

* **Clients distincts par date de première commande**
   * Si vous activez les commandes d’invités, utilisez `customer_email`

* Dans la table **`orders`**
* Cette mesure exécute un **décompte de valeurs distinctes**
* Sur la colonne **`customer_id`**
* Ordonné par l’horodatage **`Customer's first order date`**

>[!NOTE]
>
>Veillez à [ajouter toutes les nouvelles colonnes en tant que dimensions aux mesures](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) avant de créer de nouveaux rapports.

## Rapports

### Instructions du rapport

**Chiffre d&#39;affaires attendu par client par mois**

* Mesure `A` : `Revenue (hide)`
   * `Calendar months between first order and this order` `<= X` (Choisissez un nombre raisonnable pour X, par exemple, 24 mois)
   * `Is in current month?` = `No`

* &#x200B;
  [!UICONTROL Mesure]: `Revenue`
* [!UICONTROL Filter] :

* Mesure `B` : `All time customers (hide)`
   * `Is in current month?` = `No`

* [!UICONTROL Metric] : `New customers by first order date`
* [!UICONTROL Filter] :

* Mesure `C` : `All time customers by month since first order (hide)`
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
* [!UICONTROL Group by] : `Calendar months between first order and this order` - Tout afficher
* Remplacez `group by` pour la mesure `All time customers` par Indépendant à l’aide de l’icône en forme de crayon en regard de `group by`.
* Modifiez les champs `Show top/bottom` comme suit :
   * [!UICONTROL Revenue] : `Top 24 sorted by Calendar months between first order and this order`
   * [!UICONTROL All time customers] : `Top 24 sorted by All time customers`
   * [!UICONTROL All time customers by month since first order] : `Top 24 sorted by All time customers by month since first order`

**Chiffre d’affaires moyen par mois par cohorte**

* Mesure `A` : `Revenue`
* &#x200B;
  [!UICONTROL Metric view]: `Cohort`
* [!UICONTROL Cohort date] : `Customer's first order date`
* [!UICONTROL Perspective] : `Average value per cohort member`

**Chiffre d’affaires moyen cumulé par mois par cohorte**

* Mesure `A` : `Revenue`
* &#x200B;
  [!UICONTROL Metric view]: `Cohort`
* [!UICONTROL Cohort date] : `Customer's first order date`
* [!UICONTROL Perspective] : `Cumulative average value per cohort member`

Après avoir compilé tous les rapports, vous pouvez les organiser dans le tableau de bord suivant vos besoins. Le résultat peut ressembler à l’image en haut de la page.

Si vous rencontrez des questions lors de la création de cette analyse ou si vous souhaitez simplement contacter l’équipe des services professionnels, [contactez l’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
