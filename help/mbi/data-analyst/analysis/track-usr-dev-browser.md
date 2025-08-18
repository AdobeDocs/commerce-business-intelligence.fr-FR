---
title: Google Analytics - Suivre les données des appareils utilisateur et des navigateurs dans votre base de données
description: Découvrez combien d’utilisateurs se connectent réellement via des appareils mobiles et comment cela affecte la valeur de durée de vie de ces utilisateurs.
exl-id: 57b1bc45-b139-4370-86ea-2fbd021aa14d
role: Admin, User
feature: Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# Suivi des [!UICONTROL Google Analytics]

Avec [!UICONTROL Google Analytics], vous pouvez [enregistrer les informations sur la source de référence](../analysis/google-track-user-acq.md) pour comprendre d’où viennent vos utilisateurs les plus précieux. Cette rubrique décrit la plateforme (par exemple, un appareil ou un navigateur) sur laquelle travaillent vos utilisateurs. Vous pourrez ainsi comprendre combien d’utilisateurs se connectent réellement via des appareils mobiles et comment cela affecte la valeur de durée de vie de ces utilisateurs.

## Enregistrement des données de l’appareil utilisateur et du navigateur

Chaque fois qu’une requête est envoyée à votre site web, le navigateur de l’utilisateur envoie une chaîne User-Agent avec des informations sur la plateforme qui effectue la requête. Voici quelques exemples de chaîne Agent-utilisateur :

1. `Mozilla/5.0 (Macintosh; Intel Mac OS X 10\_8\_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/27.0.1453.116 Safari/537.36`
1. `Mozilla/5.0 (Windows NT 6.1; WOW64; rv:17.0) Gecko/17.0 Firefox/17.0`
1. `Mozilla/5.0 (iPhone; U; CPU iPhone OS 4\_0 like Mac OS X; en-us) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8A293 Safari/6531.22.7`
1,` Mozilla/5.0 (iPad; CPU OS 5\_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B176 Safari/7534.48.3`
1. `Mozilla/5.0 (Linux; U; Android 2.2; en-us; Nexus One Build/FRF91) AppleWebKit/533.1 (KHTML, like Gecko) Version/4.0 Mobile Safari/533.1`

Si vous regardez attentivement, vous verrez que la chaîne contient des informations sur le système d’exploitation de l’utilisateur, son navigateur et le nom de l’appareil qu’il utilise (s’il porte un nom). Bien que les chaînes User-Agent varient considérablement d’une plateforme à l’autre et même d’une version à l’autre d’une même plateforme, il est généralement vrai que le nom de la plateforme existe quelque part dans . Par exemple, #1 ci-dessus est un Mac avec le navigateur Chrome, #2 ci-dessus est un ordinateur Windows avec le navigateur Firefox, #3 est un iPhone, #4 est un iPad et #5 est un appareil Android.

Votre serveur peut accéder à ces informations chaque fois qu’une demande est effectuée. En PHP, la chaîne User-Agent est stockée en `$_SERVER['HTTP_USER_AGENT']`. Dans Ruby on Rails, il est stocké dans `request.env['HTTP_USER_AGENT']`. D’autres langues et environnements vous permettront d’y accéder de la même manière.

### Quand enregistrer ces données ?

[!DNL Adobe] vous recommande d’ajouter un nouveau champ appelé `Platform` ou `User-Agent` à vos tables de base de données `Customers` et `Orders` pour stocker ces informations chaque fois qu’un utilisateur est créé ou qu’une commande est passée. Si vous utilisez une base de données SQL, ce champ doit être un `VARCHAR(255)`. 

>[!NOTE]
>
>La chaîne `User-Agent` peut être beaucoup plus longue que cette valeur, mais en pratique, elle dépasse rarement cette longueur.

### Comment analyser les segments utiles ?

Il existe un certain nombre de bibliothèques pour vous aider à analyser la chaîne de `User-Agent` en composants tels que le système d’exploitation, l’appareil, etc. Consultez le projet [ua-parser](https://github.com/tobie/ua-parser) pour en savoir plus.

Grâce à ces nouvelles informations, vous pouvez mieux comprendre comment les utilisateurs accèdent à votre site. Vous pouvez ensuite personnaliser leur expérience ou créer des campagnes marketing pour certains groupes.

## Connexe

* [Suivre la source de référence des commandes via [!DNL Google Anaytics] E-Commerce](../importing-data/integrations/google-ecommerce.md)
* [Suivre la source de référence des utilisateurs dans votre base de données](../analysis/google-track-user-acq.md)
* [Découvrez vos sources et canaux d’acquisition les plus précieux.](../analysis/most-value-source-channel.md)
* [Connecter votre  [!DNL Google Adwords] ](../importing-data/integrations/google-adwords.md)
* [Augmenter le retour sur investissement de vos campagnes publicitaires](../analysis/roi-ad-camp.md)
* [Comment fonctionne  [!DNL Google Analytics] ’attribution UTM ?](../analysis/utm-attributes.md)
