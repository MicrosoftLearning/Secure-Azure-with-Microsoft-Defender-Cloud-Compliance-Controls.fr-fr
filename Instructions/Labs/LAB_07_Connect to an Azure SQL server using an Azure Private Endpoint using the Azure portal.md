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
   |Hôte Azure Bastion |Saisissez **az-bastionhost-1a**.|
   |Nom d’adresse IP publique Azure Bastion|Sélectionner **Créer une adresse IP publique**|
   |Ajouter une adresse IP publique|Sélectionnez **OK**.|

8. Sélectionnez **Suivant** pour passer à l’onglet **adresses IP**.

9. Dans la zone d’**espace d’adressage IPv4** configurée existante dans la colonne **Sous-réseaux**, cliquez sur l’entrée **par défaut**.

10. Dans le modèle **Modifier sous-réseau**, entrez ou sélectionnez les informations suivantes :

    |Paramètre|Valeur|
    |---|---|
    |Objectif du sous-réseau|Utilisez le paramètre par défaut « Par défaut ».|
    |Nom|**subnet-2**|
    |Inclure un espace d’adressage IPv4|Laissez le paramètre par défaut coché.|
    |Plage d'adresses IPv4|Utilisez le paramètre par défaut « 10.0.0.0/16 ».|
    |Adresse de début|10.0.0.0.|
    |Taille|Utilisez le paramètre par défaut « /24 » (256 adresses).|
    |Plage d’adresses de sous-réseau|10.0.0.0-10.0.0.255.|

11. En bas de la page **Modifier le sous-réseau**, sélectionnez **Enregistrer**.

12. En bas de la page **Adresses IP**, sélectionnez **Examiner et créer**.

13. En bas de la page **Examiner et créer**, sélectionnez **Créer**.

>**Remarque** : Le déploiement de Bastion peut prendre jusqu’à 15 minutes pour atteindre l’instanciation complète.
 
### Créez une machine virtuelle.

>**Remarque** : dans cette tâche, vous allez créer une machine virtuelle qui sera utilisée pour tester le point de terminaison privé.

1. Dans le portail, recherchez et sélectionnez **Machines virtuelles**.

2. Dans **Machines virtuelles**, sélectionnez **+ Créer**, puis **Machine virtuelle Azure**.

3. Dans Créer une machine virtuelle, saisissez ou sélectionnez les informations suivantes sur la page **Informations de base** :

   |Paramètre|Valeur|
   |---|---|
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
   |Aucun port d’entrée public|Sélectionnez **Aucun**.|
   |Sélectionner des ports d’entrée|Le paramètre par défaut est grisé.|

4. Sélectionnez **Suivant : Disques**, puis **Suivant : Réseaux**.
  
5. Sur la page **Mise en réseau**, saisissez ou sélectionnez les informations suivantes :

   |Paramètre|Valeur|
   |---|---|
   |**Interface réseau**|
   |Réseau virtuel|Sélectionnez **vnet-2**.|
   |Sous-réseau|Utilisez le paramètre par défaut subnet-2 (10.0.0.0/24).|
   |IP publique|Utilisez le paramètre par défaut (new) vm-3-ip.|
   |Groupe de sécurité réseau de la carte réseau|Utilisez le paramètre par défaut « Aucun ».|
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
   |Abonnement|Sélectionnez votre abonnement.|
   |Resource group|Sélectionnez **az-rg-1**.|
   |**Détails de la base de données**|
   |Nom de la base de données|Saisissez **az-sql-db1a**.|
   |Serveur|Sélectionnez **Créer nouveau**.|
   |**Détails du serveur**|
   |Nom du serveur|Saisissez **az-sql-svr1a**.|
   |Emplacement|Utilisez le paramètre par défaut « USA Est ».|
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

7. Dans la section **Points de terminaison privés**, sélectionnez **+ Ajouter un point de terminaison privé**.

8. Sélectionnez **Revoir + créer**.

9. Sélectionnez **Créer**.

10. Dans **Créer un point de terminaison privé**, entrez ou sélectionnez les informations suivantes :

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

12. Cliquez sur **OK**.

13. Sélectionnez **Revoir + créer**.

14. Sélectionnez **Créer**.

>**Remarque** : le déploiement du serveur Azure SQL et du point de terminaison privé peut prendre jusqu’à 10 minutes pour une instanciation complète.

