---
title: Gestion des paramètres du compte
description: Découvrez comment personnaliser les paramètres de votre compte pour votre Data Warehouse.
exl-id: 847d51b1-287e-4c14-b64e-0bd9bfcccedc
role: Admin, User
feature: Accounts
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '349'
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
