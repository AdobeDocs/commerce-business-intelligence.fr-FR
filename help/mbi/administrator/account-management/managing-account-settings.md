---
title: Gestion des paramètres du compte
description: Découvrez comment personnaliser les paramètres de votre compte pour votre Data Warehouse.
exl-id: 847d51b1-287e-4c14-b64e-0bd9bfcccedc
role: Admin, User
feature: Accounts
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b6935462-7263-4ced-a703-60de6a5aeb2d
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
subfeature_v2:
  - id: a763c1a2-1d0a-40d7-9617-8139636fd12e
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 4e01225a6bd285afbe988b9c24e07e2ea34649fc
workflow-type: tm+mt
source-wordcount: 352
ht-degree: 0%

---

# Personnalisation des paramètres de votre compte

>[!NOTE]
>
>Nécessite des [autorisations d’administrateur.](../../administrator/user-management/user-management.md)

Dans votre compte [!DNL Commerce Intelligence], vous pouvez personnaliser les paramètres de votre compte pour votre Data Warehouse. Pour y accéder, sélectionnez le nom de votre organisation dans le coin supérieur droit de n’importe quel écran, puis choisissez **[!UICONTROL Account Settings]** dans la liste déroulante.

* **[!UICONTROL Client Name:]** Ce paramètre apparaît dans le coin supérieur droit de tous les tableaux de bord et ailleurs dans votre compte. Si vous voulez changer **[!UICONTROL "Vandelay Industries Co., Ltd]** en **[!UICONTROL "Vandelay]**, c&#39;est ici que vous devez le faire.

* **[!UICONTROL Currency:]** Il s’agit de la *devise par défaut* pour toutes les valeurs monétaires de votre compte. Chaque fois qu’une valeur décimale ou monétaire est synchronisée dans votre Data Warehouse, ce paramètre détermine le symbole placé avant cette valeur dans vos rapports.

* **[!UICONTROL Blackout Hours:]** Ce paramètre garantit que, aux heures sélectionnées de la journée, votre Data Warehouse n’accède pas à vos bases de données connectées. Toutes les heures sont exprimées à zéro heure et en heure standard de l&#39;Est (EST). Par exemple, si vous ne souhaitez pas que votre base de données de production soit accessible entre 9:0000 EST et 13:00 EST, vous devez saisir le tableau de chiffres suivant : **9, 10, 11, 12**.

* **[!UICONTROL Forced update hours:]** Ce paramètre garantit qu’une mise à jour Data Warehouse commence automatiquement dans votre compte *au cours des heures* que vous avez spécifiées. Comme pour les heures d&#39;arrêt de la surveillance, elles sont également en ET. Par exemple, si vous souhaitez que les mises à jour de Data Warehouse commencent automatiquement à **minuit** et **midi** EST, vous devez saisir le tableau de chiffres suivant : **0, 12**.

* **[!UICONTROL Send email summaries if the data has not updated yet:]** Cette option gère les situations dans lesquelles l’envoi d’un résumé d’e-mail est planifié *avant l’actualisation des données d’un de ses rapports*. Si vous choisissez **Non**, votre compte ignore l’envoi de l’e-mail à l’heure prévue. Au lieu de cela, votre compte l’envoie une fois que vos données ont été mises à jour. Si vous choisissez **[!UICONTROL Yes]**, votre compte envoie l’e-mail, inclut un message expliquant que les données sont obsolètes et envoie un autre e-mail une fois que vos données ont été mises à jour.

* **[!UICONTROL Enable data updates:]** Cette option garantit que les mises à jour de données s’exécutent sur votre compte. Si vous définissez le paramètre sur **[!UICONTROL No]**, les synchronisations des données et les calculs des colonnes sont interrompus dans votre compte.

>[!NOTE]
>
>Veillez à sélectionner **[!UICONTROL Save Customizations]** après avoir effectué les modifications.
