---
title: Vérification de la clé hôte SSH
description: Découvrez comment Commerce Intelligence inscrit des clés d’hôte SSH, comment les actualiser, résoudre les erreurs et quand contacter le support pour les connexions au tunnel SSH.
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
source-git-commit: b51e9fceba0c62f4ef3dde340d26cd78641ef3a2
workflow-type: tm+mt
source-wordcount: 1130
ht-degree: 0%

---

# Vérification de la clé hôte SSH {#ssh-host-keys}

[!DNL Commerce Intelligence] utilise une vérification stricte de la clé hôte SSH pour les connexions de base de données chiffrées (tunnel SSH), notamment [MySQL](mysql-via-ssh-tunnel.md), [MongoDB](mongodb-via-ssh-tunnel.md) et [PostgreSQL](postgresql.md).

Pendant la **[!UICONTROL Save & Test]**, le système inscrit les clés d&#39;hôte de bastion SSH pour votre connexion et les stocke en toute sécurité par connexion. Après l’inscription, la réplication et le tunneling ne réussissent que lorsque les clés d’hôte de bastion actives correspondent aux clés inscrites.

Ce modèle améliore la sécurité en bloquant les attaques d&#39;un homme du milieu et les modifications inattendues de l&#39;hôte. Cela signifie également que la rotation des clés de l’hôte, les documents de confiance manquants ou les modifications de l’infrastructure peuvent apparaître comme des erreurs de clé de l’hôte SSH sur la connexion au lieu de défaillances de tunnel génériques.

>[!NOTE]
>
>**Administrateur** désigne un utilisateur disposant d’autorisations Administrateur sur votre compte [!DNL Commerce Intelligence], et non sur votre console d’organisation Adobe, sauf indication contraire. Seuls les administrateurs peuvent exécuter **[!UICONTROL Refresh SSH Host Keys]**. Si vous ne voyez pas ce contrôle, demandez à un administrateur de votre compte d’exécuter l’actualisation ou contactez l’assistance Adobe.

Vous ne pouvez pas modifier, charger ou gérer des fichiers `known_hosts`. L’inscription et l’actualisation s’exécutent sur l’infrastructure Adobe affectée à votre compte.

>[!IMPORTANT]
>
>La rotation de la clé de l’hôte nécessite l’exécution d’un administrateur **[!UICONTROL Refresh SSH Host Keys]**. Si des clés d’hôte de bastion ont été modifiées ou si l’identité du bastion a été modifiée (nom d’hôte, adresse IP ou port), le fait d’exécuter à nouveau **[!UICONTROL Save & Test]** ou de réenregistrer la connexion ne met pas à jour les clés inscrites. La connexion peut continuer à échouer jusqu’à ce qu’un administrateur actualise les clés de l’hôte.

## Enregistrer et tester {#save-and-test}

**[!UICONTROL Save & Test]** effectue **inscription initiale de la clé de l’hôte SSH uniquement**. Il est conservateur par défaut et ne fait pas pivoter ni ne remplace les clés déjà inscrites pour la connexion.

| État de la clé hôte inscrite | Fonctions d’enregistrement et de test |
| --- | --- |
| Les clés hôtes ne sont pas encore inscrites | **[!UICONTROL Save & Test]** analyse l&#39;hôte et le port du bastion, inscrit les clés de l&#39;hôte et les stocke pour cette connexion. |
| Les clés de l&#39;hôte sont déjà inscrites | **[!UICONTROL Save & Test]** ignore l’inscription. Il ne remplace, ne fait pas pivoter ou ne supprime pas les clés existantes inscrites, même si les clés de bastion en direct ne correspondent plus. |
| Les clés inscrites sont manquantes, vides ou non valides | **[!UICONTROL Save & Test]** ne répare pas le matériel de confiance non valide par lui-même. Un administrateur doit exécuter **[!UICONTROL Refresh SSH Host Keys]** ou contacter l’assistance si les erreurs se poursuivent |

Après une première inscription réussie, **[!UICONTROL Save & Test]** exécute ultérieurement valider les informations d’identification et les paramètres de connexion, mais laissez les clés d’hôte SSH inscrites inchangées.

## Actualiser les clés d’hôte SSH {#refresh-ssh-host-keys}

