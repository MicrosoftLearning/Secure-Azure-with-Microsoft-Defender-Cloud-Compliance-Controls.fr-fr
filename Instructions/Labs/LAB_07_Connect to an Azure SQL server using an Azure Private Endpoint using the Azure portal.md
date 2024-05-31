---
lab:
  title: Exercice 07 - Se connecter à un serveur Azure SQL à l’aide d’un point de terminaison privé Azure à l’aide du portail Azure
  module: Module 08 - Connect to an Azure SQL server using an Azure Private Endpoint using the Azure portal
---


>**Remarque** : pour suivre ce labo, vous devez disposer d’un [abonnement Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) où vous disposez de droits d’accès administratif. 


Azure Private Endpoint est le composant fondamental de Private Link dans Azure. Il permet aux ressources Azure, comme les machines virtuelles, de communiquer en privé et en toute sécurité avec les ressources Private Link comme le serveur Azure SQL.

---

## Tâches d'apprentissage

- Créer un réseau virtuel et un hôte Azure bastion.
  
- Création d’une machine virtuelle
  
- Créer un serveur Azure SQL et un point de terminaison privé
  
- Tester la connectivité au point de terminaison privé du serveur SQL

## Instructions de l’exercice 

### Créez un groupe de ressources et un réseau virtuel.

>**Remarque** : L’hôte bastion sera utilisé pour se connecter de façon sécurisée à la machine virtuelle afin de tester le point de terminaison privé.

