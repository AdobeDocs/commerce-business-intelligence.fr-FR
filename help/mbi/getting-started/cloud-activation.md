---
title: Activez votre [!DNL MBI] Compte pour les abonnements à Cloud Starter
description: Découvrez comment activer [!DNL MBI] pour les projets Cloud Starter.
exl-id: 172439ee-fa1d-4872-b6a9-c61a212a7cbe
source-git-commit: 6f018ab220f2ae573cbc9016f9efb83c27a254be
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Activez votre [!DNL MBI] Compte pour `Cloud Starter` Abonnements

Pour activer [!DNL MBI] pour `Cloud Starter` projets, créez d’abord un [!DNL MBI] , puis créez une `SSH` puis enfin connectez-vous à votre base de données Commerce. Voir [activation des abonnements on-premise](../getting-started/onpremise-activation.md).

>[!NOTE]
>
>Pour activer l’aide [!DNL MBI] pour `Cloud Pro` pour les projets, contactez votre équipe de compte d’Adobe ou votre conseiller technique client.

1. Créez votre [!DNL MBI] Compte.

   - Accédez à [Connexion au compte Adobe Commerce](https://account.magento.com/customer/account/login)

   - Accédez à **[!UICONTROL My Account** > **My [!DNL MBI] Instances]**.

   - Cliquez sur **[!UICONTROL Create Instance]**. Si vous ne voyez pas ce bouton, contactez votre équipe de compte d’Adobe ou votre conseiller technique du client.

   - Sélectionnez votre `Cloud Starter` abonnement. Si vous avez uniquement une `cloud starter` Cette option sera automatiquement sélectionnée.

   - Cliquez sur **[!UICONTROL Continue]**.

   - Saisissez vos informations pour créer votre compte.

   ![](../assets/create-account-2.png)

   - Accédez à votre boîte de réception et vérifiez votre adresse électronique.

   ![](../assets/create-account-3.png)

   - Créez votre mot de passe.

   ![](../assets/create-account-4.png)

   - Une fois votre compte créé, vous avez la possibilité d’ajouter des utilisateurs à votre nouveau compte. Vous pouvez désormais ajouter des administrateurs techniques pour réaliser les étapes suivantes.

   ![](../assets/create-account-5.png)

1. Informations d’entrée sur votre magasin pour définir vos préférences.

   ![](../assets/create-account-6.png)

   Vous devez recueillir certaines informations avant de pouvoir connecter votre base de données pour la troisième étape du flux d’intégration. Vous allez renseigner la variable `Connect your database` dans l’étape 9.

1. Créer un [!DNL MBI] Utilisateur.

   - Créez un utilisateur dans votre [Compte Adobe Commerce](https://accounts.magento.com).

   - _Pourquoi un nouvel utilisateur ?_ [!DNL MBI] nécessite qu’un utilisateur soit ajouté au projet pour récupérer en permanence de nouvelles données à transférer au [!DNL MBI] entrepôt de données. Cet utilisateur servira de connexion. L’ajout de cet utilisateur au projet se fera à l’étape 4.

   - La raison d&#39;avoir un dédié [!DNL MBI] L’utilisateur doit empêcher l’utilisateur ajouté d’être désactivé ou supprimé par inadvertance et arrêter la fonction [!DNL MBI] connexion.

1. Ajoutez l’utilisateur nouvellement créé à l’environnement Principal du projet en tant que `Contributor`.

   ![](../assets/create-account-7.png)

1. Obtenez votre [!DNL MBI] `SSH` clés.

   - Accédez au `Connect your database` de la [!DNL MBI] configurer l’interface utilisateur et faire défiler l’écran vers le bas jusqu’à `Encryption settings`.

   - Pour le `Encryption Type` champ, choisissez `SSH Tunnel`.

   - Dans la liste déroulante, vous pouvez copier et coller le [!DNL MBI] `Public Key`.

   ![](../assets/create-account-8.png)

1. Ajoutez la nouvelle [!DNL MBI] `Public key` au [!DNL MBI] utilisateur créé à l’étape 5.

   - Accédez à [votre compte Adobe Commerce cloud](https://accounts.magento.cloud/). Connectez-vous avec les informations de connexion de votre compte pour le nouveau [!DNL MBI] utilisateur créé. Ensuite, accédez au `Account Settings` .

   - Faites défiler la page vers le bas et développez la liste déroulante pour `SSH` clés. Cliquez ensuite sur **[!UICONTROL Add a public key]**.

   ![](../assets/create-account-9.png)

   - Ajoutez la variable [!DNL MBI] `SSH Public Key` du haut.

   ![](../assets/create-account-10.png)

1. Fournir [!DNL MBI] Informations d’identification MySQL.

   - Mettez à jour votre `.magento/services.yaml`

   ```sql
   mysql:
       type: mysql:10.0
       disk: 2048
       configuration:
           schemas:
               - main
           endpoints:
               mysql:
                   default_schema: main
                   privileges:
                       main: admin
               mbi:
                   default_schema: main
                   privileges:
                       main: ro
   ```

   - Mettez à jour votre `.magento.app.yaml`

   ```sql
           relationships:
               database: "mysql:mysql"
               mbi: "mysql:mbi"
               redis: "redis:redis"
   ```

1. Obtenir des informations sur la connexion de votre base de données à [!DNL MBI].

   Exécuter
   `echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 --decode | json_pp`

   pour obtenir des informations sur la connexion à votre base de données.

   Vous devriez recevoir des informations similaires à la sortie ci-dessous :

   ```json
           "mbi" : [
                 {
                    "scheme" : "mysql",
                    "rel" : "mbi",
                    "cluster" : "vfbfui4vmfez6-master-7rqtwti",
                    "query" : {
                       "is_master" : true
                    },
                    "ip" : "169.254.169.143",
                    "path" : "main",
                    "host" : "[!DNL MBI].internal",
                    "hostname" : "3m7xizydbomhnulyglx2ku4wpq.mysql.service._.magentosite.cloud",
                    "username" : "mbi",
                    "service" : "mysql",
                    "port" : 3306,
                    "password" : "[password]"
                 }
              ],
   ```

1. Connexion à votre base de données Commerce

   ![](../assets/create-account-11.png)

   - `Integration Name`: [Choisissez un nom pour votre intégration.]

   - `Host`: `[!DNL MBI].internal`

   - `Port`: `3306`

   - `Username`: `mbi`

   - `Password`: [mot de passe d’entrée fourni dans la sortie pour l’étape 8.]

   - `Database Name`: `main`

   - `Table Prefixes`: [laisser vide s’il n’y a aucun préfixe de tableau]

1. Définissez les paramètres de fuseau horaire.

   ![Entrées](../assets/create-account-12.png)

   - `Database`: `Timezone: UTC`

   - `Desired Timezone`: [Sélectionnez le fuseau horaire dans lequel vos données doivent s’afficher.]

1. Obtenez des informations sur vos paramètres de chiffrement.

   - L’interface utilisateur du projet fournit une `SSH` Chaîne d’accès. Cette chaîne peut être utilisée pour collecter les informations nécessaires pour `Remote Address` et `Username` lors de la configuration de `Encryption` paramètres. Utilisez la variable `SSH Access` chaîne trouvée en cliquant sur le bouton d’accès au site sur votre branche de Principal de votre interface utilisateur de projet et en recherchant votre `User Name` et `Remote Address` comme illustré ci-dessous.

   ![](../assets/create-account-13.png)

   ![](../assets/create-account-14.png)

1. Informations d’entrée pour votre `Encryption` paramètres

   ![](../assets/create-account-15.png)

   **Entrées**

   - `Encryption Type`: `SSH Tunnel`

   - `Remote Address`: `ssh.us-3.magento.cloud`

   - `Username`: `vfbfui4vmfez6-master-7rqtwti--mymagento`

   - `Port`: `22`

1. Cliquez sur **[!UICONTROL Save Integration]**.

1. Vous êtes maintenant connecté à votre [!DNL MBI] compte .

1. Une fois que vous êtes connecté [!DNL MBI] dans votre base de données Commerce, contactez votre équipe de compte d’Adobe pour coordonner les étapes suivantes, telles que la configuration des intégrations et d’autres étapes de configuration.

1. Une fois la configuration terminée, vous pouvez [connexion](../getting-started/sign-in.md) à [!DNL MBI] compte .
