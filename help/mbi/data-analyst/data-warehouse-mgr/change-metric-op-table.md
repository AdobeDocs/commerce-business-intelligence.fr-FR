---
title: Modification du tableau opérationnel d’une mesure
description: Découvrez comment modifier le tableau de données utilisé par une mesure pour effectuer son fonctionnement.
exl-id: c7a074ca-31f4-43e5-85d9-b64dca95dc23
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# Modification du tableau opérationnel d’une mesure

Dans certains cas, vous pouvez décider de modifier le tableau de données utilisé par une mesure pour effectuer son opération. Par exemple, si vous disposez d’un nouveau tableau Utilisateurs, vous souhaitez migrer les mesures liées aux utilisateurs de la table &quot;Utilisateurs\_Ancien&quot; afin d’utiliser plutôt le tableau &quot;Utilisateurs\_Nouveaux&quot;.

1. Accédez à **[!UICONTROL Data]** > **[!UICONTROL Metrics]**
1. Cliquez sur **[!UICONTROL Edit]** en regard de la mesure pour laquelle vous souhaitez changer le `operational` table.
1. Dans l’éditeur, cliquez sur **[!UICONTROL Change]**.

   ![](../../assets/change-metrics-1.png)
1. Sélectionnez maintenant le nouveau tableau sur lequel vous souhaitez baser cette mesure.
1. Ensuite, vous devez faire correspondre les dimensions de données existantes à celles correspondantes dans le nouveau tableau. Par exemple, si vous aviez une colonne appelée `User's registration date`, sélectionnez simplement la colonne du nouveau tableau qui enregistre les mêmes données de date. (Voir l’étape suivante si le nouveau tableau ne contient pas de colonnes correspondantes)

   ![](../../assets/change-metrics-2.png)

1. Si le nouveau tableau ne contient pas de colonne correspondante, vous pouvez effectuer l’une des opérations suivantes : **créez-le dans votre tableau de données** ou [support technique](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) s’il s’agit d’une colonne de calcul ou d’une dimension effectuée par [!DNL MBI]). Vous pouvez également **supprimer la dimension de la mesure ;**. Pour supprimer une dimension dont vous n’avez plus besoin, revenez simplement à l’éditeur de mesures et sélectionnez les dimensions à supprimer sous . `Dimensions`.

   ![](../../assets/change-metrics-3.png)
