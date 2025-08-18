---
title: Limitation de l'accès à votre base de données
description: Découvrez comment restreindre l’accès, en limitant l’accès au serveur qui héberge votre base de données.
exl-id: 7a0bc0d7-086e-4a6e-b1dd-6db13814710e
role: Admin, User
feature: Accounts, User Management
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# Restreindre l’accès

Lorsque vous créez un tunnel SSH vers votre serveur, il n&#39;est pas nécessaire que [!DNL Adobe Commerce Intelligence] ayez accès à autre chose qu&#39;à la base de données. Si vous ne souhaitez pas que le [!DNL Commerce Intelligence] dispose d’un accès complet au serveur hébergeant votre base de données, vous pouvez restreindre l’accès en forçant l’utilisateur [!DNL Commerce Intelligence Linux] à accéder à un shell [bash limité](https://www.gnu.org/software/bash/manual/html_node/The-Restricted-Shell.html).

Vous avez peut-être deviné d’après son nom, mais un shell bash restreint est utilisé pour configurer un environnement plus contrôlé que le shell standard. Ce qui est important à propos de ce type de shell, c’est que les utilisateurs shell restreints ne peuvent pas accéder aux fonctions système ni effectuer des modifications.

Pour restreindre l’utilisateur ou l’utilisatrice [!DNL Commerce Intelligence Linux], vous devez effectuer deux opérations :

1. Définissez la variable d’environnement PATH sur la chaîne vide. Cela signifie que l’utilisateur ne peut pas accéder aux exécutables système.

1. Vérifiez que le shell exécuté est `bash -r`

Ces deux opérations peuvent être effectuées dans le fichier `authorized_keys` du répertoire de `dir/.ssh` principal de l’utilisateur dans le cadre de la commande exécutée lorsque l’utilisateur se connecte. Voici à quoi cela ressemble :

```bash
... other keys ...
command="env PATH="" /bin/bash -r" <rjmetrics public key goes here>
... other keys ...
```

Une fois cette opération terminée, l’utilisateur que vous avez créé pour [!DNL Commerce Intelligence] ne peut pas apporter de modifications à votre système.
