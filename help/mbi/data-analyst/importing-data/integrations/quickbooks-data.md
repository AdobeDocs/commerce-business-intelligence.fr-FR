---
title: Données QuickBooks attendues
description: Découvrez comment effectuer facilement le suivi des champs de données pertinents pour l’analyse.
exl-id: a60996bd-e3d1-497d-abce-f02ef1444f1a
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/aMWa4wHUfzDfBSSRKAkqqnYBEp481pfULZjJJpbe-oI
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
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
source-wordcount: 796
ht-degree: 0%

---

# Données de [!DNL QuickBooks] attendues

Une fois [vous avez connecté votre [!DNL QuickBooks] compte](../../../data-analyst/importing-data/integrations/quickbooks.md), vous pouvez utiliser le [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) pour effectuer facilement le suivi des champs de données pertinents à analyser. Les tableaux ci-dessous sont créés dans votre Data Warehouse :

Pour visualiser tous les champs disponibles pour le tracking, cliquez sur les liens dans la colonne du nom de la table.

## Entités de transaction {#transactionentities}

| **Nom de la table** | **Description** |
|-----|-----|
| [`bill`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Bill) | La table `bills` contient des informations sur les transactions AP ou une demande de paiement d&#39;un tiers. Les attributs incluent le type de devise, le taux de change, le montant total, la date d’échéance, le solde, etc. |
| [`billpayments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/BillPayment) | Les entités `BillPayment` sont la transaction finale de paiement des factures reçues d&#39;un fournisseur. Ce tableau inclut les informations sur le fournisseur, le type de paiement, le montant total, la date de transaction, etc. |
| [`creditmemos`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/CreditMemo) | La table `creditmemos` enregistre les mouvements qui sont des remboursements ou des crédits de paiements complets et partiels. Certains attributs incluent le nom du client, les informations de facturation et d’expédition du client, le montant et la date. |
| [`deposits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Deposit) | Les `Deposits` incluent les dépôts directs et les paiements des clients transférés dans le compte d’actifs après avoir été détenus dans le compte d’`Undeposited Funds`. Les attributs incluent le montant, l’ID de dépôt et la date. |
| [`estimates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Estimate) | `Estimates` sont des transactions données à des clients qui incluent une proposition de prix pour un bien ou un service. Ce tableau enregistre le montant, les informations sur la remise, les informations client et la date. |
| [`invoices`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Invoice) | `Invoices` sont des formulaires de vente qu’un client paie ultérieurement. Le tableau des factures enregistre toutes les informations sur les acomptes, les dates, les lignes, les taxes et les clients. |
| [`journalentries`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/JournalEntry) | La table `journalentries` enregistre les informations sur les comptes AR et AP, y compris l&#39;ID de pièce, la date de transaction et les informations sur les lignes. |
| [`payments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Payment) | Un enregistrement `payment` inclut des attributs tels que l&#39;ID paiement, les montants lettrés et non lettrés, la date de transaction, le type de transaction et le statut de traitement. |
| [`purchases`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Purchase) | Le tableau `purchases` représente vos dépenses et inclut l’identifiant d’achat, le type de paiement, le montant et toute information sur les lignes. |
| [`purchaseorders`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PurchaseOrder) | La table `purchaseorders` contient les demandes de marchandises envoyées aux fournisseurs. Ce tableau inclut les informations sur le fournisseur, l&#39;ID de commande fournisseur, la date de transaction, les informations sur les lignes, le montant total et les informations sur le compte AP. |
| [`refundreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/RefundReceipt) | La table `refundreceipts` enregistre les remboursements accordés aux clients. Les attributs incluent l&#39;ID de réception de remboursement, les informations sur les lignes, le montant total, les informations sur le client et le solde. |
| [`salesreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/SalesReceipt) | La table `salesreceipts` enregistre des informations dans les réceptions de vente remises aux clients, y compris l&#39;identifiant de réception de vente, les informations sur les lignes, le montant total, les informations client, la date de transaction et les éventuels acomptes. |
| [`timeactivities`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TimeActivity) | La table `timeactivities` contient des enregistrements de temps pour les fournisseurs et/ou les employés et inclut l&#39;ID d&#39;activité de temps, les informations sur les employés/fournisseurs, le temps enregistré, la description de l&#39;activité et la date enregistrée. |
| [`transfers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Transfer) | Le tableau `transfers` enregistre des informations sur les fonds transférés entre les comptes. Les attributs incluent l’ID de transfert, le montant, les informations de compte et la date. |
| [`vendorcredits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/VendorCredit) | Les crédits fournisseur sont des transactions AP qui sont des remboursements ou des crédits accordés aux fournisseurs. Le tableau `vendorcredits` inclut l&#39;ID crédit fournisseur, les informations sur les lignes, les informations fournisseur, le compte AP, le montant total et la date. |

