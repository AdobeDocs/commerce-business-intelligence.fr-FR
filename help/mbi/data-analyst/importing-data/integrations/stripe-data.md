---
title: Données Stripe attendues
description: Explorez les principaux tableaux de données que vous pouvez importer de Stripe dans Commerce Intelligence.
exl-id: 694577b2-48f9-4376-850d-acae1776afe3
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/dCiDusso9q9gvZOXKeHcDcuVK-jCXkqR3pQg6eTKzdo
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 323
ht-degree: 0%

---

# Données de [!DNL Stripe] attendues

Une fois [vous avez connecté votre [!DNL Stripe] compte](../integrations/stripe.md), vous pouvez utiliser le [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) pour effectuer facilement le suivi des champs de données pertinents à analyser.

Cette rubrique explore les principaux tableaux de données que vous pouvez importer depuis [!DNL Stripe] vers [!DNL Commerce Intelligence]. Une fois la configuration terminée, les tableaux suivants seront créés dans votre Data Warehouse. Cliquez sur les liens de la colonne Nom de la table pour en savoir plus sur les attributs de chaque table.

| **Nom de la table** | **Description** |
|-----|-----|
| [`Customers`](https://stripe.com/docs/sources/customers) | Les objets client vous permettent d’effectuer des frais récurrents et de suivre plusieurs frais associés à un même client. |
| [`Charges`](https://stripe.com/docs/payments/payment-intents/migration/charges) | Ce tableau contient des informations sur les frais facturés aux cartes de crédit et de débit, notamment le montant, la devise, le statut, l’ID client, etc. |
| [`Coupons`](https://stripe.com/docs/api/coupons/object) | Ce tableau contient des informations sur un pourcentage ou un montant de remise que vous pouvez appliquer à un client. Les coupons s&#39;appliquent uniquement aux factures ; ils ne s&#39;appliquent pas aux frais ponctuels. |
| [`Invoices`](https://stripe.com/docs/billing/migration/invoice-states) | Ce tableau contient des informations sur les factures, notamment le montant dû, les abonnements, les éléments de facture, les ajustements automatiques de calcul au prorata, etc. |
| [`Plans`](https://stripe.com/docs/api/plans/object) | Ce tableau contient les informations sur les prix des différents produits et niveaux de fonctionnalité de votre site. Par exemple, vous pouvez avoir un plan de 10 $/mois pour les fonctionnalités de base et un plan de 20 $/mois pour les fonctionnalités premium. |
| [`Subscriptions`](https://stripe.com/docs/api/subscriptions/object) | Ce tableau contient les détails des abonnements auxquels vos clients appartiennent. Les attributs incluent l&#39;ID client, le statut, les dates d&#39;annulation/de fin, le pourcentage de taxe, des informations d&#39;évaluation, etc. |
| [`Events`](https://stripe.com/docs/development/dashboard/events) | Les événements vous informent d’un événement intéressant qui s’est produit sur un compte. [Lorsqu’un événement intéressant se produit](https://stripe.com/docs/api/events/types), un nouvel objet d’événement est créé. Par exemple, lorsqu’une imputation réussit `charge.succeeded` création d’un événement, ou lorsqu’une facture ne peut pas être payée, un événement `invoice.payment\_failed` est créé. |

{style="table-layout:auto"}

>[!NOTE]
>
>De nombreuses requêtes d’API peuvent entraîner la création de plusieurs événements. Par exemple, si vous créez un abonnement pour un client, vous recevez à la fois un événement `customer.subscription.created` et un événement `charge.succeeded`.

## Connexe :

* [Connexion  [!DNL Stripe]](../integrations/stripe.md)
* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=fr)
