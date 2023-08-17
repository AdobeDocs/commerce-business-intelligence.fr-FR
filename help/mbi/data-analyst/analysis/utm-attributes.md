---
title: Google Analytics et attribution UTM
description: Découvrez le processus d’attribution de sources Google Analytics.
exl-id: 48b8a3d3-f1ac-4d3f-8f65-db1245c9ae0a
role: Admin, Data Architect, Data Engineer, User
feature: Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---

# [!DNL Google Analytics] et attribution UTM

Il est essentiel pour [suivi de la source d’acquisition d’utilisateurs](../../data-analyst/analysis/google-track-user-acq.md) to [identifier les campagnes publicitaires les plus performantes ;](../../data-analyst/analysis/most-value-source-channel.md). Cette rubrique explore les [!DNL Google Analytics] processus d’attribution de source. En d&#39;autres termes, à quel moment est enregistrée l&#39;information.

## Qu’est-ce que l’attribution ?

`Attribution` consiste à spécifier une source de référence d’une activité particulière. Ces activités sont généralement des macro-conversions ou des micro-conversions, macro étant des choses comme **achats**, micro-être des choses comme **inscription, inscription par email, commentaire sur un blog,** etc.

Idéalement, chaque fois qu’un événement de conversion se produit, une source de référence est enregistrée. Mais comment la source est-elle déterminée ?

En réalité, les utilisateurs proviennent souvent de nombreuses sources avant d’effectuer une micro ou une macro conversion. Par exemple, ils peuvent venir sur le site par le biais de l’option organique, puis partir, puis venir par le biais du référencement payant, puis partir, puis venir directement sur le site lui-même. Ces informations de suivi source sont souvent fournies sur le site par l’intermédiaire des paramètres UTM, mais il existe également des systèmes plus sophistiqués. Pour vos besoins, concentrez-vous sur [UTM](https://support.google.com/analytics/answer/1033867?hl=en&amp;ref_topic=1032998).

## Comment [!DNL Google Analytics] sources de référence d’attributs via les paramètres UTM ?

Lorsque les paramètres UTM sont spécifiés dans l’URL, ils sont analysés et placés dans une [!DNL Google Analytics] [cookie](https://en.wikipedia.org/wiki/HTTP_cookie). Si un site web n’a pas [!DNL Google Analytics], cela ne sert à rien d’avoir des UTM. [!DNL Google Analytics] comporte des règles sur la manière dont il traite un utilisateur qui accède à plusieurs URL avec les UTM au cours de sa vie (plus d’informations à ce sujet plus tard). En supposant que le site web soit configuré pour capturer des paramètres UTM dans une base de données externe, lorsqu’une conversion de macro ou de microdonnées se produit, quelle que soit la variable [!DNL Google Analytics] au moment de la conversion est répliqué vers la base de données.

## Premier clic ou Dernier clic

### Attribution Dernier clic

L’attribution Dernier clic est le modèle d’attribution le plus courant utilisé par [!DNL Google Analytics]. Dans ce cas, la variable [!DNL Google Analytics] représente les paramètres de la gestion dynamique des balises pour la source la plus récente avant l’événement de conversion, à savoir : [enregistré dans la base](../../data-analyst/analysis/google-track-user-acq.md). La variable [!DNL Google Analytics] Le cookie ne remplace les paramètres UTM précédents que si l’utilisateur clique sur une nouvelle URL contenant un nouvel ensemble de paramètres UTM.

Prenons l’exemple d’un utilisateur qui consulte un site web pour la première fois via [!DNL Google Analytics] *recherche payante*, puis renvoie via *référencement naturel*, puis revient au *site web directement* ou au moyen d’un *lien de l&#39;email* **sans paramètres UTM** avant l’événement de conversion. Dans cet exemple, la variable [!DNL Google Analytics] indique que la source de l’utilisateur est organique, car il s’agit de la dernière source avant la conversion. La variable *path* de l’utilisateur avant que cet événement de conversion final ne soit ignoré. Si, au lieu de cela, l’utilisateur a consulté le site web à partir d’un lien de courrier électronique avec UTM, la variable [!DNL Google Analytics] indique que la source est &quot;email&quot;. Par conséquent, s’il existe des paramètres UTM dans le cookie et que l’utilisateur y accède directement, la variable [!DNL Google Analytics] Le cookie affiche les paramètres UTM plutôt que &quot;direct&quot;.

>[!NOTE]
>
>d’un utilisateur spécifique ; [!DNL Google Analytics] les paramètres de cookie sont effacés lorsque le cookie [expires](https://developers.google.com/analytics/devguides/collection/analyticsjs/cookie-usage)ou lorsqu’un utilisateur efface ses cookies dans le navigateur.*

### Attribution du premier clic

Certains outils d’attribution payante vous permettent de capturer &quot;la pile de crêpes&quot; de sources dans le chemin d’un utilisateur. Dans ce cas, dans l’exemple ci-dessus, l’attribution du premier clic nous indiquerait le référencement payant. Certains sites web peuvent également implémenter leurs propres cookies qui capturent une pile de crêpes et stockent la première source dans leur base de données.

## Comment analyser l’attribution ?

[!DNL Google Analytics] dispose de fonctionnalités puissantes dans son interface web qui vous permet d’exécuter quatre modèles d’attribution différents :

1. premier clic
1. dernier clic
1. linéaire (diviser les recettes uniformément entre toutes les sources dans le chemin)
1. pondéré (attribution personnalisée)

Maintenant que vous comprenez quel est le modèle d’attribution pour chaque micro ou macro-conversion, la question devient &quot;Que faites-vous avec la totalité des conversions d’un utilisateur ?&quot;  Par exemple, observez les UTM enregistrés en fonction de la logique de dernier clic GA :

* Enregistrement d’utilisateur sous licence organique
* Premier achat de l’utilisateur sous recherche payante 5,00 $
* Second achat de l’utilisateur sous email 50,00 $
* Troisième achat de l’utilisateur sous 10 $ organiques

Voici où vous demandez : &quot;Combien de recettes ai-je obtenu du référencement payant ? De l&#39;email ?  Du bio ?&quot;. Vous pouvez dire que les réponses sont 5, 50 et 10 (quelle que soit la dernière source), ou vous pouvez aussi dire que vous attribuez toutes les recettes à la première source (toutes les 65 sont organiques). Vous pouvez également appliquer une analyse pondérée ou appliquer le modèle linéaire (soit environ 22 chacune).

## Documentation connexe

* [Suivi de la source de référence de commande via [!DNL Google Analytics] Commerce électronique](../importing-data/integrations/google-ecommerce.md)
* [Suivi de la source de référence des utilisateurs dans votre base de données](../analysis/google-track-user-acq.md)
* [Suivi des données de périphérique, de navigateur et de système d’exploitation utilisateur dans votre base de données](../analysis/google-track-user-acq.md)
* [Découvrez vos sources et canaux d’acquisition les plus précieux](../analysis/most-value-source-channel.md)
* [Connectez-vous à [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)
* [Augmentation du retour sur investissement de vos campagnes publicitaires](../analysis/roi-ad-camp.md)
* [Cinq bonnes pratiques pour le balisage UTM dans [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
