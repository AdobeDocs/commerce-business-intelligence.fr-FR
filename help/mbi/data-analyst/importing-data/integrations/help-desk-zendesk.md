---
title: Rapports du centre d’aide pour Zendesk
description: Découvrez les canaux de référence les plus précieux.
exl-id: b6142ef2-2be8-401f-ac35-f86fc68d204e
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# Rapports du service d’assistance pour [!DNL Zendesk]

>[!NOTE]
>
>Cette option n’est disponible que pour les clients qui se trouvent sur la variable `Pro` planifiez et utilisez la nouvelle architecture. Vous utilisez la nouvelle architecture si vous avez le `Data Warehouse Views` section disponible après sélection `Manage Data` dans la barre d’outils principale.

Consolidation de votre [!DNL Zendesk] les données de votre base de données transactionnelle sont un excellent moyen de mieux comprendre comment vos clients interagissent avec vos équipes de vente ou de succès client. Il vous aide également à déterminer le type de clients qui utilisent votre plateforme d’assistance. Cette rubrique explique comment configurer un tableau de bord pour obtenir des rapports détaillés sur votre [!DNL Zendesk] les performances et l’association avec vos clients transactionnels.

Avant de commencer, vous souhaitez connecter votre [[!DNL Zendesk]](../integrations/zendesk.md). Cette analyse contient [colonnes calculées avancées](../../data-warehouse-mgr/adv-calc-columns.md).

<!-- Getting Started -->

## Prise en main

### Colonnes à suivre

* `audits` table
* `_id`
* `created_at`
* `id`
* `ticket_id`
* `_updated_at`

* `audits_~_events` table
* `_sub_id`
* `_id_of_parent`
* `author_id`
* `field_name`
* `public`
* `type`
* `value`

* `tickets` table
* `_id`
* `assignee_id`
* `created_at`
* `id`
* `requester_id`
* `status`
* `updated_at`
* `via_~_source_~_from_~_address`
* `_updated_at`

* `users` table
* `_id`
* `created_at`
* `emails`
* `id`
* `role`
* `updated_at`
* `_updated_at`

### Filtrer les ensembles à créer

* `[!DNL Zendesk] Tickets` table
   * `status != deleted`

* `Filter set name`: `Tickets we count`
* `Filter set logic`:

## Colonnes calculées

### Colonnes à créer

* **`[!DNL Zendesk] user's`** table
   * `User is agent? (Yes/No) `
   * 
      * `Column type` - `Same Table > Calculation`

      * `Input columns` - `role`, `email`

      * `SQL Calculation` `- case when `A` is not `null` and `A !=`end-user` then `Yes` when `B` n’est pas `null` et `B` like `%@magento.com` then `Yes` else `No` end

      * Remplacer `@magento.com` avec votre domaine

      * `Datatype` - `String`

* **`[!DNL Zendesk] audits_~_events`** table
   * Sélectionnez une définition : `Joined Column`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] audits_~_events.author_id8`
   * [!UICONTROL One]: `[!DNL Zendesk] users.id`

   * Sélectionnez une [!UICONTROL table]: `[!DNL Zendesk] users`
   * Sélectionnez une [!UICONTROL column]: `User is agent? (Yes/No)`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events.author_id = [!DNL Zendesk] users.id`

* **`Author is agent? (Yes/No)`**