### Autoriser certaines adresses IP Internet publiques à accéder à votre serveur logique Azure SQL

>**Remarque** : pour cette tâche, supposons que vous souhaitez activer l’accès public à votre serveur Azure SQL et autoriser uniquement les connexions depuis votre réseau virtuel. Le paramètre Accès public peut être défini par défaut sur **Désactivé**.

1. Dans la zone de recherche du portail Azure, saisissez **az-sql-srv1a** ou le nom du serveur que vous avez saisi lors des étapes précédentes.
   
2. Sélectionnez **Mise en réseau** dans la section **Sécurité** d’**az-sql-svr1a**.
  
3. Sur la page **Mise en réseau**, sélectionnez l’onglet **Accès public**.
  
4. Vérifiez si **Accès au réseau public** est désactivé. S’il est désactivé, sélectionnez **Réseaux sélectionnés** pour Accès au réseau public.

>**Remarque** : les connexions provenant des adresses IP configurées dans la section Règles du pare-feu ci-dessous auront accès à cette base de données. Par défaut, aucune adresse IP publique n’est autorisée.

5. Si nécessaire, accédez à la section **Règles du pare-feu** de la page **Mise en réseau**, puis sélectionnez **+ Ajouter l’adresse IPv4 de votre client** si l’adresse IP de votre client n’est pas déjà renseignée dans les champs **Nom de la règle**, **Adresse IPv4 de début** et **Adresse IPv4 de fin**.

   ![image](https://github.com/user-attachments/assets/fff5bfb1-53fd-40ea-9a31-5a095e7f3dbc) 

7. Sélectionnez **Enregistrer**.

### Tester la connectivité au point de terminaison privé

>**Remarque** : dans cette tâche, vous allez utiliser la machine virtuelle que vous avez créée aux étapes précédentes pour vous connecter au serveur SQL Server via le point de terminaison privé.

1. Dans la zone de recherche du portail Azure, tapez **vm-3**, puis sélectionnez-la dans la liste déroulante Ressources.

2. Sur la page **Présentation** de vm-3, sélectionnez **Se connecter**, puis **Bastion**.

3. Entrez le nom d’utilisateur **Tenantadmin2** et le mot de passe **Superuser#170** que vous avez utilisés lors de la création de la machine virtuelle.

   **Important :** Important : accédez aux paramètres Edge, puis aux **fenêtres contextuelles et redirections.** Sélectionnez l’option radiale intitulée **Toujours autoriser les fenêtres contextuelles et les redirections depuis https://portal.azure.com,** puis cliquez sur **Terminé.**

4. Sélectionnez le bouton **Connecter**.
  
5. Ouvrez Windows PowerShell sur le serveur après vous être connecté.

6. Pour vérifier la résolution de noms du point de terminaison privé, entrez la commande suivante dans la fenêtre du terminal :

   ```bash
   nslookup server-name.database.windows.net

>**Note**: Replace **sqlserver-name** with the name of the SQL server you created in the previous steps. For example, enter **nslookup az-sql-srv1a.database.windows.net** You’ll receive a message similar to the one shown below:

   ````
   
   Server:  UnKnown Address:  168.63.129.16
   
   Non-authoritative answer: Name:    az-sql-srv1a.privatelink.database.windows.net Address:  10.1.0.5 Aliases:  az-sql-srv1a.database.windows.net
   ````
   
>**Note**: A  private IP address of 10.1.0.5 is returned for the SQL server name. This address is in **az-sql-srv1a** subnet of **vnet-2** virtual network you created previously.

7. Install [SQL Server Management Studio (SSMS)](https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?preserve-view=true&amp;view=sql-server-2017) on **vm-3.**
 
8. Open **SQL Server Management Studio.**

9. In **Connect to server,** enter or select this information:

    |Setting|Value|
    |---|---|
    |Server type|Leave the default setting as Database Engine.|
    |Server name|Enter **az-sql-srv1a.database.windows.net.**|
    |Authentication|Select **SQL Server Authentication.**|
    |User name|Enter **Tenantadmin2**.|
    |Password|Enter **Superuser#170**.|
    |Remember password|Select **Yes.**|
    |Connectivity Security|
    |Encryption|Leave the default setting as Mandatory.|
   
10. Select **Connect.**

11. Browse databases from left menu.

12. Close the remote desktop connection to vm-3.
  
> **Results**: You have connected to an Azure SQL server using an Azure Private Endpoint using the Azure portal.
