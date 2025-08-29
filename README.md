---
source-git-commit: 6233779ba2e2a99ed229f8aa97497eb8d9d877f7
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 5%

---
# Documentation technique de Adobe Commerce Intelligence

Nous acceptons les contributions de la communauté ainsi que des employés d’Adobe qui ne font pas partie des équipes de documentation.

## Code de conduite d’Adobe Open Source

Ce projet respecte le [Code de conduite d’Adobe Open Source](code-of-conduct.md) ou le [Code de conduite .NET Foundation](https://dotnetfoundation.org/code-of-conduct). Pour plus d’informations, consultez l’article [Contribution](contributing.md).

## À propos de vos contributions au contenu d’Adobe

Consultez le Guide du contributeur aux documents Adobe [](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html).

La façon dont vous contribuez dépend de qui vous êtes et du type de modifications que vous souhaitez apporter :

### Modifications mineures

Si vous contribuez à des mises à jour mineures, consultez l’article et cliquez sur la zone de commentaires qui s’affiche au bas de l’article, cliquez sur **Options de commentaires détaillées**, puis cliquez sur **Suggérer une modification** pour accéder au fichier source Markdown sur GitHub. Utilisez l’interface utilisateur GitHub pour effectuer vos mises à jour. Pour plus d’informations[ consultez le guide du contributeur aux ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html)documents Adobe .

Les modifications ou précisions mineures que vous apportez aux documents et aux exemples de code dans ce référentiel sont soumises aux conditions d’utilisation d’Adobe.

### Modifications majeures ou nouveaux articles des membres de la communauté

Si vous faites partie de la communauté Adobe et que vous souhaitez rédiger un nouvel article ou apporter des modifications majeures, utilisez l’onglet Problèmes du référentiel Git pour soumettre un problème et commencer une conversation avec l’équipe de documentation. Une fois que vous avez accepté un plan, vous devez travailler avec un employé pour vous aider à introduire ce nouveau contenu en utilisant à la fois les référentiels publics et privés.

### Modifications majeures apportées par les employés d’Adobe

Si vous êtes rédacteur technique, responsable de programme ou développeur au sein de l’équipe produit d’une solution Adobe Experience Cloud et qu’il vous incombe de contribuer ou de rédiger des articles techniques, vous devez utiliser le référentiel privé à l’adresse `https://git.corp.adobe.com/AdobeDocs`.

## Outils et configuration

Les contributeurs de la communauté peuvent utiliser l’interface utilisateur de GitHub pour apporter des modifications mineures, ou dupliquer le référentiel pour apporter des contributions majeures.

Pour plus d’informations, consultez le Guide du contributeur aux documents Adobe [](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html).

## Comment utiliser Markdown pour formater votre rubrique

Tous les articles de ce référentiel utilisent GitHub Flavored Markdown. Si vous ne connaissez pas Markdown, voir :

- [Principes de base de Markdown](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/)
- [Aide-mémoire imprimable Markdown](https://guides.github.com/pdfs/markdown-cheatsheet-online.pdf)

## Points d’extension de pré-validation pour l’optimisation des images

Ce référentiel comprend des hooks de prévalidation automatisés qui optimisent les images avant validation. **Tous les contributeurs doivent activer ces raccordements** afin d’assurer une optimisation cohérente des images et une taille de référentiel réduite.

### Configuration rapide

Après avoir cloné le référentiel, exécutez :

```bash
.githooks/setup-hooks.sh
```

### Ce que font les crochets

- Détecter automatiquement les fichiers image intermédiaires (PNG, JPG, JPEG, GIF, SVG)
- Exécutez `image_optim` pour compresser et optimiser les images.
- Réévaluation automatique des images optimisées
- Vérifiez que toutes les images validées sont correctement optimisées.

### Avantages

- Taille réduite du référentiel
- Chargement plus rapide des pages pour la documentation
- Qualité d’image cohérente pour tous les contributeurs et contributrices
- Aucune optimisation manuelle requise

Pour obtenir des instructions détaillées sur la configuration, le dépannage et la configuration, voir [`.githooks/README.md`](.githooks/README.md).