* **`[!DNL Zendesk] audits`** table
   * Sélectionnez une définition : `Exists`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] audits_~_events._id_of_parent`
   * [!UICONTROL One]: `[!DNL Zendesk] audits._id`

   * Sélectionnez une [!UICONTROL table]: `[!DNL Zendesk] audits_~_events`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events._id_of_parent = [!DNL Zendesk] audits._id`
   * [!UICONTROL Filter]:
   * `field_name` = `status`
   * `type` = `Change`
   * `value` = `solved`

   * Sélectionnez une définition : `Exists`
   * Sélectionnez une [!UICONTROL table]: `[!DNL Zendesk] audits_~_events`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events._id_of_parent = [!DNL Zendesk] audits._id`
   * [!UICONTROL Filter]: `Author is agent? (Yes/No)`
   * `type` = `Comment`
   * `public` = `1`

* **`Status changes to solved? (1/0)`**
* **`Is agent comment? (1/0)`**

* **`[!DNL Zendesk] Tickets`** table
   * Sélectionnez une définition : `Joined Column`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] tickets.requester_id`
   * [!UICONTROL One]: `[!DNL Zendesk] users.id`

   * Sélectionnez une [!UICONTROL table]: `[!DNL Zendesk] users`
   * Sélectionnez une [!UICONTROL column]: `email`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.requester_id = [!DNL Zendesk] users.id`

   * Sélectionnez une définition : `Joined Column`
   * Sélectionnez une [!UICONTROL table]: `[!DNL Zendesk] users`
   * Sélectionnez une [!UICONTROL column]: `role`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.requester_id = [!DNL Zendesk] users.id`

   * Sélectionnez une définition : `Max`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] audits.ticket_id`
   * [!UICONTROL One]: `[!DNL Zendesk] tickets.id`

   * Sélectionnez une [!UICONTROL table]: `[!DNL Zendesk] audits`
   * Sélectionnez une [!UICONTROL column]: `created_at`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits.ticket_id = [!DNL Zendesk] tickets.id`
   * [!UICONTROL Filter]:
   * `status` a été remplacé par `solved = 1`

   * Sélectionnez une définition : `Min`
   * Sélectionnez une [!UICONTROL table]: `[!DNL Zendesk] audits`
   * Sélectionnez une [!UICONTROL column]: `created_at`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits.ticket_id = [!DNL Zendesk] tickets.id`
   * [!UICONTROL Filter]:
   * `Is agent comment? = 1`

* `Requester's email`
* `Requester's role`
* `Ticket's latest solved date`
* `First agent response date`
* `Seconds to resolution`
   * 
      * `Column type` - `Same Table > Date Difference`

      * `Ticket's latest solved date` moins `created_at`

* **`Seconds to first response`**
   * 
      * `Column type` - `Same Table > Date Difference`

      * `First agent response date` moins `created_at`

* **`Requester's ticket number`**
   * 
      * `Column type` - `Same Table > Event Number`

      * `Event Owner` - `requester_id`

      * `Event Rank` - `created_at`

* **`Ticket created_at (hour of day)`**
   * 
      * `Column type` - &quot;Même tableau > Calcul&quot;

      * `Input columns` - `created_at`

      * `SQL Calculation` - `to_char(A,'HH24')::int`

      * `Datatype` - Entier

* **`Ticket created_at (day of week)`**
   * 
      * `Column type` - &quot;Même tableau > Calcul&quot;

      * `Input columns` - `created_at`

      * `Calculation` - `to_char(A,'D')||'. '||to_char(A,'Day')`

     *`Datatype` – `String`

* **`customer_entity`** table
   * Sélectionnez une définition : `Count`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] tickets.email`
   * 
     [!UICONTROL One]: `customer_entity.email`

   * Sélectionnez une [!UICONTROL table]: `[!DNL Zendesk] tickets`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.email = customer_entity.email`
   * [!UICONTROL Filter]:
   * `Tickets we count`

* **`User's lifetime number of support tickets requested`**
* **`Has user filed a support ticket? (Yes/No)`**
   * 
      * `Column type` - &quot;Même tableau > Calcul&quot;

      * `Input columns` - `User's lifetime number of support tickets requested`

      * `Calculation` - `case when A>0 then 'Yes' else 'No' end`

      * `Datatype` – `String`

* **`[!DNL Zendesk] Tickets`** table
   * Sélectionnez une définition : `Joined Column`
   * Sélectionnez une [!UICONTROL table]: `customer_entity`
   * Sélectionnez une [!UICONTROL column]: `User's lifetime number of support tickets requested`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.email = customer_entity.email`

* **`Requester's lifetime number of support tickets`**

## Mesures

* **[!DNL Zendesk]Nouveaux tickets**
   * `Tickets we count`

* Dans le **`[!DNL Zendesk] tickets`** table
* Cette mesure effectue une **Count**
* Sur le **`id`** column
* Commandé par le **`created_at`** timestamp
* [!UICONTROL Filter]:

* **[!DNL Zendesk]billets soldés**
   * `Tickets we count`
   * status IN `closed, solved`

