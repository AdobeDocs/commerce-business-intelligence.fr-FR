---
title: Limitation de l’accès à votre base de données
description: Découvrez comment restreindre l’accès au serveur qui héberge votre base de données.
exl-id: 7a0bc0d7-086e-4a6e-b1dd-6db13814710e
role: Admin, User
feature: Accounts, User Management
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# Limitation de l’accès

Lorsque vous créez un tunnel SSH vers votre serveur, [!DNL Adobe Commerce Intelligence] n’a pas besoin d’accéder à autre chose que la base de données. Si vous ne souhaitez pas que [!DNL Commerce Intelligence] ait un accès complet au serveur qui héberge votre base de données, vous pouvez restreindre l&#39;accès en forçant l&#39;utilisateur [!DNL Commerce Intelligence Linux] dans un [shell bash restreint](https://www.gnu.org/software/bash/manual/html_node/The-Restricted-Shell.html).

Vous avez peut-être deviné à partir du nom, mais un shell bash restreint est utilisé pour configurer un environnement plus contrôlé que le shell standard. Ce qui est important dans ce type de shell, c&#39;est que les utilisateurs restreints de shell ne peuvent pas accéder aux fonctions du système ni apporter des modifications.

Pour restreindre l’utilisateur de [!DNL Commerce Intelligence Linux], vous devez effectuer deux opérations :

1. Définissez la variable d’environnement PATH sur la chaîne vide. Cela signifie que l’utilisateur ne peut pas accéder aux exécutables du système.

1. Assurez-vous que le shell exécuté est `bash -r`

Ces deux opérations peuvent être effectuées dans le fichier `authorized_keys` du répertoire `dir/.ssh` de l’utilisateur, dans le cadre de la commande exécutée lorsque l’utilisateur se connecte. Il ressemble à ceci :

```bash
... other keys ...
command="env PATH="" /bin/bash -r" <rjmetrics public key goes here>
... other keys ...
```

Une fois cette opération terminée, l’utilisateur que vous avez créé pour [!DNL Commerce Intelligence] ne peut pas apporter de modifications à votre système.
