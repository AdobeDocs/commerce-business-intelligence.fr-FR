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

# Personnalisation des paramètres du compte

>[!NOTE]
>
>Nécessite [Autorisations d’administrateur.](../../administrator/user-management/user-management.md)

Dans votre compte [!DNL Commerce Intelligence], vous pouvez personnaliser les paramètres de votre compte pour votre Data Warehouse. Pour y accéder, sélectionnez le nom de votre organisation dans le coin supérieur droit de n’importe quel écran, puis sélectionnez **[!UICONTROL Account Settings]** dans la liste déroulante.

* **[!UICONTROL Client Name:]** Ce paramètre s’affiche dans le coin supérieur droit de tous les tableaux de bord et ailleurs dans votre compte. Si vous souhaitez remplacer **[!UICONTROL "Vandelay Industries Co., Ltd]** par **[!UICONTROL "Vandelay]**, voici où procéder.

* **[!UICONTROL Currency:]** Il s’agit de la *devise par défaut* pour toutes les valeurs monétaires de votre compte. Chaque fois qu’une valeur décimale ou monétaire est synchronisée dans votre Data Warehouse, ce paramètre détermine le symbole placé avant cette valeur dans vos rapports.

* **[!UICONTROL Blackout Hours:]** Ce paramètre garantit que, aux heures sélectionnées de la journée, votre Data Warehouse n’accède pas à vos bases de données connectées. Toutes les heures sont exprimées à zéro heure et en heure normale de l’Est (heure de l’Est). Par exemple, si vous ne souhaitez pas que l’accès à votre base de données de production se fasse entre 9h00 HNE et 13h00 HNE, saisissez le tableau de chiffres suivant : **9, 10, 11, 12**.

* **[!UICONTROL Forced update hours:]** Ce paramètre garantit qu&#39;une mise à jour de Data Warehouse commence automatiquement dans votre compte *pendant les heures* que vous avez spécifiées. Comme pour les heures de blackout, ils sont aussi en ET. Par exemple, si vous souhaitez que les mises à jour de Data Warehouse commencent automatiquement à **minuit** et **midi** EST, vous devez saisir le tableau de chiffres suivant : **0, 12**.

* **[!UICONTROL Send email summaries if the data has not updated yet:]** Cette option gère les situations lorsqu’un résumé d’email est programmé pour envoyer *avant que les données de l’un de ses rapports* ne soient actualisées. Si vous choisissez **Non**, votre compte ignore l’envoi de l’email à l’heure planifiée. À la place, votre compte l’envoie une fois vos données mises à jour. Si vous choisissez **[!UICONTROL Yes]**, votre compte envoie le courrier électronique, inclut un message expliquant que les données sont obsolètes et envoie un autre courrier électronique une fois vos données mises à jour.

* **[!UICONTROL Enable data updates:]** Cette option garantit que les mises à jour de données s’exécutent sur votre compte. Si vous définissez le paramètre sur **[!UICONTROL No]**, les synchronisations des données et les calculs des colonnes s’arrêtent dans votre compte.

>[!NOTE]
>
>Veillez à sélectionner **[!UICONTROL Save Customizations]** après avoir apporté des modifications.