1. Démarrez une session de navigateur et connectez-vous au [menu du Portail Azure.](https://portal.azure.com/)
   
2. Dans le menu du portail Azure, sélectionnez + **Créer une ressource** > **Mise en réseau** > **Réseau virtuel** ou recherchez Réseau virtuel dans la zone de recherche du portail.

3. Sélectionnez **Créer**.

4. Sous l’onglet **Informations de base** de la page **Créer un réseau virtuel**, entrez ou sélectionnez les informations suivantes :
   
   |Paramètre|Valeur|
   |---|---|
   |**Détails du projet**|
   |Abonnement|Sélectionnez votre abonnement.|
   |Resource group|Sélectionnez **Créer nouveau**. Entrez **CreateSQLEndpointTutorial.** Sélectionnez **OK**.|
   |**Détails de l’instance**|
   |Nom du réseau virtuel|Entrez **myVNet1a.**|
   |Région|Sélectionnez **(États-Unis) USA Est**.|  
    
5. Sélectionnez **Suivant** pour passer à l’onglet **Sécurité**.
  
6. Sélectionnez **Activer Azure Bastion** dans la section Azure Bastion de l’onglet Sécurité.

   >**Remarque** : Azure Bastion utilise votre navigateur pour vous connecter à des machines virtuelles dans votre réseau virtuel via un Secure Shell (SSH) ou un protocole RDP (Remote Desktop Protocol) à l’aide de leurs adresses IP privées. Les machines virtuelles ne requièrent pas d’adresse IP publique, de logiciel client ou de configuration spéciale.

7. Entrez ou sélectionnez les informations suivantes dans le champ **nom d’hôte Azure Bastion** :

   |Paramètre|Valeur|
   |---|---|
   |Nom d’hôte Azure Bastion|Entrez **mybastionhost**|
   |Nom d’adresse IP publique Azure Bastion|Sélectionner **Créer une adresse IP publique**|
   |Ajouter une adresse IP publique|Entrer **my-bstn-public-ip**|
   |SKU|Conservez la valeur par défaut **Standard**.|
   
8. Cliquez sur **OK**.

9. Sélectionnez **Suivant** pour passer à l’onglet **Sécurité**.

10. Sélectionnez **Suivant** pour passer à l’onglet **adresses IP**.

11. Dans la zone d’espace d’adressage de la colonne Sous-réseaux, sélectionnez le mot sous-réseau **par défaut** .

12. Dans le modèle **Modifier sous-réseau**, entrez ou sélectionnez les informations suivantes :

   |Paramètre|Valeur|
   |---|---|
   |Objectif du sous-réseau|Conservez la valeur par défaut de **Valeur par défaut**.|
   |Nom|Entrer **mysubnet1a**|
   |Plage d'adresses IPv4|Conserver la valeur par défaut  de **10.0.0/16**|
   |Adresse de début|Conserver la valeur par défaut **/24 (256 adresses**|

13. Sélectionnez **Enregistrer**.

14. Sélectionnez **Vérifier + créer** dans la partie inférieure de l’écran, puis une fois la validation réussie, sélectionnez **Créer**.

    >**Remarque** : Le déploiement de Bastion peut prendre jusqu’à 15 minutes pour atteindre l’instanciation complète.
 
### Créez une machine virtuelle.

>**Remarque** : dans cette tâche, vous allez créer une machine virtuelle qui sera utilisée pour tester le point de terminaison privé.

1. Dans le menu du portail Azure, sélectionnez + **Créer une ressource** > **Calcul** > **Machine virtuelle** ou, dans la zone de recherche de ce portail, recherchez **Machine virtuelle**.
   
2. Dans **Créer une machine virtuelle**, entrez ou sélectionnez les valeurs sous l’onglet **Informations de base** :

   |Paramètre|Valeur|
   |---|---|
   |**Détails du projet**|
   |Abonnement|Sélectionnez votre abonnement|
   |Resource group|Sélectionnez **CreateSQLEndpointTutorial**.|
   |**Détails de l’instance**|
   |Nom de la machine virtuelle|Entrez **myVM**.|
   |Région|Sélectionnez **(États-Unis) USA Est**.|
   |Options de disponibilité|Dans le menu déroulant Zone de disponibilité, sélectionnez **Aucune redondance d’infrastructure requise**.|
   |Type de sécurité|Dans le menu déroulant Type de sécurité, sélectionnez **Standard**.|
   |Image|Sélectionnez **Windows Server 2022 Datacenter - x64 Gen2**.|
   |Architecture de machine virtuelle|Sélectionnez **x64**.|
   |Exécuter avec la remise Azure Spot|Conservez la valeur par défaut de la case non cochée.|
   |Taille|Conservez la valeur par défaut de **Standard_D2s_v3-2 vcpus, 8 Go de mémoire.**|
   |**Compte administrateur**|
   |Type d'authentification|Sélectionnez **Mot de passe**.|
   |Nom d’utilisateur|Entrez **Tenantadmin2.**|
   |Mot de passe|Entrez **Superuser#170.**|
   |Confirmer le mot de passe|Ressaisissez **Superuser#170.**|
   |**Règles des ports d’entrée**|
   |Sélectionner des ports d’entrée|Sélectionnez **Aucun**.|

4. Sélectionnez l'onglet **Mise en réseau** ou choisissez **Suivant : Disques**, puis **Suivant : Mise en réseau**.
  
5. Sous l’onglet **Réseau**, entrez ou sélectionnez les informations suivantes :

   |Paramètre|Valeur|
   |---|---|
   |**Interface réseau**|
   |Réseau virtuel|Sélectionnez **myVNet1a.**|
   |Sous-réseau|Sélectionnez **mySubnet1a.**|
   |Adresse IP publique|Sélectionnez **Aucun**.|
   |Groupe de sécurité réseau de la carte réseau|Sélectionnez **De base**.|
   |Aucun port d’entrée public|Sélectionnez **Aucun**.|
  
6. Sélectionnez **Revoir + créer**.

7. Passez en revue les paramètres, puis sélectionnez **Créer**.

### Créer un serveur SQL Azure et un point de terminaison privé

>**Remarque** : dans cette tâche, vous allez créer un serveur SQL Server dans Azure.

1. Dans le menu du portail Azure, sélectionnez + **Créer une ressource** > **Bases de données** > **Base de données SQL.**
   
2. Sous l’onglet **De base** de la page **Créer une base de données SQL**, entrez ou sélectionnez les informations suivantes :

   |Paramètre|Valeur|
   |---|---|
   |**Détails du projet**|
   |Abonnement|Sélectionnez votre abonnement.|
   |Resource group|Sélectionnez **CreateSQLEndpointTutorial**.|
   |**Détails de la base de données**|
   |Nom de la base de données|Entrez **mysqldatabase**.|
   |Serveur|Sélectionnez **Créer nouveau**.|  

3. Dans **Créer un serveur de base de données SQL**, entrez ou sélectionnez les informations suivantes :
  
   |Paramètre|Value|
   |---|---|
   |**Détails du serveur**|
   |Nom du serveur|Entrez **mysqlserver1a.** Si ce nom est utilisé, créez un nom unique.|
   |Emplacement|Sélectionnez **(États-Unis) USA Est**.|
   |**Authentification**|
   |Méthode d'authentification|Sélectionnez **Utiliser l’authentification SQL**.|
   |Connexion d’administrateur du serveur|Entrez **Tenantadmin2.**|
   |Mot de passe|Entrez **Superuser#170.**|
   |Confirmez le mot de passe.|Entrez **Superuser#170.**|

4. Cliquez sur **OK**.
   
   |Paramètre|Valeur|
   |---|---|
   |**Détails de la base de données**|
   |Vous souhaitez utiliser un pool élastique SQL ?|Sélectionnez **Non**.|
   |Calcul + stockage|Prenez les paramètres par défaut ou sélectionnez **Configurer la base de données** pour configurer les paramètres de calcul et de stockage.|
   |**Redondance du stockage de sauvegarde**|
   |Redondance du stockage de sauvegarde|Sélectionnez **Stockage de sauvegarde redondant localement**.|
   
5. Sélectionnez l’onglet **Mise en réseau** ou sélectionnez **Suivant : Réseau**.

6. Sous l’onglet **Réseau**, entrez ou sélectionnez les informations suivantes :

   |Paramètre|Valeur|
   |---|---|
   |**Connectivité réseau**|
   |Méthode de connexion|Sélectionnez **Point de terminaison privé**.|

7. Sélectionnez **+ Ajouter un point de terminaison privé** dans **Points de terminaison privés**.

8. Dans **Créer un point de terminaison privé**, entrez ou sélectionnez les informations suivantes :

   |Paramètre|Valeur|
   |---|---|
   |Abonnement|Sélectionnez votre abonnement.|
   |Resource group|Sélectionnez **CreateSQLEndpointTutorial**.|
   |Emplacement|Sélectionnez **USA Est**.|
   |Name|Entrez **myPrivateSQLendpoint**.|
   |Sous-ressource cible|Conservez la valeur par défaut **SqlServer**.|
   |**Mise en réseau**|
   |Réseau virtuel|Sélectionnez **myVNet1a.**|
   |Sous-réseau|Sélectionnez **mySubnet1a.**|
   |**Intégration à un DNS privé**|
   |Intégrer à une zone DNS privée|Conservez la valeur par défaut **Oui**.|
   |Zone DNS privée|Laissez la valeur par défaut **(Nouveau) privatelink.database.windows.net**.|

 9. Cliquez sur **OK**.

 10. Sélectionnez **Revoir + créer**.

 11. Sélectionnez **Create** (Créer).

### Désactiver l’accès public au serveur logique Azure SQL

>**Remarque** : pour cette tâche, supposons que vous souhaitez désactiver tout accès public à votre serveur Azure SQL et autoriser uniquement les connexions depuis votre réseau virtuel.

1. Dans la zone de recherche du portail Azure, entrez **mysqlserver** ou le nom du serveur que vous avez saisi dans les étapes précédentes.

2. Dans la page **Mise en réseau**, sélectionnez l’onglet **Accès public**, puis **Désactiver** pour l’**Accès au réseau public**.

   ![image](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/44ff5c24-70cf-49ed-b2ab-5e210c478b3a)


4. Sélectionnez **Enregistrer**.

### Tester la connectivité au point de terminaison privé

>**Remarque** : dans cette tâche, vous allez utiliser la machine virtuelle que vous avez créée aux étapes précédentes pour vous connecter au serveur SQL Server via le point de terminaison privé.

1. Dans le volet de navigation de gauche, sélectionnez **Groupes de ressources**.

2. Sélectionnez **CreateSQLEndpointTutorial**.

3. Sélectionnez **myVM**.

4. Sur la page de présentation pour **myVM,** sélectionnez Se connecter, puis **Bastion.**

5. Entrez le nom d’utilisateur **Tenantadmin2** et le mot de passe **Superuser#170** que vous avez utilisés lors de la création de la machine virtuelle.

   **Important :** accédez aux paramètres Edge/fenêtres contextuelles et redirections et basculez le commutateur bloqué sur **désactivé** avant de sélectionner Connecter.

7. Sélectionnez le bouton **Connecter**.
  
8. Ouvrez Windows PowerShell sur le serveur après vous être connecté.

9. Entrez `nslookup sqlserver-name.database.windows.net.` Remplacez **sqlserver-name** par le nom du serveur SQL Server que vous avez créé aux étapes précédentes. Vous recevez un message similaire à ce qui est montré ci-dessous :

   ````  
   Server:  UnKnown
   Address:  168.63.129.16
   
   Non-authoritative answer:
   Name:    mysqlserver1a.privatelink.database.windows.net
   Address:  10.1.0.5
   Aliases:  mysqlserver1a.database.windows.net
   ````
    
>**Remarque**: une adresse IP privée 10.1.0.5 a été renvoyée pour le nom du serveur SQL Server. Cette adresse se trouve dans le sous-réseau **mySubnet1a** du réseau virtuel **myVNet1a** que vous avez créé précédemment.

9. Installez [SQL Server Management Studio](https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?preserve-view=true&view=sql-server-2017) sur **myVM**.
 
10. Ouvrez **SQL Server Management Studio**.

11. Dans **Se connecter au serveur**, entrez ou sélectionnez les informations suivantes :

    |Paramètre|Valeur|
    |---|---|
    |Type de serveur|Sélectionnez **Moteur de base de données**.|
    |Nom du serveur|Entrez **sqlserver1a.database.windows.net.**|
    |Authentification|Sélectionnez **Authentification SQL Server**.|
    |Nom d’utilisateur|Entrez **Tenantadmin2**.|
    |Mot de passe|Entrez **Superuser#170**.|
    |Se souvenir du mot de passe|Sélectionnez **Oui**.|
   
12. Sélectionnez **Se connecter**.

13. Parcourez les bases de données dans le menu de gauche.

14. (Facultatif) Créez ou interrogez des informations à partir de mysqldatabase.

15. Fermez la connexion Bureau à distance à myVM.
  
> **Résultats** : vous vous êtes connecté(e) à un serveur Azure SQL via un point de terminaison privé Azure en utilisant le Portail Azure
