---
title: Données QuickBooks attendues
description: Découvrez comment effectuer facilement le suivi des champs de données pertinents à des fins d’analyse.
exl-id: a60996bd-e3d1-497d-abce-f02ef1444f1a
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---

# Données [!DNL QuickBooks] attendues

Une fois [que vous avez connecté votre  [!DNL QuickBooks] compte](../../../data-analyst/importing-data/integrations/quickbooks.md), vous pouvez utiliser le [Gestionnaire de Data Warehouse](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) pour facilement suivre les champs de données pertinents à des fins d’analyse. Les tableaux suivants sont créés dans votre Data Warehouse :

Pour visualiser tous les champs disponibles pour le tracking, cliquez sur les liens de la colonne du nom du tableau.

## Entités de transaction {#transactionentities}

| **Nom de la table** | **Description** |
|-----|-----|
| [`bill`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Bill) | La table `bills` contient des informations sur les transactions AP ou une demande de paiement auprès d’un tiers. Les attributs incluent le type de devise, le taux d’exchange, le montant total, la date d’échéance, le solde, etc. |
| [`billpayments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/BillPayment) | `BillPayment` Les entités sont la transaction finale de paiement des factures reçues d’un fournisseur. Ce tableau comprend les informations sur le fournisseur, le type de paiement, le montant total, la date de transaction, etc. |
| [`creditmemos`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/CreditMemo) | La table `creditmemos` enregistre les transactions qui sont des remboursements ou des crédits de paiements complets et partiels. Certains attributs incluent le nom du client, les informations de facturation et d’expédition du client, le montant et la date. |
| [`deposits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Deposit) | `Deposits` comprend les dépôts directs et les paiements client déplacés dans le compte de ressource après avoir été conservés dans le compte `Undeposited Funds`. Les attributs incluent le montant, l’ID de dépôt et la date. |
| [`estimates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Estimate) | `Estimates` sont des transactions données à des clients qui incluent des prix proposés pour un bien ou un service. Ce tableau enregistre le montant, les informations de remise, les informations sur les clients et la date. |
| [`invoices`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Invoice) | `Invoices` sont des formulaires de vente qu’un client paie ultérieurement. Le tableau des factures consigne toutes les informations de dépôt, date, éléments de ligne, informations fiscales et informations sur le client. |
| [`journalentries`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/JournalEntry) | La table `journalentries` enregistre les informations de compte AR et AP, y compris l’identifiant de l’entrée de journal, la date de transaction et les informations sur l’élément de ligne. |
| [`payments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Payment) | Un enregistrement `payment` comprend des attributs tels que l’identifiant de paiement, les montants appliqués et non appliqués, la date de transaction, le type de transaction et l’état du traitement. |
| [`purchases`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Purchase) | La table `purchases` représente vos dépenses et inclut l’identifiant d’achat, le type de paiement, le montant et toutes les informations d’article. |
| [`purchaseorders`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PurchaseOrder) | La table `purchaseorders` contient les demandes de marchandises envoyées aux fournisseurs. Ce tableau comprend les informations sur le fournisseur, l’identifiant de commande d’achat, la date de transaction, les informations sur les éléments de ligne, le montant total et les informations sur le compte AP. |
| [`refundreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/RefundReceipt) | La table `refundreceipts` enregistre les remboursements donnés aux clients. Les attributs incluent l’identifiant de reçu du remboursement, les informations sur l’article, le montant total, les informations sur les clients et le solde. |
| [`salesreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/SalesReceipt) | La table `salesreceipts` enregistre les informations dans les reçus de vente donnés aux clients, y compris l’identifiant du ticket de caisse, les informations sur l’article, le montant total, les informations sur le client, la date de transaction et les éventuels dépôts. |
| [`timeactivities`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TimeActivity) | La table `timeactivities` contient des enregistrements d’heure pour les fournisseurs et/ou les employés et inclut l’ID d’activité temporelle, les informations sur les employés/fournisseurs, l’heure consignée, la description de l’activité et la date enregistrée. |
| [`transfers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Transfer) | La table `transfers` enregistre des informations sur les fonds déplacés entre les comptes. Les attributs incluent l’ID de transfert, le montant, les informations de compte et la date. |
| [`vendorcredits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/VendorCredit) | Les crédits de fournisseur sont des transactions AP qui sont des remboursements ou des crédits accordés aux fournisseurs. La table `vendorcredits` comprend l’ID de crédit du fournisseur, les informations sur l’élément de ligne, les informations sur le fournisseur, le compte AP, le montant total et la date. |

