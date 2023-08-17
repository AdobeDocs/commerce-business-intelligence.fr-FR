---
title: Données Stripe attendues
description: Explorez les principaux tableaux de données que vous pouvez importer depuis Stripe dans Commerce Intelligence.
exl-id: 694577b2-48f9-4376-850d-acae1776afe3
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# Valeur attendue [!DNL Stripe] data

Après [vous avez connecté votre [!DNL Stripe] account](../integrations/stripe.md), vous pouvez utiliser la variable [Gestionnaire de Data Warehouse](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) pour effectuer facilement le suivi des champs de données pertinents à des fins d’analyse.

Cette rubrique explore les principaux tableaux de données à partir desquels vous pouvez importer des [!DNL Stripe] into [!DNL Commerce Intelligence]. Une fois la configuration terminée, les tableaux suivants sont créés dans votre Data Warehouse. Cliquez sur les liens de la colonne Nom du tableau pour en savoir plus sur les attributs de chaque tableau.

| **Nom de la table** | **Description** |
|-----|-----|
| [`Customers`](https://stripe.com/docs/sources/customers) | Les objets du client vous permettent d’effectuer des frais récurrents et de suivre plusieurs frais associés au même client. |
| [`Charges`](https://stripe.com/docs/payments/payment-intents/migration/charges) | Ce tableau contient des informations sur les frais liés aux cartes de crédit et de débit, notamment le montant, la devise, l’état, l’ID de client, etc. |
| [`Coupons`](https://stripe.com/docs/api/coupons/object) | Ce tableau contient des informations sur une remise de pourcentage ou de montant que vous pouvez appliquer à un client. Les coupons ne s&#39;appliquent qu&#39;aux factures, elles ne s&#39;appliquent pas aux frais ponctuels. |
| [`Invoices`](https://stripe.com/docs/billing/migration/invoice-states) | Ce tableau contient des informations sur les factures, notamment le montant dû, les abonnements, les éléments de facture, les éventuels ajustements automatiques des frais de propriété, etc. |
| [`Plans`](https://stripe.com/docs/api/plans/object) | Ce tableau contient les informations de tarification pour les différents produits et niveaux de fonctionnalités de votre site. Par exemple, vous pouvez avoir un abonnement de 10 $ par mois pour les fonctions de base et un abonnement de 20 $ par mois pour les fonctions Premium. |
| [`Subscriptions`](https://stripe.com/docs/api/subscriptions/object) | Ce tableau contient les détails des plans d’abonnement auxquels vos clients appartiennent. Les attributs incluent l’ID de client, l’état, l’annulation/la fin aux dates, le pourcentage d’impôts, les informations d’évaluation, etc. |
| [`Events`](https://stripe.com/docs/development/dashboard/events) | Les événements vous informent sur quelque chose d’intéressant qui s’est produit dans un compte. [Lorsqu’un événement intéressant se produit](https://stripe.com/docs/api/events/types), un nouvel objet d’événement est créé. Par exemple, lorsqu’une charge réussit `charge.succeeded` est créé ; ou lorsqu’une facture ne peut pas être soldée par un événement `invoice.payment\_failed` est créé. |

{style="table-layout:auto"}

>[!NOTE]
>
>De nombreuses demandes d’API peuvent entraîner la création de plusieurs événements. Par exemple, si vous créez un abonnement pour un client, vous recevez à la fois une `customer.subscription.created` et un  `charge.succeeded` .

## En rapport :

* [Connexion [!DNL Stripe]](../integrations/stripe.md)
* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
