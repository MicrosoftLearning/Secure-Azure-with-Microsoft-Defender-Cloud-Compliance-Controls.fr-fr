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
   
2. Dans la zone de recherche située en haut du portail, entrez **Réseaux virtuels.** Sélectionnez **Réseaux virtuels** dans les résultats de la recherche.

3. Dans la page **Réseaux virtuels**, sélectionnez **+ Créer**.

4. Sous l’onglet **Informations de base** de la page **Créer un réseau virtuel**, entrez ou sélectionnez les informations suivantes :
   
   |Paramètre|Valeur|
   |---|---|
   |**Détails du projet**|
   |Abonnement|Sélectionnez votre abonnement.|
   |Resource group|Sélectionnez **az-rg-1**.|
   |**Détails de l’instance**|
   |Nom du réseau virtuel|Saisissez **vnet-2**.|
   |Région|Sélectionnez **(États-Unis) USA Est**.|  
    
5. Sélectionnez **Suivant** pour passer à l’onglet **Sécurité**.
  
6. Sélectionnez **Activer Azure Bastion** dans la section Azure Bastion de l’onglet Sécurité.

   >**Remarque** : Azure Bastion est un service payant qui fournit une connectivité RDP/SSH sécurisée à vos machines virtuelles via TLS. Lorsque vous vous connectez via Azure Bastion, vos machines virtuelles n’ont pas besoin d’une adresse IP publique. 

7. Saisissez ou sélectionnez les informations suivantes dans le champ **Azure Bastion** :

   |Paramètre|Valeur|
   |---|---|
   |**Détails du projet**|
   |Hôte Azure Bastion |Saisissez **az-bastionhost-1a**.|
   |Nom d’adresse IP publique Azure Bastion|Sélectionner **Créer une adresse IP publique**|
   |Ajouter une adresse IP publique|Sélectionnez **OK**.|

9. Sélectionnez **Suivant** pour passer à l’onglet **adresses IP**.

10. Dans la zone d’**espace d’adressage IPv4** configurée existante dans la colonne **Sous-réseaux**, cliquez sur l’entrée **par défaut**.

11. Dans le modèle **Modifier sous-réseau**, entrez ou sélectionnez les informations suivantes :

    |Paramètre|Valeur|
    |---|---|
    |**Détails du projet**|
    |Objectif du sous-réseau|Utilisez le paramètre par défaut « Par défaut ».|
    |Nom|**subnet-2**|
    |Plage d'adresses IPv4|Utilisez le paramètre par défaut « 10.0.0.0/16 ».|
    |Adresse de début|Utilisez le paramètre par défaut « /24 » (256 adresses).|

13. En bas de la page **Modifier le sous-réseau**, sélectionnez **Enregistrer**.

14. En bas de la page **Adresses IP**, sélectionnez **Examiner et créer**.

    >**Remarque** : Le déploiement de Bastion peut prendre jusqu’à 15 minutes pour atteindre l’instanciation complète.

15. En bas de la page **Examiner et créer**, sélectionnez **Créer**.
 
### Créez une machine virtuelle.

>**Remarque** : dans cette tâche, vous allez créer une machine virtuelle qui sera utilisée pour tester le point de terminaison privé.

1. Dans le portail, recherchez et sélectionnez **Machines virtuelles**.

2. Dans **Machines virtuelles**, sélectionnez **+ Créer**, puis **Machine virtuelle Azure**.

3. Dans Créer une machine virtuelle, saisissez ou sélectionnez les informations suivantes sur la page **Informations de base** :

   |Paramètre|Valeur|
   |---|---|
   |**Détails du projet**|
   |Abonnement|Sélectionnez votre abonnement.|
   |Resource group|Sélectionnez **az-rg-1**.|
   |**Détails de l’instance**|
   |Nom de la machine virtuelle|Saisissez **vm-3**.|
   |Région|Sélectionnez **(États-Unis) USA Est**.|
   |Options de disponibilité|Dans le menu déroulant Zone de disponibilité, sélectionnez **Aucune redondance d’infrastructure requise**.|
   |Type de sécurité|Dans le menu déroulant Type de sécurité, sélectionnez **Standard**.|
   |Image|Sélectionnez **Windows Server 2022 Datacenter - x64 Gen2**.|
   |Architecture de machine virtuelle|Sélectionnez **x64**.|
   |Exécuter avec la remise Azure Spot|Laissez le paramètre par défaut non coché.|
   |Taille|Utilisez le paramètre par défaut « Standard_D2s_v3-2 vcpus, 8 Go de mémoire ».|
   |**Compte administrateur**|
   |Nom d’utilisateur|Entrez **Tenantadmin2.**|
   |Mot de passe|Entrez **Superuser#170.**|
   |Confirmer le mot de passe|Ressaisissez **Superuser#170.**|
   |**Règles des ports d’entrée**|
   |Sélectionner des ports d’entrée|Sélectionnez **Aucun**.|

