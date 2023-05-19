---
title: Types de colonne calculés avancés
description: Découvrez les principes de base de la plupart des cas d’utilisation des colonnes, mais vous souhaiterez peut-être que les colonnes calculées soient un peu plus complexes que ce que le Gestionnaire de Data Warehouse peut créer.
exl-id: 9871fa19-95b3-46e4-ae2d-bd7c524d12db
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 4%

---

# Types de colonne calculés avancés

De nombreuses analyses que vous souhaitez peut-être créer impliquent l’utilisation d’un **nouvelle colonne** que vous voulez `group by` ou `filter by`. Le [Création de colonnes calculées](../data-warehouse-mgr/creating-calculated-columns.md) Ce tutoriel aborde les principes de base de la plupart des cas d’utilisation, mais vous souhaiterez peut-être que la colonne calculée soit un peu plus complexe que ce que le Gestionnaire de Data Warehouse peut créer.
{ : #top}

Ces types de colonnes peuvent être créés par l’équipe Adobe des analystes de Data Warehouse. Pour définir une nouvelle colonne calculée, renseignez les informations suivantes :

1. Le **`definition`** de cette colonne (y compris les entrées, les formules ou la mise en forme)
1. Le **`table`** que vous souhaitez créer la colonne sur
1. Quelconque **`example data points`** qui décrivent ce que la colonne doit contenir

Voici quelques exemples courants de colonnes calculées avancées que les utilisateurs trouvent souvent utiles :

* [Ordre séquentiel (ou classement) de l’événement](#compareevents)
* [Rechercher l’intervalle entre deux événements](#twoevents)
* [Comparaison des valeurs d’événement séquentiel](#sequence)
* [Convertir une devise](#currency)
* [Conversion des fuseaux horaires](#timezone)
* [Quelque chose d’autre](#else)

## J’essaie de classer les événements de manière séquentielle. {#compareevents}

Cela s’appelle une **numéro de l’événement** colonne calculée. Cela signifie que vous essayez de trouver la séquence dans laquelle les événements se sont produits pour un propriétaire d’événement particulier, comme un client ou un utilisateur.

Voici un exemple :

| **`event\_id`** | **`owner\_id`** | **`timestamp`** | **`Owner's event number`** |
|-----|-----|-----|-----|
| 1 | `A` | 2015-01-01 00:00:00 | 1 |
| 2 | `B` | 2015-01-01 00:30:00 | 1 |
| 3 | `A` | 2015-01-01 02:00:00 | 2 |
| 4 | `A` | 2015-01-02 13:00:00 | 3 |
| 5 | `B` | 2015-01-03 13:00:00 | 2 |

{style="table-layout:auto"}

Une colonne calculée de numéro d’événement peut être utilisée pour observer les différences de comportement entre les premiers événements, les événements de répétition ou les énièmes événements de vos données.

Vous souhaitez que la colonne Numéro de commande du client soit en action ? Cliquez sur l’image pour l’afficher comme dimension Groupe par dans un rapport.

![Utilisation d&#39;une colonne calculée de type numéro d&#39;événement à Group By le numéro de commande du client.](../../assets/EventNumber.gif)<!--{: style="max-width: 500px;"}-->

Pour créer ce type de colonne calculée, vous devez savoir :

* Le tableau sur lequel vous souhaitez créer cette colonne
* Champ qui identifie le propriétaire des événements (`owner\_id` dans cet exemple)
* Le champ par lequel vous souhaitez classer les événements (`timestamp` dans cet exemple)

[Haut de page](#top)

## J&#39;essaie de trouver le temps entre deux événements. {#twoevents}

Cela s’appelle une `date difference` colonne calculée. Cela signifie que vous essayez de trouver l’heure entre deux événements appartenant à un seul enregistrement, en fonction des horodatages de l’événement.

Voici un exemple :

| `id` | `timestamp\_1` | `timestamp\_2` | `Seconds between timestamp\_2 and timestamp\_1` |
|-----|-----|-----|-----|
| `A` | 2015-01-01 00:00:00 | 2015-01-01 12:30:00 | 45000 |
| `B` | 2015-01-01 08:00:00 | 2015-01-01 10:00:00 | 7200 |

{style="table-layout:auto"}

Une colonne calculée de différence de date peut être utilisée pour créer une mesure qui calcule la durée moyenne ou médiane entre deux événements. Cliquez sur l’image ci-dessous pour découvrir comment la variable `Average time to first order` est utilisée dans un rapport.

![Utilisation d’une colonne calculée de différence de date pour calculer le temps moyen jusqu’au premier ordre.](../../assets/DateDifference.gif)<!--{: style="max-width: 500px;"}-->

Pour créer ce type de colonne calculée, vous devez savoir :

* Le tableau sur lequel vous souhaitez créer cette colonne
* Les deux horodatages entre lesquels vous souhaitez connaître la différence

[Haut de page](#top)

## J’essaie de comparer les valeurs d’événement séquentiel. {#sequence}

Cela s’appelle une **comparaison d’événements séquentiels**. Cela signifie que vous essayez de trouver le delta entre une valeur (devise, nombre, horodatage) et la valeur correspondante pour l’événement précédent du propriétaire.

Voici un exemple :

| **`event\_id`** | **`owner\_id`** | **`timestamp`** | **`Seconds since owner's previous event`** |
|-----|-----|-----|-----|
| 1 | `A` | 2015-01-01 00:00:00 | NULL |
| 2 | `B` | 2015-01-01 00:30:00 | NULL |
| 3 | `A` | 2015-01-01 02:00:00 | 7720 |
| 4 | `A` | 2015-01-02 13:00:00 | 126000 |
| 5 | `B` | 2015-01-03 13:00:00 | 217800 |

{style="table-layout:auto"}

Une comparaison d’événements séquentiels peut être utilisée pour trouver la durée moyenne ou médiane entre chaque événement séquentiel. Cliquez sur l’image ci-dessous pour afficher la variable **Durée moyenne et moyenne entre les commandes** mesures en action.

=![Utilisation d’une colonne calculée de comparaison d’événements séquentiels pour calculer la durée moyenne et moyenne entre les commandes.](../../assets/SeqEventComp.gif)<!--{: style="max-width: 500px;"}-->

Pour créer ce type de colonne calculée, vous devez savoir :

* Le tableau sur lequel vous souhaitez créer cette colonne
* Champ qui identifie le propriétaire des événements (`owner\_id` dans l’exemple)
* Champ de valeur dans lequel vous souhaitez voir la différence entre pour chaque événement séquentiel (`timestamp` dans cet exemple)

[Haut de page](#top)

## J&#39;essaie de convertir des devises. {#currency}

A **conversion de devise** la colonne calculée convertit les montants des transactions d’une devise enregistrée en devise de création de rapports, en fonction du taux de change au moment de l’événement.

Voici un exemple :

| **`id`** | **`timestamp`** | **`transaction\_value\_EUR`** | **`transaction\_value\_USD`** |
|-----|-----|-----|-----|
| `1` | 2015-01-01 00:00:00 | 30 | 33.57 |
| `2` | 2015-01-02 00:00:00 | 50 | 55.93 |

{style="table-layout:auto"}

Pour créer ce type de colonne calculée, vous devez savoir :

* Le tableau sur lequel vous souhaitez créer cette colonne
* Colonne du montant de la transaction que vous souhaitez convertir
* La colonne qui indique la devise dans laquelle les données ont été enregistrées (généralement un code ISO)
* Devise de création de rapports préférée

[Haut de page](#top)

## J’essaie de convertir les fuseaux horaires. {#timezone}

A **conversion de fuseau horaire** la colonne calculée convertit les horodatages d’une source de données spécifique de leur fuseau horaire enregistré en fuseau horaire de création de rapports.

Voici un exemple :

| **`id`** | **`timestamp\_UTC`** | **`timestamp\_ET`** |
|-----|-----|-----|
| `1` | 2015-01-01 00:00:00 | 2014-12-31 19:00:00 |
| `2` | 2015-01-01 12:00:00 | 2015-01-01 07:00:00 |

{style="table-layout:auto"}

Pour créer ce type de colonne calculée, vous devez savoir :

* Le tableau sur lequel vous souhaitez créer cette colonne
* La colonne d’horodatage que vous souhaitez convertir
* Le fuseau horaire dans lequel les données ont été enregistrées
* Fuseau horaire de création de rapports préféré

[Haut de page](#top)

## J&#39;essaie de faire quelque chose qui n&#39;est pas listé ici. {#else}

Ne vous inquiétez pas. Ce n&#39;est pas parce qu&#39;il n&#39;est pas répertorié ici que ce n&#39;est pas possible. L’équipe Adobe d’analystes Data Warehouse peut vous aider.

Pour définir une nouvelle colonne calculée, [envoi d’un ticket d’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) avec des détails précis sur ce que vous souhaitez créer.

## Documentation connexe

* [Créer des colonnes calculées](../data-warehouse-mgr/creating-calculated-columns.md)
* [Types de colonnes calculés](../data-warehouse-mgr/calc-column-types.md)
* [Création [!DNL Google ECommerce] dimensions avec les données de commande et de client ;](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
