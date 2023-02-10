---
title: Connexion de MySQL via une connexion directe
description: Découvrez comment vous connecter [!DNL MongoDB] via une connexion directe.
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---

# Connexion [!DNL MongoDB] via une connexion directe

## Dans cet article

* [Autoriser l’accès au [!DNL MBI] Adresse IP](#allowlist)
* [Créez un ](#steptwo)
* [Saisissez les informations de connexion dans [!DNL MBI]](#stepthree)

## Accéder à

* [`MySQL via SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md)
* `MySQL via direct connection`
* [`MySQL via cPanel`](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>Nous vous recommandons vivement d’utiliser [SSH](../integrations/mysql-via-ssh-tunnel.md) ou une autre forme de cryptage pour sécuriser vos données ! S’il ne s’agit pas d’une option, vous pouvez toujours vous connecter directement. [!DNL MBI] à votre base de données en suivant les instructions de cet article.

Dans cet article, nous vous guidons tout au long des étapes nécessaires pour connecter directement votre base de données MySQL à [!DNL MBI]. Ces paramètres peuvent également être utilisés avec Commerce ou toute autre base de données eCommerce utilisant MySQL.

## Autoriser l’accès au [!DNL MBI] Adresses IP {#allowlist}

Pour que la connexion soit établie, vous devez configurer votre pare-feu afin d’autoriser l’accès à partir de nos adresses IP. Ils sont `54.88.76.97` et `34.250.211.151`, mais il se trouve également sur la page des informations d’identification MySQL :

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Création d’un utilisateur MySQL pour [!DNL MBI]

La méthode la plus simple pour créer une `MySQL` user pour [!DNL MBI] doit exécuter la requête suivante lorsque vous êtes connecté à `MySQL` avec `GRANT` des privilèges. Remplacer `MBI IP Address` avec le [!DNL MBI] Adresse IP et remplacement `secure password` avec un mot de passe sécurisé de votre choix :

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<MBI IP address>' IDENTIFIED BY '<secure password>';
```

Pour empêcher cet utilisateur d’accéder aux données de bases de données, de tableaux ou de colonnes spécifiques, vous pouvez exécuter `GRANT` requêtes qui permettent uniquement d’accéder aux données que vous autorisez.

**Exécutez à nouveau la requête GRANT pour toutes les adresses IP requises à l’aide du même utilisateur et du même mot de passe.**

## Entrer les informations de connexion dans MBI

Pour terminer, nous devons saisir les informations de connexion et d’utilisateur dans [!DNL MBI]. Avez-vous laissé la page des informations d’identification MySQL ouverte ? Si ce n’est pas le cas, accédez à **[!UICONTROL Data** > **Connections]** et cliquez sur **[!UICONTROL Add New Data Source]**, puis l’icône MySQL. N’oubliez pas de modifier la variable `Encrypted` bascule vers `Yes`.

Renseignez les informations suivantes dans cette page, en commençant par le `Database Connection` section :

* `Connection Nickname`: Saisissez un nom pour l’intégration (par exemple, Boutique eCommerce).
* `Username`: Nom d’utilisateur de la variable [!DNL MBI] Utilisateur MySQL
* `Password`: Le mot de passe du [!DNL MBI] Utilisateur MySQL
* `Port`: Port de MySQL sur votre serveur (`3306` par défaut)
* `Host`: Par défaut, il s’agit de localhost. En général, il s’agit de la valeur de l’adresse de liaison de votre serveur MySQL, qui est, par défaut, `127.0.0.1 (localhost)`, mais peut également être une adresse réseau locale (par exemple, `192.168.0.1`) ou l’adresse IP publique de votre serveur.

   La valeur se trouve dans votre `my.cnf` (situé généralement à l’emplacement `/etc/my.cnf`) sous la ligne qui indique `\[mysqld\]`. Si la ligne d’adresse de liaison est commentée dans ce fichier, votre serveur est sécurisé suite à des tentatives de connexion externes.

C&#39;est tout ! Lorsque vous avez terminé, cliquez sur **[!UICONTROL Save & Test]** pour terminer la configuration.

## Documentation connexe

* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
