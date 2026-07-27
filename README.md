---
source-git-commit: aa7acd0d863a3cd48ff83675b72c2a96eae02b4d
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 0%

---
# Documentation technique de Adobe Commerce Intelligence

Nous acceptons les contributions de la communauté ainsi que des employés d’Adobe qui ne font pas partie des équipes de documentation.

## Code de conduite d’Adobe Open Source

Ce projet a adopté le [Code de conduite d’Adobe Open Source](code-of-conduct.md) ou le Code de conduite de la Fondation [.NET](https://dotnetfoundation.org/code-of-conduct). Pour plus d’informations, consultez l’article [Contribution](contributing.md).

## À propos de vos contributions au contenu d’Adobe

Consultez le Guide du contributeur aux documents Adobe [](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html).

La façon dont vous contribuez dépend de qui vous êtes et du type de modifications que vous souhaitez apporter :

### Modifications mineures

Si vous contribuez à des mises à jour mineures, consultez l’article et cliquez sur la zone de commentaires qui s’affiche au bas de l’article, cliquez sur **Options de commentaires détaillées**, puis cliquez sur **Suggérer une modification** pour accéder au fichier source Markdown sur GitHub. Utilisez l’interface utilisateur GitHub pour effectuer vos mises à jour. Pour plus d’informations](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html) consultez le guide du contributeur aux [documents Adobe .

Les modifications ou précisions mineures que vous apportez aux documents et aux exemples de code dans ce référentiel sont soumises aux conditions d’utilisation d’Adobe.

### Modifications majeures ou nouveaux articles des membres de la communauté

Si vous faites partie de la communauté Adobe et que vous souhaitez rédiger un nouvel article ou apporter des modifications majeures, utilisez l’onglet Problèmes du référentiel Git pour soumettre un problème et commencer une conversation avec l’équipe de documentation. Une fois que vous avez accepté un plan, vous devez travailler avec un employé pour vous aider à introduire ce nouveau contenu en utilisant à la fois les référentiels publics et privés.

### Modifications majeures apportées par les employés d’Adobe

Si vous êtes rédacteur technique, responsable de programme ou développeur au sein de l’équipe produit d’une solution Adobe Experience Cloud et qu’il vous incombe de contribuer ou de rédiger des articles techniques, vous devez utiliser le référentiel privé de GHEC.

## Outils et configuration

Les contributeurs de la communauté peuvent utiliser l’interface utilisateur de GitHub pour apporter des modifications mineures, ou dupliquer le référentiel pour apporter des contributions majeures.

Pour plus d’informations, consultez le Guide du contributeur aux documents Adobe [](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html).

## Comment utiliser Markdown pour formater votre rubrique

Tous les articles de ce référentiel utilisent GitHub Flavored Markdown. Si vous ne connaissez pas Markdown, voir :

- [Guide de syntaxe Markdown](https://experienceleague.adobe.com/en/docs/authoring-guide/using/markdown/markdown-syntax)
- [Aide-mémoire sur la syntaxe Markdown](https://experienceleague.adobe.com/en/docs/authoring-guide/using/markdown/cheatsheet)

## Points d’extension de pré-validation pour l’optimisation des images

Ce référentiel comprend des hooks de prévalidation automatisés qui optimisent les images avant validation. **Tous les contributeurs doivent activer ces raccordements** afin d’assurer une optimisation cohérente des images et une taille de référentiel réduite.

### Configuration rapide

Après avoir cloné le référentiel, exécutez :

```bash
.githooks/setup-hooks.sh
```

### Ce que font les crochets

- Détecter automatiquement les fichiers image intermédiaires (`.png`, `.jpeg`, `.jpg`, `.gif`, `.svg`)
- Exécutez `image_optim` pour compresser et optimiser les images pixellisées (`.png`, `.jpeg`, `.jpg`, `.gif`).
- Réévaluation automatique des images optimisées
- Assurez-vous que toutes les images pixellisées validées sont correctement optimisées
- Vérifiez les SVG intermédiaires par rapport à une limite de taille et abandonnez la validation si un SVG surdimensionné est référencé à partir de `help/` (sinon, avertissez simplement).

### Avantages

- Taille réduite du référentiel
- Chargement plus rapide des pages pour la documentation
- Qualité d’image cohérente pour tous les contributeurs et contributrices
- Aucune optimisation manuelle requise

Pour obtenir des instructions détaillées sur la configuration, le dépannage et la configuration, voir [`.githooks/README.md`](.githooks/README.md).

## Guide de création d’Experience League

### Prise en main

- [Présentation de la prise en main](https://experienceleague.adobe.com/en/docs/authoring-guide/using/getting-started/getting-started)
- [Configuration Git](https://experienceleague.adobe.com/en/docs/authoring-guide/using/setup/tools/git-setup)
- [Principes de base de la documentation Git et GitHub](https://experienceleague.adobe.com/en/docs/authoring-guide/using/setup/tools/git-fundamentals)
- [Vidéos de démarrage rapide](https://experienceleague.adobe.com/en/docs/authoring-guide/using/getting-started/quick-start-guides/quick-start-overview)

### Workflows

- [Workflow pour les contributeurs peu fréquents](https://experienceleague.adobe.com/en/docs/authoring-guide/using/editing/git-workflow-infrequent-user)
- [Demandes d’extraction GitHub](https://experienceleague.adobe.com/en/docs/authoring-guide/using/editing/public-github)

### Création

- [Bonnes pratiques de création](https://experienceleague.adobe.com/en/docs/authoring-guide/using/authoring/authoring-best-practices)
- [Guide de syntaxe Markdown](https://experienceleague.adobe.com/en/docs/authoring-guide/using/markdown/markdown-syntax)
- [Aide-mémoire sur la syntaxe Markdown](https://experienceleague.adobe.com/en/docs/authoring-guide/using/markdown/cheatsheet)
- [Utilisation des tableaux](https://experienceleague.adobe.com/en/docs/authoring-guide/using/authoring/tables)
- [Ajout de liens](https://experienceleague.adobe.com/en/docs/authoring-guide/using/authoring/linking)
- [Déplacement et restructuration du contenu](https://experienceleague.adobe.com/en/docs/authoring-guide/using/authoring/restructure-new)
