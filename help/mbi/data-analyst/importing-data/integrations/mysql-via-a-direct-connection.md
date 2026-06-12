---
title: Connexion à MySQL via une connexion directe
description: Découvrez comment vous connecter via  [!DNL MongoDB]  connexion directe.
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/HkKVLKV9RpLIWN-YY5GggdnlHeBB2Xg9odAbSZklHGE
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 3a6b80d7bcfa5db4d86ab4da81239e3ea804f6ad
workflow-type: tm+mt
source-wordcount: 399
ht-degree: 0%

---

# Connexion [!DNL MySQL] via une connexion directe

## Dans cette rubrique

* [Autoriser l’accès à l’adresse  [!DNL Commerce Intelligence] ](#allowlist)
* [Créez un  [!DNL MySQL]  pour  [!DNL Commerce Intelligence]](#steptwo)
* [Saisissez les informations de connexion dans  [!DNL Commerce Intelligence]](#stepthree)

## Atteindre

* [[!DNL MySQL] via `SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md)
* [Vérification de la clé hôte SSH](../integrations/ssh-host-key-verification.md)
* [[!DNL MySQL] via  [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>[!DNL Adobe] vous recommande d’utiliser [SSH](../integrations/mysql-via-ssh-tunnel.md) ou une autre forme de chiffrement pour sécuriser vos données ! Pour la vérification de la clé hôte SSH, voir [Vérification de la clé hôte SSH](../integrations/ssh-host-key-verification.md). Si cette option n&#39;est pas disponible, vous pouvez tout de même [!DNL Commerce Intelligence] connecter directement à votre base de données à l&#39;aide des instructions de cette rubrique.

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

* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