{style="table-layout:auto"}

## Nommer les entités de liste {#namelistentities}

| **Nom de la table** | **Description** |
|-----|-----|
| [`accounts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Account) | Ce tableau comprend l’identifiant du compte, le nom, le statut, le type, le solde, la devise et l’heure de création. |
| [`budgets`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Budget) | Ce tableau enregistre toutes les informations relatives aux budgets d&#39;entreprise, y compris l&#39;identifiant du budget, le nom, les dates de début et de fin, le type, le statut et les détails. |
| [`classes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Class) | Les classes, appliquées aux lignes de détail des transactions, vous permettent d’effectuer le suivi des segments qui ne sont pas liés à un client ou à un projet. Ce tableau enregistre l’ID de classe, le nom, la sous-classe et le statut. |
| [`customers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Customer) | La table `customers` contient toutes les informations relatives à vos clients, y compris l’identifiant, le nom, les adresses de facturation et d’expédition, le numéro de téléphone et l’adresse e-mail du client. |
| [`departments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Department) | Le tableau `departments` comprend l&#39;ID, le nom et le type du service (sous-service ou service de niveau supérieur). |
| [`employees`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Employee) | La table `employees` enregistre des informations sur les personnes qui travaillent pour votre société. Les attributs comprennent l&#39;ID employé, le nom, l&#39;adresse, le numéro de téléphone et les informations facturables, si la société est compatible avec la paie. |
| [`items`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Item) | Le tableau `items` contient des détails sur les produits ou services vendus par votre société. Ce tableau comprend l&#39;ID article, le nom, la description, le prix unitaire, le type, les informations d&#39;achat, la quantité en stock et les informations sur le compte de résultat et d&#39;actif. |
| [`paymentmethods`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PaymentMethod) | Le tableau `paymentmethods` enregistre le mode de paiement reçu pour les biens et services. Il contient l&#39;ID paiement, le type et le nom. |
| [`taxagencies`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxAgency) | Cette table enregistre des informations sur les agences fiscales, y compris l&#39;ID d&#39;agence fiscale, et des informations de suivi sur les taxes pour les achats et les ventes. |
| [`taxcodes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxCode) | Les codes taxe sont utilisés pour effectuer le suivi du statut de taxe (imposable ou non) des produits, services et clients. Le tableau `taxcodes` inclut l&#39;ID code taxe, le nom, la description, le statut, le statut de taxe, le taux de taxe et le groupe de taxe. |
| [`taxrates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxRate) | Les taux d’imposition sont utilisés pour calculer les impôts à payer. Ce tableau comprend l&#39;identifiant du taux de taxe, le nom, la description, le taux, l&#39;agence fiscale, etc. |
| [`terms`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Term) | Cette entité représente les conditions dans lesquelles les ventes sont effectuées. Le tableau des termes comprend l’ID du terme, le nom, le type, le pourcentage de remise et les jours d’échéance. |
| [`vendors`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Vendor) | Le tableau des fournisseurs contient des informations sur les fournisseurs auprès desquels vous effectuez des achats. Les attributs du tableau incluent l&#39;ID fournisseur, le nom de la société, le numéro de compte, le solde du compte, le statut 1099, l&#39;adresse de facturation, le numéro de téléphone, l&#39;adresse e-mail et l&#39;adresse Web. |

{style="table-layout:auto"}

## Connexe :

* [Connexion  [!DNL QuickBooks]](../integrations/quickbooks.md)
* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
