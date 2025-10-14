---
title: Connexion à MySQL via une connexion directe
description: Découvrez comment vous connecter via  [!DNL MongoDB]  connexion directe.
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# Connexion [!DNL MySQL] via une connexion directe

## Dans cette rubrique

* [Autoriser l’accès à l’adresse  [!DNL Commerce Intelligence] &#x200B;](#allowlist)
* [Créez un  [!DNL MySQL]  pour  [!DNL Commerce Intelligence]](#steptwo)
* [Saisissez les informations de connexion dans  [!DNL Commerce Intelligence]](#stepthree)

## Atteindre

* [[!DNL MySQL] via &#x200B;](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL] via  [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>[!DNL Adobe] vous recommande d’utiliser [SSH](../integrations/mysql-via-ssh-tunnel.md) ou une autre forme de chiffrement pour sécuriser vos données ! Si cette option n&#39;est pas disponible, vous pouvez tout de même [!DNL Commerce Intelligence] connecter directement à votre base de données à l&#39;aide des instructions de cette rubrique.

Cette rubrique vous guide tout au long de la connexion directe de votre base de données [!DNL MySQL] à [!DNL Commerce Intelligence]. Ces paramètres peuvent également être utilisés avec [!DNL Adobe Commerce] ou toute autre base de données eCommerce utilisant MySQL.

## Autoriser l&#39;accès aux adresses IP [!DNL Commerce Intelligence] {#allowlist}

Pour que la connexion soit établie, vous devez configurer votre pare-feu afin d’autoriser l’accès à partir de vos adresses IP. Ils sont `54.88.76.97` et `34.250.211.151`, mais ils se trouvent également sur la page des informations d’identification [!DNL MySQL] :

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Créer un utilisateur [!DNL MySQL] pour [!DNL Commerce Intelligence]

La méthode la plus simple pour créer un utilisateur `MySQL` pour [!DNL Commerce Intelligence] consiste à exécuter la requête suivante lorsque vous êtes connecté à `MySQL` avec des privilèges `GRANT`. Remplacez `Commerce Intelligence IP Address` par l’adresse IP [!DNL Commerce Intelligence] et `secure password` par un mot de passe sécurisé de votre choix :

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<Commerce Intelligence IP address>' IDENTIFIED BY '<secure password>';
```

Pour empêcher cet utilisateur d&#39;accéder aux données de bases de données, de tables ou de colonnes spécifiques, vous pouvez exécuter des requêtes `GRANT` qui autorisent uniquement l&#39;accès aux données que vous autorisez.

**Réexécutez la requête GRANT pour toutes les adresses IP requises à l’aide du même utilisateur et du même mot de passe.**

## Saisir les informations de connexion dans Commerce Intelligence

Pour conclure, vous devez saisir les informations de connexion et d’utilisateur dans [!DNL Commerce Intelligence]. Avez-vous laissé la page des informations d’identification [!DNL MySQL] ouverte ? Dans le cas contraire, accédez à **[!UICONTROL Data** > **Connections]** et cliquez sur **[!UICONTROL Add New Data Source]**, puis sur l’icône [!DNL MySQL]. N’oubliez pas de remplacer le bouton (bascule) `Encrypted` par `Yes`.

Saisissez les informations suivantes dans cette page, en commençant par la section `Database Connection` :

* `Connection Nickname` : saisissez un nom pour l’intégration (par exemple, Boutique eCommerce)
* `Username` : nom d’utilisateur de l’utilisateur [!DNL Commerce Intelligence] [!DNL MySQL]
* `Password` : mot de passe de l’utilisateur [!DNL Commerce Intelligence] [!DNL MySQL]
* `Port` : port de MySQL sur votre serveur (`3306` par défaut)
* `Host` : par défaut, il s’agit de localhost. En règle générale, il s’agit de la valeur bind-address de votre serveur [!DNL MySQL], qui est `127.0.0.1 (localhost)` par défaut, mais il peut également s’agir d’une adresse réseau locale (par exemple, `192.168.0.1`) ou de l’adresse IP publique de votre serveur.

  La valeur se trouve dans votre fichier `my.cnf` (situé à l’adresse `/etc/my.cnf`) sous la ligne qui lit `\[mysqld\]`. Si la ligne bind-address est commentée dans ce fichier, votre serveur est protégé contre les tentatives de connexion externes.

Lorsque vous avez terminé, cliquez sur **[!UICONTROL Save & Test]** pour terminer la configuration.

## Documentation connexe

* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=fr)
