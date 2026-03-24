---
title: Utilisation de la colonne Calculée de la différence de date
description: Découvrez l’objectif et les utilisations de la colonne calculée Différence de date.
exl-id: 6ecab794-3466-4b3a-a929-3e56287522aa
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/5SElfBoU6vqCNthFdj96eCNH26dC54ucjqknnhQXQy8
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 272
ht-degree: 0%

---

# Colonne Calculée De La Différence De Date

Cette rubrique décrit l’objectif et les utilisations de la colonne calculée `Date Difference` disponible dans la page **[!DNL Manage Data > Data Warehouse]**. Vous trouverez ci-dessous une explication de son fonctionnement, suivie d’un exemple et des mécanismes de sa création.

**Explication**

Le type de colonne `Date Difference` calcule le temps entre deux événements appartenant à un seul enregistrement, en fonction des horodatages d’événement. La valeur brute calculée dans cette colonne est exprimée en secondes, mais elle est automatiquement convertie en minutes, heures, jours, etc., pour être affichée dans les rapports. Toutefois, lorsque vous l’utilisez comme filtre/regroupement par , vous devez utiliser la valeur en secondes.

Une colonne calculée `date difference` peut être utilisée pour créer une mesure qui calcule le temps moyen ou médian entre deux événements, tel que le temps moyen entre l’enregistrement du client et ses premières commandes.

**Exemple**

| **`id`** | **`timestamp_1`** | **`timestamp_2`** | **`Seconds between timestamp_2 and timestamp_1`** |
|--- |--- |--- |--- |
| `A` | 2015-01-01 00:00:00 | 2015-01-01 12:30:00 | 45000 |
| `B` | 2015-01-01 08:00:00 | 2015-01-01 10:00:00 | 7200 |

{style="table-layout:auto"}


Dans l’exemple ci-dessus, la colonne `Date Difference` est la colonne `Seconds between timestamp_2 and timestamp_1`. Il effectue les `timestamp_2 minus timestamp_1` de calcul.

**mécanique**

Les étapes suivantes décrivent comment créer une colonne `Date Difference`.

1. Accédez à la page **[!DNL Manage Data > Data Warehouse]**.
1. Accédez à la table sur laquelle vous souhaitez créer cette colonne.
1. Cliquez sur **[!UICONTROL Create a Column]** et configurez votre colonne comme suit :
   * Sélectionnez `Column Definition Type` > `Same Table`
   * Sélectionnez `Column Definition Equation` > `DATE_DIFF = (Ending DATETIME - Starting DATETIME)`
   * Sélectionnez `Ending DATETIME` colonne > Choisissez le champ de date et heure de fin, qui correspond généralement à l’événement qui se produit ultérieurement
   * Sélectionnez `Starting DATETIME` colonne ** > Choisissez le champ datetime de début, qui est généralement l’événement qui se produit plus tôt

1. Attribuez un nom à la colonne, puis cliquez sur **[!UICONTROL Save]**.
1. La colonne peut être utilisée *immédiatement*.

À titre d’exemple, l’exemple suivant est configuré pour calculer le `Seconds between order date and customer's creation date` :

![Configuration du calcul de la différence de date affichant les sélections de colonnes datetime](../../assets/date_diff.png)
