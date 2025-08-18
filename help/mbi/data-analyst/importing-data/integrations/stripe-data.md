---
title: Données Stripe attendues
description: Explorez les principaux tableaux de données que vous pouvez importer de Stripe dans Commerce Intelligence.
exl-id: 694577b2-48f9-4376-850d-acae1776afe3
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '323'
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
