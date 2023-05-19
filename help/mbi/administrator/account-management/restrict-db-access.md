---
title: Limitation de l’accès à votre base de données
description: Découvrez comment restreindre l’accès au serveur qui héberge votre base de données.
exl-id: 7a0bc0d7-086e-4a6e-b1dd-6db13814710e
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Limitation de l’accès

Lorsque vous créez un tunnel SSH vers votre serveur, il n’est pas nécessaire d’utiliser [!DNL Adobe Commerce Intelligence] pour avoir accès à tout ce qui est autre que la base de données. Si vous ne voulez pas [!DNL Commerce Intelligence] pour disposer d’un accès complet au serveur qui héberge votre base de données, vous pouvez en restreindre l’accès en obligeant le [!DNL Commerce Intelligence Linux] dans un [shell bash restreint](https://www.gnu.org/software/bash/manual/html_node/The-Restricted-Shell.html).

Vous avez peut-être deviné à partir du nom, mais un shell bash restreint est utilisé pour configurer un environnement plus contrôlé que le shell standard. Ce qui est important dans ce type de shell, c&#39;est que les utilisateurs restreints de shell ne peuvent pas accéder aux fonctions du système ni apporter des modifications.

Pour restreindre les [!DNL Commerce Intelligence Linux] utilisateur, vous devez effectuer deux opérations :

1. Définissez la variable d’environnement PATH sur la chaîne vide. Cela signifie que l’utilisateur ne peut pas accéder aux exécutables du système.

1. Assurez-vous que le shell exécuté est `bash -r`

Ces deux options peuvent être effectuées à l’intérieur de la variable `authorized_keys` dans le fichier d’accueil de l’utilisateur. `dir/.ssh` dans le cadre de la commande exécutée lorsque l’utilisateur se connecte. Il ressemble à ceci :

```bash
... other keys ...
command="env PATH="" /bin/bash -r" <rjmetrics public key goes here>
... other keys ...
```

Une fois cette opération terminée, l’utilisateur que vous avez créé pour [!DNL Commerce Intelligence] ne peuvent pas apporter de modifications à votre système.