**[!UICONTROL Refresh SSH Host Keys]** met à jour les clés de l&#39;hôte SSH inscrit lorsque le bastion a changé ou lorsque le matériel de confiance doit être réparé. Un administrateur lance l’actualisation à partir de la connexion dans **[!UICONTROL Data]** > **[!UICONTROL Connections]**.

L’actualisation s’exécute de manière asynchrone sur l’infrastructure Adobe affectée à votre compte. [!DNL Commerce Intelligence] renvoie une valeur une fois l’actualisation mise en file d’attente. Il n&#39;exécute pas l&#39;analyse sur votre station de travail.

Une actualisation **réécrit** les clés d’hôte inscrites uniquement lorsque l’une de ces conditions est remplie :

* Les clés d’hôte inscrites sont manquantes
* Les clés d’hôte inscrites sont vides
* Impossible de lire les clés d&#39;hôte inscrites
* Échec de la validation des clés d’hôte inscrites
* Une nouvelle analyse renvoie des lignes de clé hôte différentes de celles des clés inscrites
* Les empreintes digitales de la numérisation et les clés inscrites ne correspondent pas

Si les clés inscrites sont à jour et valides, l’actualisation se termine sans les modifier.

>[!TIP]
>
>Exécutez **[!UICONTROL Refresh SSH Host Keys]** après que votre équipe a fait pivoter les clés d&#39;hôte SSH sur le bastion, a modifié le nom d&#39;hôte du bastion ou l&#39;adresse IP, ou a remplacé le point d&#39;entrée SSH. Patientez quelques minutes, puis exécutez **[!UICONTROL Save & Test]** pour confirmer la connexion.

## Migration de compte {#migration}

Vous ne déclenchez pas la migration du compte. Adobe effectue des déplacements de serveur de données pendant la maintenance ou la mise à l’échelle et copie les clés hôtes SSH inscrites afin que la vérification stricte continue de fonctionner après le déplacement.

Une fois qu’Adobe vous a notifié que la migration est terminée :

1. Exécutez **[!UICONTROL Save & Test]** pour confirmer la connexion. L’inscription doit être ignorée si les clés ont été copiées avec succès.
1. Si les erreurs de clé de l’hôte SSH persistent, demandez à un administrateur d’exécuter **[!UICONTROL Refresh SSH Host Keys]**, patientez quelques minutes, puis **[!UICONTROL Save & Test]**.
1. Contactez l’assistance Adobe si les erreurs se poursuivent après **[!UICONTROL Save & Test]** et jusqu’à deux tentatives de **[!UICONTROL Refresh SSH Host Keys]**.

## Messages d’erreur relatifs à la clé hôte SSH {#ssh-host-key-errors}

Le statut de la connexion affiche un seul message de clé hôte SSH convivial. Les erreurs OpenSSH brutes ne s’affichent pas dans le tableau de bord.

Le tableau suivant mappe les messages courants aux causes probables et aux étapes suivantes standard.