{style="table-layout:auto"}

## Nommer les entités de liste {#namelistentities}

| **Nom de la table** | **Description** |
|-----|-----|
| [`accounts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Account) | Ce tableau comprend l’ID du compte, le nom, l’état, le type, le solde, la devise et l’heure de création. |
| [`budgets`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Budget) | Ce tableau répertorie toutes les informations relatives aux budgets de l’entreprise, notamment l’identifiant du budget, le nom, les dates de début et de fin, le type, l’état et les détails. |
| [`classes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Class) | Les classes, appliquées aux lignes de détail des transactions, vous permettent de suivre les segments qui ne sont pas liés à un client ou à un projet. Ce tableau enregistre l’ID, le nom, la sous-classe et l’état de la classe. |
| [`customers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Customer) | La table `customers` contient toutes les informations relatives à vos clients, y compris l’identifiant, le nom, les adresses de facturation et de livraison, le numéro de téléphone et l’adresse électronique du client. |
| [`departments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Department) | La table `departments` comprend l’ID, le nom et le type de service (sous-service ou service de niveau supérieur). |
| [`employees`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Employee) | La table `employees` enregistre des informations sur les personnes qui travaillent pour votre entreprise. Les attributs incluent l’ID d’employé, le nom, l’adresse, le numéro de téléphone et les informations facturables, si la société est activée sur les salaires. |
| [`items`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Item) | La table `items` contient des détails sur les produits ou services que votre entreprise vend. Ce tableau comprend l’identifiant de l’article, le nom, la description, le prix unitaire, le type, les informations d’achat, la quantité en main et les informations sur le compte de revenu et de ressource. |
| [`paymentmethods`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PaymentMethod) | La table `paymentmethods` enregistre le mode de paiement reçu pour les biens et services. Il contient l’ID, le type et le nom du paiement. |
| [`taxagencies`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxAgency) | Ce tableau contient des informations sur les agences fiscales, y compris l’ID d’agence fiscale, ainsi que des informations de suivi sur les taxes d’achat et de vente. |
| [`taxcodes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxCode) | Les codes d’imposition servent à effectuer le suivi de la situation fiscale (imposable ou non) des produits, des services et des clients. La table `taxcodes` comprend l&#39;ID, le nom, la description, l&#39;état, le statut imposable, le taux d&#39;imposition et le groupe fiscal. |
| [`taxrates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxRate) | Les taux d&#39;imposition sont utilisés pour calculer les passifs fiscaux. Ce tableau comprend l’ID du taux d’imposition, le nom, la description, le taux, l’agence fiscale, etc. |
| [`terms`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Term) | Cette entité représente les termes sous lesquels les ventes sont effectuées. Le tableau des termes comprend l’identifiant, le nom, le type, le pourcentage de remise et les jours d’échéance du terme. |
| [`vendors`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Vendor) | Le tableau vendeurs contient des informations sur les fournisseurs auprès desquels vous effectuez un achat. Les attributs de tableau comprennent l’identifiant du fournisseur, le nom de la société, le numéro de compte, le solde du compte, le statut 1099, l’adresse de facturation, le numéro de téléphone, l’adresse électronique et l’adresse web. |

{style="table-layout:auto"}

## En rapport :

* [Connexion [!DNL QuickBooks]](../integrations/quickbooks.md)
* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=fr)