5. Sélectionnez **Suivant : Disques**, puis **Suivant : Réseaux**.
  
6. Sur la page **Mise en réseau**, saisissez ou sélectionnez les informations suivantes :

   |Paramètre|Valeur|
   |---|---|
   |**Interface réseau**|
   |Réseau virtuel|Sélectionnez **vnet-2**.|
   |Sous-réseau|Sélectionnez **subnet-2 (10.0.0.0/24)**.|
   |Adresse IP publique|Sélectionnez **Aucun**.|
   |Groupe de sécurité réseau de la carte réseau|Sélectionnez **De base**.|
   |Aucun port d’entrée public|Sélectionnez **Aucun**.|
   |Sélectionner des ports d’entrée|Laissez la valeur par défaut vide.|
   |Supprimer la carte réseau lors de la suppression de la machine virtuelle|Laissez le paramètre par défaut « Activer la mise en réseau accélérée » coché.|
   |Équilibrage de charge|Utilisez le paramètre par défaut « Aucun ».|
  
6. Sélectionnez **Revoir + créer**.

7. Passez en revue les paramètres, puis sélectionnez **Créer**.

### Créer un serveur SQL Azure et un point de terminaison privé

>**Remarque** : dans cette tâche, vous allez créer un serveur SQL Server dans Azure.

1. Dans la zone de recherche en haut du portail, saisissez **Base de données SQL**. Sélectionnez **Bases de données SQL** dans les résultats de la recherche.

2. Sur la page **Bases de données SQL**, sélectionnez **+ Créer**.
   
3. Sous l’onglet **De base** de la page **Créer une base de données SQL**, entrez ou sélectionnez les informations suivantes :

   |Paramètre|Valeur|
   |---|---|
   |**Détails du projet**|
   |Abonnement|Sélectionnez votre abonnement.|
   |Resource group|Sélectionnez **az-rg-1**.|
   |**Détails de la base de données**|
   |Nom de la base de données|Saisissez **az-sql-db1a**.|
   |Nom du serveur|Saisissez **az-sql-svr1a**. Si ce nom est utilisé, créez un nom unique.|
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
   |Vous souhaitez utiliser un pool élastique SQL ?|Utilisez le paramètre par défaut « Non ».|
   |Environnement de la charge de travail|Utilisez le paramètre par défaut « Développement ».|
   |Calcul + stockage|Utilisez le paramètre par défaut « Usage général - Serverless ».|
   |**Redondance du stockage de sauvegarde**|
   |Redondance du stockage de sauvegarde|Sélectionnez **Stockage de sauvegarde redondant localement**.|
   
5. Sélectionnez l’onglet **Mise en réseau** ou sélectionnez **Suivant : Réseau**.

6. Sous l’onglet **Réseau**, entrez ou sélectionnez les informations suivantes :

   |Paramètre|Valeur|
   |---|---|
   |**Connectivité réseau**|
   |Méthode de connexion|Sélectionnez **Point de terminaison privé**.|
   |Stratégie de connexion|Laissez le paramètre par défaut sur « Par défaut » - Utilise la stratégie de redirection pour toutes les connexions client provenant d’Azure (sauf les connexions de points de terminaison privés) et un proxy pour toutes les connexions client provenant de l’extérieur d’Azure.|
   |Connexions de chiffrement|Utilisez le paramètre par défaut « TLS.12 ».|

7. Sélectionnez **+ Ajouter un point de terminaison privé** dans **Points de terminaison privés**.

8. Dans **Créer un point de terminaison privé**, entrez ou sélectionnez les informations suivantes :

   |Paramètre|Valeur|
   |---|---|
   |Abonnement|Sélectionnez votre abonnement.|
   |Resource group|Sélectionnez **az-rg-1**.|
   |Emplacement|Sélectionnez **USA Est**.|
   |Nom|Saisissez **az-pe-1a**.|
   |Sous-ressource cible|Utilisez le paramètre par défaut « SqlServer ».|
   |**Mise en réseau**|
   |Réseau virtuel|Sélectionnez **vnet-2**.|
   |Sous-réseau|Sélectionnez **subnet-2**.|
   |**Intégration à un DNS privé**|
   |Intégrer à une zone DNS privée|Utilisez le paramètre par défaut « Oui ».|
   |Zone DNS privée|Utilisez la valeur par défaut (Nouveau) privatelink.database.windows.net.|