| Message ou statut | Ce que cela signifie | Causes possibles | Étape suivante standard |
| --- | --- | --- | --- |
| Échec de la vérification de la clé hôte SSH | La clé hôte du bastion ne correspond pas aux clés inscrites ou le matériel de confiance est inutilisable | Clés d’hôte SSH pivotées au bastion ; nom d’hôte, adresse IP ou port du bastion modifié ; clés inscrites manquantes, vides, non valides ou illisibles | Confirmez **Adresse distante** et **Port SSH**. Demandez à votre équipe d&#39;infrastructure si les clés de l&#39;hôte bastion ont changé. Demandez à un administrateur d’exécuter **[!UICONTROL Refresh SSH Host Keys]**, patientez quelques minutes, puis **[!UICONTROL Save & Test]**. |
| Impossible d&#39;inscrire les clés de l&#39;hôte SSH | **[!UICONTROL Save & Test]** n&#39;a pas pu analyser ni stocker les clés de l&#39;hôte bastion | Bastion inatteignable depuis l&#39;infrastructure Adobe ; défaillance du DNS ; pare-feu bloque les adresses IP [!DNL Commerce Intelligence] ; erreur **Adresse distante** ou **Port SSH** ; échec de l&#39;analyse de la clé hôte sur le bastion | Vérifiez la liste autorisée du pare-feu à l’aide des adresses IP [!DNL Commerce Intelligence] sur la page des informations d’identification de base de données. Confirmez que le bastion accepte le SSH sur le port configuré. Corrigez les champs de connexion et exécutez-**[!UICONTROL Save & Test]** à nouveau. |
| Les clés de l&#39;hôte SSH sont manquantes ou non valides | Une vérification stricte a bloqué le tunnel car le matériel d&#39;approbation inscrit est absent ou corrompu | Première connexion : inscription non terminée ; échec de l’actualisation préalable ; migration sans copie des clés ; problème sur l’infrastructure Adobe | Demandez à un administrateur d’exécuter **[!UICONTROL Refresh SSH Host Keys]**, puis **[!UICONTROL Save & Test]**. Contactez l’assistance technique si l’erreur persiste. |
| Impossible d&#39;actualiser les clés de l&#39;hôte SSH | L’actualisation n’a pas mis à jour les clés inscrites | Échec du réseau, du DNS ou de l’analyse lors de l’actualisation ; problème sur l’infrastructure Adobe | Patientez quelques minutes. Demandez à un administrateur de réexécuter **[!UICONTROL Refresh SSH Host Keys]** (deuxième tentative si la première a échoué). Confirmez l’accessibilité et la liste autorisée du bastion. Contactez l’assistance technique si la connexion échoue toujours après deux tentatives d’actualisation et une **[!UICONTROL Save & Test]**. |

## Liste de contrôle de dépannage {#troubleshooting}

1. Vérifiez que les paramètres **Adresse distante**, **Port SSH** et utilisateur Linux correspondent à ceux de votre bastion.
1. Vérifiez que votre pare-feu autorise les adresses IP [!DNL Commerce Intelligence] affichées sur la page des informations d’identification de la base de données.
1. Demandez à votre équipe d&#39;infrastructure si les clés de l&#39;hôte SSH sur le bastion ont changé récemment.
1. Exécutez **[!UICONTROL Save & Test]** pour valider les paramètres et inscrire les clés s’il n’en existe pas encore.
1. Demandez à un administrateur d’exécuter **[!UICONTROL Refresh SSH Host Keys]**, patientez quelques minutes, puis **[!UICONTROL Save & Test]**. Si la première actualisation ne résout pas l’erreur, répétez cette étape.
1. Si la connexion affiche toujours une erreur de clé d’hôte SSH après deux tentatives d’actualisation, cliquez sur **[!UICONTROL Contact Support]** sur la page de connexion (ou sur le canal de prise en charge de votre compte).

## Quand contacter l’assistance Adobe {#contact-support}

Contactez l’assistance technique lorsque :

* Les erreurs de clé hôte SSH continuent après qu’un administrateur s’exécute **[!UICONTROL Refresh SSH Host Keys]** deux fois et **[!UICONTROL Save & Test]** échoue toujours
* **[!UICONTROL Refresh SSH Host Keys]** ne se termine jamais ou le statut de la connexion ne change pas après 15 à 30 minutes
* Les erreurs ont commencé immédiatement après qu’Adobe vous a notifié de la migration du compte ou de la maintenance du serveur de données
* Les paramètres du bastion et la liste autorisée du pare-feu sont corrects, votre équipe n&#39;a pas fait pivoter les clés d&#39;hôte et vous ne pouvez toujours pas vous connecter
* Vous avez besoin d’un administrateur pour exécuter **[!UICONTROL Refresh SSH Host Keys]**, mais aucun administrateur n’est disponible sur le compte

Indiquez le nom de la connexion, l&#39;heure approximative de la dernière **[!UICONTROL Save & Test]** ou tentative d&#39;actualisation et si les clés de l&#39;hôte de bastion ont été modifiées récemment. N’envoyez pas de clés privées ni de phrases secrètes.

## Connexe {#related}

* [Connecter MySQL via le tunnel SSH](mysql-via-ssh-tunnel.md)
* [Connecter MongoDB via le tunnel SSH](mongodb-via-ssh-tunnel.md)
* [Connexion de PostgreSQL via le tunnel SSH](postgresql.md)
* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=fr)
