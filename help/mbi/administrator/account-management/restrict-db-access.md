---
title: Limitation de l'accès à votre base de données
description: Découvrez comment restreindre l’accès, en limitant l’accès au serveur qui héberge votre base de données.
role: Admin, User
feature: Accounts, User Management
exl-id: 7a0bc0d7-086e-4a6e-b1dd-6db13814710e
TQID: 'https://experienceleague.adobe.com/O2cS-hbhjqktc4LpJD6agxgIwabrypgCY9fnJTCR2XM'
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: 9e444628-408e-5d74-8cd4-c552f0d5d47f
    internal-label: Accounts
  - id: b6935462-7263-4ced-a703-60de6a5aeb2d
    internal-label: Administration
subfeature_v2:
  - id: d971c7be-3e54-4af9-807c-8d1f9f7b22df
    internal-label: User management
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%
---

# Restreindre l’accès

Lorsque vous créez un tunnel SSH vers votre serveur, il n&#39;est pas nécessaire que [!DNL Adobe Commerce Intelligence] ayez accès à autre chose qu&#39;à la base de données. Pour l’inscription de la clé de l’hôte SSH, les erreurs et le dépannage, consultez [Vérification de la clé de l’hôte SSH](../../data-analyst/importing-data/integrations/ssh-host-key-verification.md). Si vous ne souhaitez pas que le [!DNL Commerce Intelligence] dispose d’un accès complet au serveur hébergeant votre base de données, vous pouvez restreindre l’accès en forçant l’utilisateur [!DNL Commerce Intelligence Linux] à accéder à un shell [bash limité](https://www.gnu.org/software/bash/manual/html_node/The-Restricted-Shell.html).

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