9. Cliquez sur **OK**.

10. Sélectionnez **Revoir + créer**.

11. Sélectionnez **Create** (Créer).

### Désactiver l’accès public au serveur logique Azure SQL

>**Remarque** : pour cette tâche, supposons que vous souhaitez désactiver tout accès public à votre serveur Azure SQL et autoriser uniquement les connexions depuis votre réseau virtuel. Le paramètre **Accès public** peut être défini par défaut sur **Désactivé**.

1. Dans la zone de recherche du portail Azure, saisissez **az-sql-svr1a** ou le nom du serveur que vous avez saisi lors des étapes précédentes.

2. Sélectionnez **Mise en réseau** dans la section **Sécurité** d’**az-sql-svr1a**. Dans la page **Mise en réseau**, sélectionnez l’onglet **Accès public**, puis **Désactiver** pour l’**Accès au réseau public**.

   ![image](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/44ff5c24-70cf-49ed-b2ab-5e210c478b3a)

3. Sélectionnez **Enregistrer**.

### Tester la connectivité au point de terminaison privé

>**Remarque** : dans cette tâche, vous allez utiliser la machine virtuelle que vous avez créée aux étapes précédentes pour vous connecter au serveur SQL Server via le point de terminaison privé.

1. Dans le volet de navigation de gauche, sélectionnez **Groupes de ressources**.

2. Sélectionnez **az-rg-1**.

3. Sélectionnez **vm-3**.

4. Sur la page Vue d’ensemble de **vm-3**, sélectionnez Se connecter, puis **Bastion**.

5. Entrez le nom d’utilisateur **Tenantadmin2** et le mot de passe **Superuser#170** que vous avez utilisés lors de la création de la machine virtuelle.

   **Important :** accédez aux paramètres Edge/fenêtres contextuelles et redirections et basculez le commutateur bloqué sur **désactivé** avant de sélectionner Connecter.

7. Sélectionnez le bouton **Connecter**.
  
8. Ouvrez Windows PowerShell sur le serveur après vous être connecté.

9. Entrez `nslookup sqlserver-name.database.windows.net.` Remplacez **sqlserver-name** par le nom du serveur SQL Server que vous avez créé aux étapes précédentes. Vous recevez un message similaire à ce qui est montré ci-dessous :

   ````  
   Server:  UnKnown
   Address:  168.63.129.16
   
   Non-authoritative answer:
   Name:    az-sql-svr1a.privatelink.database.windows.net
   Address:  10.1.0.5
   Aliases:  az-sql-svr1a.database.windows.net
   ````
    
>**Remarque**: une adresse IP privée 10.1.0.5 a été renvoyée pour le nom du serveur SQL Server. Cette adresse se trouve dans le sous-réseau **az-sql-svr1a** du réseau virtuel **vnet-2** que vous avez créé précédemment.

9. Installez [SQL Server Management Studio](https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?preserve-view=true&view=sql-server-2017) sur **vm-3**.
 
10. Ouvrez **SQL Server Management Studio**.

11. Dans **Se connecter au serveur**, entrez ou sélectionnez les informations suivantes :

    |Paramètre|Valeur|
    |---|---|
    |Type de serveur|Sélectionnez **Moteur de base de données**.|
    |Nom du serveur|Saisissez **az-sql-svr1a.database.windows.net**.|
    |Authentification|Sélectionnez **Authentification SQL Server**.|
    |Nom d’utilisateur|Entrez **Tenantadmin2**.|
    |Mot de passe|Entrez **Superuser#170**.|
    |Se souvenir du mot de passe|Sélectionnez **Oui**.|
    |Sécurisation de la connectivité|
    |Chiffrement|Utilisez le paramètre par défaut « Obligatoire ».|
   
13. Sélectionnez **Connecter**.

14. Parcourez les bases de données dans le menu de gauche.

15. Fermez la connexion du bureau à distance vers vm-3.
  
> **Résultats** : vous vous êtes connecté(e) à un serveur Azure SQL via un point de terminaison privé Azure en utilisant le Portail Azure
