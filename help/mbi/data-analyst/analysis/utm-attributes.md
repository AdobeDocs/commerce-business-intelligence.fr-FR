---
title: Google Analytics et attribution UTM
description: Découvrez le processus d’attribution de sources Google Analytics.
exl-id: 48b8a3d3-f1ac-4d3f-8f65-db1245c9ae0a
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 0%

---

# Google Analytics et attribution UTM

Il est essentiel pour [suivi de la source d’acquisition d’utilisateurs](../../data-analyst/analysis/google-track-user-acq.md) to [identifier les campagnes publicitaires les plus performantes ;](../../data-analyst/analysis/most-value-source-channel.md). Dans ce tutoriel, nous explorons le processus d’attribution de sources Google Analytics. En d&#39;autres termes, à quel moment est enregistrée l&#39;information.

## Qu’est-ce que l’attribution ?

`Attribution` consiste à spécifier une source de référence d’une activité particulière. Ces activités sont généralement des macro-conversions ou des micro-conversions, macro étant des choses comme **achats**, micro-être des choses comme **inscription, inscription par email, commentaire sur un blog,** etc.

Idéalement, chaque fois qu’un événement de conversion se produit, une source de référence est enregistrée. Mais comment la source est-elle déterminée ?

La réalité est que les utilisateurs proviennent souvent de nombreuses sources avant d’effectuer une micro ou macro conversion (par exemple, ils peuvent venir sur le site par le biais de l’option organique, puis partir, puis effectuer un référencement payant, puis partir, puis se rendre directement sur le site lui-même). Ces informations de suivi source sont souvent fournies sur le site par l’intermédiaire des paramètres UTM, mais il existe également des systèmes plus sophistiqués. À nos fins, nous nous concentrerons sur [UTM](https://support.google.com/analytics/answer/1033867?hl=en&amp;ref_topic=1032998).

## Comment [!DNL Google Analytics] sources de référence d’attributs via les paramètres UTM ?

Lorsque les paramètres de la gestion dynamique des balises sont spécifiés dans l’URL, ils sont analysés et placés dans une [!DNL Google Analytics] [cookie](https://en.wikipedia.org/wiki/HTTP_cookie). Si un site web n’a pas [!DNL Google Analytics], cela ne sert à rien d’avoir des UTM. [!DNL Google Analytics] comporte des règles sur la manière dont il traite un utilisateur qui accède à plusieurs URL avec des UTM au cours de sa vie (plus d’informations à ce sujet plus tard). En supposant que le site web soit configuré pour capturer des paramètres UTM dans une base de données externe, chaque fois qu’une conversion de macro ou de microdonnées se produit, quelle que soit la variable [!DNL Google Analytics] au moment de la conversion est répliqué vers la base de données.

## Premier clic ou Dernier clic

### Attribution Dernier clic

L’attribution Dernier clic est le modèle d’attribution le plus courant utilisé par [!DNL Google Analytics]. Dans ce cas, la variable [!DNL Google Analytics] représente les paramètres de la gestion dynamique des balises pour la dernière source, ou la plus récente, avant l’événement de conversion. Voici ce qui se passe : [enregistré dans la base](../../data-analyst/analysis/google-track-user-acq.md). Notez que la variable [!DNL Google Analytics] Le cookie ne remplace les paramètres UTM précédents que si l’utilisateur clique sur une nouvelle URL contenant un nouvel ensemble de paramètres UTM.

Prenons l’exemple d’un utilisateur qui consulte un site web pour la première fois via [!DNL Google Analytics][!DNL Google Analytics][!DNL Google Analytics] *recherche payante*, puis renvoie via *référencement naturel*, puis revient au *site web directement* ou au moyen d’un *lien de courrier électronique* **sans paramètres UTM** avant l’événement de conversion. Dans cet exemple, la variable [!DNL Google Analytics] indique que la source de l’utilisateur est organique, car il s’agit de la dernière source avant la conversion. Le *path* de l’utilisateur avant cet événement de conversion final est ignoré. Si, au lieu de cela, l’utilisateur a consulté le site web à partir d’un lien de courrier électronique avec UTM, la variable [!DNL Google Analytics] indique que la source est &quot;email&quot;. Par conséquent, s’il existe des paramètres UTM dans le cookie et que l’utilisateur y accède directement, la variable [!DNL Google Analytics] Le cookie affichera toujours les paramètres UTM plutôt que &quot;direct&quot;.

>[!NOTE]
>
>d’un utilisateur spécifique ; [!DNL Google Analytics] les paramètres de cookie seront effacés lorsque le cookie [expires](https://developers.google.com/analytics/devguides/collection/analyticsjs/cookie-usage)ou lorsqu’un utilisateur efface ses cookies dans le navigateur.*)

### Attribution du premier clic

Certains outils d’attribution payante vous permettent de capturer &quot;la pile de crêpes&quot; de sources dans le chemin d’accès d’un utilisateur. Dans ce cas, dans l’exemple ci-dessus, l’attribution du premier clic nous indiquerait le référencement payant. Une minorité de sites web peut également implémenter leurs propres cookies qui capturent une pile de crêpes et stockent la première source dans leur base de données.

## Comment analyser l’attribution ?

[!DNL Google Analytics] dispose de fonctionnalités plus robustes dans son interface web qui vous permet d’exécuter quatre modèles d’attribution différents : premier clic, dernier clic, linéaire (diviser les recettes uniformément entre toutes les sources du chemin) et pondéré (attribution personnalisée).

Maintenant que vous comprenez quel est le modèle d’attribution pour chaque micro ou macro-conversion, la question devient : que faites-vous de la totalité des conversions d’un utilisateur ?  Par exemple, observez les UTM enregistrés en fonction de la logique de dernier clic GA :

* Enregistrement d’utilisateur sous licence organique
* Premier achat de l’utilisateur sous recherche payante 5,00 $
* Second achat de l’utilisateur sous email 50,00 $
* Troisième achat de l’utilisateur sous 10 $ organiques

Voici où vous demandez : Combien de recettes ai-je tiré du référencement payant ?  De l&#39;email ?  Du bio ?  Vous pourriez dire que les réponses sont 5, 50 et 10 (c&#39;est-à-dire, quelle que soit la dernière source), ou vous pourriez aussi dire que vous attribuez toutes les recettes à la première source (c&#39;est-à-dire que tous les 65 vont à organique). Vous pouvez également appliquer une analyse pondérée ou appliquer le modèle linéaire (soit environ 22 chacune).

## Documentation connexe

* [Suivi de la source de référence de commande via [!DNL Google Analytics] Commerce électronique](../importing-data/integrations/google-ecommerce.md)
* [Suivi de la source de référence des utilisateurs dans votre base de données](../analysis/google-track-user-acq.md)
* [Suivi des données utilisateur, navigateur et système d’exploitation dans votre base de données](../analysis/google-track-user-acq.md)
* [Découvrez vos sources et canaux d’acquisition les plus précieux](../analysis/most-value-source-channel.md)
* [Connectez-vous à [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)
* [Augmentation du retour sur investissement de vos campagnes publicitaires](../analysis/roi-ad-camp.md)
* [5 bonnes pratiques pour le balisage UTM dans [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