* Dans le **`[!DNL Zendesk] tickets`** table
* Cette mesure effectue une **Count**
* Sur le **`id`** column
* Commandé par le **`created_at`** timestamp
* [!UICONTROL Filter]:

* **[!DNL Zendesk]Classement de tickets par les utilisateurs distincts**
   * `Tickets we count`

* Dans le **`[!DNL Zendesk] tickets`** table
* Cette mesure effectue une **Comptage distinct**
* Sur le **`requester_id`** column
* Commandé par le **`created_at`** timestamp
* [!UICONTROL Filter]:

* **[!DNL Zendesk]Durée moyenne/médiane de résolution du ticket**
   * `Tickets we count`
   * status IN `closed, solved`

* Dans le **`[!DNL Zendesk] tickets`** table
* Cette mesure effectue une **Moyenne (ou médiane)**
* Sur le **`Seconds to resolution`** column
* Commandé par le **`created_at`** timestamp
* [!UICONTROL Filter]:

* **[!DNL Zendesk]Temps moyen/médian jusqu’à la première réponse**
   * Billets comptabilisés
   * statut EN fermé, résolu

* Dans le **`[!DNL Zendesk] tickets`** table
* Cette mesure effectue une **Moyenne (ou médiane)**
* Sur le **`Seconds to first response`** column
* Commandé par le **`created_at`** timestamp
* [!UICONTROL Filter]:

>[!NOTE]
>
>Veillez à [ajouter toutes les nouvelles colonnes en tant que dimensions aux mesures ;](../../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) avant de créer de nouveaux rapports.

### Rapports

* **[!UICONTROL New/Open/Pending tickets]**
   * [!UICONTROL Metric]: `New Tickets`
   * [!UICONTROL Filter]:
   * status IN `new, open, pending`

* Mesure `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Closed/Solved tickets]**
   * [!UICONTROL Metric]: `New Tickets`
   * [!UICONTROL Filter]:
   * status IN `solved, closed`

* Mesure `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Average time to first response]**
   * [!UICONTROL Metric]: `Average time to first response`

* Mesure `A`: `Average time to first response`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Average time to resolution]**
   * [!UICONTROL Metric]: `Average time to resolution`
   * [!UICONTROL Filter]:
   * status IN `solved, closed`

* Mesure `A`: `Average time to resolution`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Tickets by status]**
   * [!UICONTROL Metric]: `New Tickets`

* Mesure `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `status`
* `Chart Type`: `Stacked Column`

* **[!UICONTROL Number of new and solved tickets]**
   * [!UICONTROL Metric]: `New Tickets`

   * [!UICONTROL Metric]: `New Tickets`

* Mesure `A`: `New tickets`
* Mesure `B`: `Solved tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Line`

* **[!UICONTROL Time to first response]**
   * [!UICONTROL Metric]: `Average time to first response`

* Mesure `A`: `Average time to first response`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Time to resolution]**
   * [!UICONTROL Metric]: `Average time to resolution`
   * [!UICONTROL Filter]:
   * status IN `solved, closed`

* Mesure `A`: `Average time to resolution`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Distinct users filing tickets]**
   * [!UICONTROL Metric]: `Distinct users filing tickets`

* Mesure `A`: `Distinct users filing tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Peak ticket days]**
   * [!UICONTROL Metric]: `New Tickets`

* Mesure `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Group by`: `Ticket created_at (day of week)`
* `Chart Type`: `Pie`

* **[!UICONTROL Peak ticket hours]**
   * [!UICONTROL Metric]:`New Tickets`

   * `Show top/bottom`: `Top 100% sorted by created_at (hour of the day)`

* Mesure `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Group by`: `Ticket created_at (hour of the day)`
* `Chart Type`: `Pie`

* **[!UICONTROL Avg LTV of users who have and have not filed tickets]**
   * [!UICONTROL Metric]: `Average lifetime revenue`

* Mesure `A`: `Average lifetime revenue`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `User has filed a support ticket?`
* `Chart Type`: `Column`

* **[!UICONTROL Number of new users who have and have not filed tickets]**
   * 
     [!UICONTROL Mesure]: Users

* Mesure `A`: `New users`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `User has filed a support ticket?`
* `Chart Type`: `Column`
