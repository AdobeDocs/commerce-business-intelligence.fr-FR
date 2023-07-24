---
title: 'Google Analytics : suivi des données de l’appareil utilisateur et du navigateur dans votre base de données'
description: Découvrez combien d’utilisateurs se connectent réellement via des appareils mobiles et comment cela affecte la valeur de durée de vie de ces utilisateurs.
exl-id: 57b1bc45-b139-4370-86ea-2fbd021aa14d
role: Admin, User
feature: Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# [!UICONTROL Google Analytics] Tracking

Avec [!UICONTROL Google Analytics] vous pouvez [enregistrer les informations de source de référence](../analysis/google-track-user-acq.md) pour comprendre d’où viennent vos utilisateurs les plus précieux. Cette rubrique aborde la plateforme (par exemple, le périphérique ou le navigateur) sur laquelle travaillent les utilisateurs. Vous pourrez ainsi comprendre combien d’utilisateurs se connectent par le biais d’appareils mobiles et comment cela affecte la valeur de durée de vie de ces utilisateurs.

## Enregistrement des données de navigateur et de périphérique utilisateur

Chaque fois qu’une demande est envoyée à votre site web, le navigateur de l’utilisateur envoie une chaîne User-Agent contenant des informations sur la plateforme qui la demande. Voici quelques exemples de la chaîne User-Agent :

1. `Mozilla/5.0 (Macintosh; Intel Mac OS X 10\_8\_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/27.0.1453.116 Safari/537.36`
1. `Mozilla/5.0 (Windows NT 6.1; WOW64; rv:17.0) Gecko/17.0 Firefox/17.0`
1. `Mozilla/5.0 (iPhone; U; CPU iPhone OS 4\_0 like Mac OS X; en-us) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8A293 Safari/6531.22.7`
1.` Mozilla/5.0 (iPad; CPU OS 5\_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B176 Safari/7534.48.3`
1. `Mozilla/5.0 (Linux; U; Android 2.2; en-us; Nexus One Build/FRF91) AppleWebKit/533.1 (KHTML, like Gecko) Version/4.0 Mobile Safari/533.1`

Si vous regardez de plus près, vous verrez que la chaîne contient des informations sur le système d’exploitation de l’utilisateur, son navigateur et le nom de l’appareil qu’il utilise (s’il porte un nom). Bien que les chaînes User-Agent varient considérablement d’une plate-forme à l’autre et même d’une version d’une même plate-forme, il est généralement vrai que le nom de la plate-forme existera quelque part à l’intérieur. Par exemple, #1 ci-dessus est un Mac avec le navigateur Chrome, #2 ci-dessus est un ordinateur Windows avec le navigateur Firefox, #3 est un iPhone, #4 est un iPad et #5 est un appareil Android.

Ces informations sont accessibles par votre serveur chaque fois qu’une demande est faite. En PHP, la chaîne User-Agent est stockée dans `$_SERVER['HTTP_USER_AGENT']`. Dans Ruby on Rails, il est stocké dans `request.env['HTTP_USER_AGENT']`. D’autres langues et environnements vous permettront d’y accéder de la même manière.

### Quand devriez-vous enregistrer ces données ?

[!DNL Adobe] recommande d’ajouter un nouveau champ appelé `Platform` ou `User-Agent` à `Customers` et `Orders` des tables de base de données permettant de stocker ces informations chaque fois qu’un utilisateur est créé ou qu’une commande est passée. Si vous utilisez une base de données SQL, ce champ doit être une `VARCHAR(255)`. 

>[!NOTE]
>
>Le `User-Agent` La chaîne est autorisée à être beaucoup plus longue, mais en pratique, elle dépasse rarement cette longueur.

### Comment analyser les segments utiles ?

Il existe un certain nombre de bibliothèques pour vous aider à analyser la variable `User-Agent` chaîne en composants tels que le système d’exploitation, le périphérique, etc. Reportez-vous à la section [projet ua-parser](https://github.com/tobie/ua-parser) pour en savoir plus.

Grâce à ces nouvelles informations, vous pouvez mieux comprendre comment les utilisateurs accèdent à votre site. Vous pouvez ensuite personnaliser leur expérience ou créer des campagnes marketing pour certains groupes.

## Associé

* [Suivi de la source de référence de commande via [!DNL Google Anaytics] Commerce électronique](../importing-data/integrations/google-ecommerce.md)
* [Suivi de la source de référence des utilisateurs dans votre base de données](../analysis/google-track-user-acq.md)
* [Découvrez vos sources et canaux d’acquisition les plus précieux](../analysis/most-value-source-channel.md)
* [Connectez-vous à [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)
* [Augmentation du retour sur investissement de vos campagnes publicitaires](../analysis/roi-ad-camp.md)
* [Comment [!DNL Google Analytics] Fonctionnement de l’attribution UTM ?](../analysis/utm-attributes.md)
