---
title: Modélisation des données MongoDB
description: Découvrez comment éviter les modèles de données qui posent problème.
exl-id: 556c854b-5d7c-4f72-8ed7-5bc08d9ee5b9
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---

# [!DNL MongoDB] Modélisation des données

When [!DNL MBI] extrait [!DNL MongoDB] données, ces données sont traduites dans un modèle relationnel.

La mauvaise nouvelle : Bien que la plupart des modèles de données ne posent pas problème, certains d’entre eux, en raison de la traduction en modèle relationnel, [!DNL MBI] ne prend pas en charge.

La bonne nouvelle : Tous ces modèles peuvent être évités.

## Tableaux imbriqués {#subnested}

Si votre collection ressemble à l’exemple ci-dessous, [!DNL MBI] ne réplique que les données du tableau d’éléments. Les données du tableau de sous-éléments ne sont pas extraites.

```bash
    {
        _id: 0000000000000001
        items: [
            {
                _id: 0000000000000002
               subItems: [
                   {
                       _id: 0000000000000003
                      name: "Donut"
                      description: "glazed"
                   }
               ]
            }
        ]
    }
```

## Clés d’objet variable {#varobjectkeys}

Les collections qui incluent des objets avec des clés d’objet variables ne sont pas répliquées dans [!DNL MBI]. Par exemple :

```bash
    {
        _id: 0000000000000001
        friends: {
            0000000000000002: "Jimmy",
            0000000000000004: "Roger",
            0000000000000005: "Susan"
        },
    }
```

Cela se produit généralement lorsqu’un objet est utilisé et qu’un tableau est plus approprié. Maintenant, retravaillez l’exemple ci-dessus :

```bash
    {
        _id: 0000000000000001
        friends: [
            { friend_id: 0000000000000002, name: "Jimmy" },
            { friend_id: 0000000000000004, name: "Roger" },
            { friend_id: 0000000000000005, name: "Susan"}
        ]
    }
```
