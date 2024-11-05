---
lab:
  title: "Exercice 02\_: créer une infrastructure de réseau virtuel"
  module: Module 03 - Filter network traffic with a network security group using the Azure portal
---


>**Remarque** : pour suivre ce labo, vous devez disposer d’un [abonnement Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) où vous disposez de droits d’accès administratif. 


Vous pouvez utiliser un groupe de sécurité réseau pour filtrer le trafic réseau sortant et entrant respectivement à destination et en provenance de ressources Azure dans un réseau virtuel Azure. Les groupes de sécurité réseau contiennent des règles de sécurité qui filtrent le trafic réseau par adresse IP, port et protocole. Quand un groupe de sécurité réseau est associé à un sous-réseau, des règles de sécurité sont appliquées aux ressources déployées dans ce sous-réseau.

## Diagramme de l'architecture

![image](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/1bfec315-129b-48a9-9c35-1f21c837068f)

---

## Tâches d'apprentissage

- Créez un groupe de sécurité réseau et des règles de sécurité.
  
- Créez des groupes de sécurité d’application.
  
- Créez un réseau virtuel et associez un groupe de sécurité réseau à un sous-réseau.
  
- Déployez des machines virtuelles et associez leurs interfaces réseau aux groupes de sécurité d’application.

## Instructions de l’exercice 

### Créez un réseau virtuel et un groupe de ressources Azure.

>**Remarque** :la tâche suivante permet de créer un réseau virtuel et un sous-réseau de ressources.

1. Démarrez une session de navigateur et connectez-vous au [menu du Portail Azure.](https://portal.azure.com/)             
   
2. Dans la zone de recherche située en haut du portail, entrez **Réseaux virtuels.** Sélectionnez **Réseaux virtuels** dans les résultats de la recherche.

3. Dans la page **Réseaux virtuels**, sélectionnez **+ Créer**.

4. Sous l’onglet **Général** de la page **Créer un réseau virtuel**, entrez ou sélectionnez les informations suivantes :
   
   |Paramètre|Valeur|
   |---|---|
   |**Détails du projet**|
   |Abonnement|Sélectionnez votre abonnement.|
   |Resource group|Entrez **azure-rg-1.**|
   |**Détails de l’instance**|
   |Nom du réseau virtuel|Entrez **vnet-1**.|
   |Région|Sélectionnez **(États-Unis) USA Est**.|  
    
5. Sélectionnez **Suivant** pour passer à l’onglet **Sécurité**.
  
6. Sélectionnez **Suivant** pour passer à l’onglet **Adresses IP**.

7. Dans la zone Espace d’adressage sous **Sous-réseaux**, sélectionnez le sous-réseau **par défaut**.

8. Dans le modèle **Modifier sous-réseau**, entrez ou sélectionnez les informations suivantes :

   |Paramètre|Valeur|
   |---|---|
   |**Détails du sous-réseau**|
   |Objectif du sous-réseau|Utilisez le paramètre par défaut « Par défaut ».|
   |Nom|Entrez **subnet-1**.|
   |Adresse de début|Utilisez le paramètre par défaut « 10.0.0.0/16 ».|
   |Taille du sous-réseau|Utilisez le paramètre par défaut « /24 » (256 adresses).

   ![image](https://github.com/user-attachments/assets/4c5834f8-459f-4063-bd82-3e65237c6b1d)

10. Sélectionnez **Enregistrer**.

11. Sélectionnez **Vérifier + créer** dans la partie inférieure de l’écran, puis une fois la validation réussie, sélectionnez **Créer**.

    ![image](https://github.com/user-attachments/assets/4fd02061-2349-42c4-8582-c7178f9b7eb6)

### La création de groupes de sécurité d’application vous permet de regrouper des serveurs avec des fonctions similaires, tels que des serveurs Web.

Un groupe de sécurité d’application vous permet de regrouper des serveurs dont les fonctions sont similaires, comme des serveurs Web.

1. Dans la zone de recherche située en haut du portail, entrez **Groupe de sécurité application**. Dans les résultats de la recherche, sélectionnez **Groupes de sécurité d’application**.

2. Dans la page **Groupes de sécurité d’applications**, sélectionnez **+ Créer**.

3. Sur la page **Informations de base** de **Créer un groupe de sécurité d’applications**, saisissez ou sélectionnez les informations suivantes :
   
   |Paramètre|Valeur|
   |---|---|
   |**Détails du projet**|
   |Abonnement|Sélectionnez votre abonnement.|
   |Resource group|Sélectionnez **az-rg-1**.|
   |**Détails de l’instance**|
   |Nom|Entrez **asg-web**.|
   |Région|Sélectionnez **USA Est**.|  
    
4. Sélectionnez **Revoir + créer**.

5. Sélectionnez **Create** (Créer).

6. Répétez les étapes précédentes en spécifiant les valeurs suivantes :
    
   |Paramètre|Valeur|
   |---|---|
   |**Détails du projet**|
   |Abonnement|Sélectionnez votre abonnement.|
   |Resource group|Sélectionnez **az-rg-1**.|
   |**Détails de l’instance**|
   |Nom|Entrez **asg-mgmt**.|
   |Région|Sélectionnez **USA Est**.|

7. Sélectionnez **Revoir + créer**.

8. Sélectionnez **Create** (Créer).

### Créez un groupe de sécurité réseau pour sécuriser le trafic réseau sur votre réseau virtuel.

Un groupe de sécurité réseau (NSG) sécurise le trafic réseau dans votre réseau virtuel.

1. Dans la zone de recherche située en haut du portail, entrez **Groupe de sécurité réseau**. Dans les résultats de la recherche, sélectionnez **Groupe de sécurité réseau**.

>**Remarque** : dans les résultats de recherche pour Groupes de sécurité réseau, vous pouvez voir Groupes de sécurité réseau (classique). Sélectionnez Groupes de sécurité réseau.

2. Dans la page **Groupe de sécurité réseau**, sélectionnez **+ Créer**.

3. Dans **Créer un groupe de sécurité réseau**, sous l’onglet **De base**, entrez ou sélectionnez les informations suivantes :
   
   |Paramètre|Valeur|
   |---|---|
   |**Détails du projet**|
   |Abonnement|Sélectionnez votre abonnement.|
   |Resource group|Sélectionnez **az-rg-1**.|
   |**Détails de l’instance**|
   |Nom|Entrez **nsg-1**.|
   |Région|Sélectionnez **USA Est**.|  
    
4. Sélectionnez **Revoir + créer**.

5. Sélectionnez **Créer**.

### Associer le groupe de sécurité réseau au sous-réseau

>**Remarque** : dans cette tâche, vous allez associer le groupe de sécurité réseau au sous-réseau du réseau virtuel que vous avez créé précédemment.

1. Dans la zone de recherche située en haut du portail, entrez **Groupe de sécurité réseau**. Dans les résultats de la recherche, sélectionnez **Groupe de sécurité réseau**.
   
2. Sélectionnez **nsg-1**.

3. Dans la section **Paramètres** de **nsg-1**, sélectionnez **Sous-réseaux**.

4. Dans la page **nsg-1 | Sous-réseaux**, sélectionnez + **Associer :**

 ![image](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Defender-for-Cloud-regulatory-compliance-controls/assets/91347931/3b2004f6-963f-43df-9d05-3999d2e97d76)

5. Sous **Associer un sous-réseau**, sélectionnez **vnet-1 (az-rg-1)** pour **Réseau virtuel.**

6. Pour **Sous-réseau**, sélectionnez **subnet-1**, puis **OK**.

### Créez des règles de sécurité pour le groupe de sécurité réseau et le sous-réseau du réseau virtuel que vous avez créé précédemment.

1. Dans la section **Paramètres** de **nsg-1**, sélectionnez **Règles de sécurité de trafic entrant**.
   
2. Sur la page **nsg-1 | Règles de sécurité de trafic entrant**, sélectionnez + **Ajouter.**

3. Créez une règle de sécurité qui autorise les ports 80 et 443 dans le groupe de sécurité d’application **asg-web**. Dans la page **Ajouter une règle de sécurité de trafic entrant**, entrez ou sélectionnez les informations suivantes :

   |Paramètre|Valeur|
   |---|---|
   |Source|Conservez la valeur par défaut **Tous**.|
   |Source port ranges|Conservez les paramètres par défaut pour les plages de ports.|
   |Destination|Sélectionnez **Groupe de sécurité d’application**.|
   |Groupes de sécurité d’application de destination|Sélectionnez **asg-web**.|
   |Service|Utilisez le paramètre par défaut « Personnalisé ».|
   |Plages de ports de destination|Entrez **80,443**.|
   |Protocol|Sélectionnez **TCP**.|
   |Action|Utilisez le paramètre par défaut « Autoriser ».|
   |Priorité|Utilisez le paramètre par défaut « 100 ».|
   |Nom|Saisissez **allowweball**.|

4. Sélectionnez **Ajouter**.

5. Effectuez les étapes précédentes avec les informations suivantes :

   |Paramètre|Valeur|
   |---|---|
   |Source|Conservez la valeur par défaut **Tous**.|
   |Source port ranges|Conservez les paramètres par défaut pour les plages de ports.|
   |Destination|Sélectionnez **Groupe de sécurité d’application**.|
   |Groupe de sécurité d’application de destination|Sélectionnez **asg-mgmt**.|
   |Service|Sélectionnez **RDP**.|
   |Plages de ports de destination|Utilisez le paramètre par défaut « 3389 ».|
   |Protocol|Utilisez le paramètre par défaut « TCP ».|
   |Action|Utilisez le paramètre par défaut « Autoriser ».|
   |Priorité|Utilisez le paramètre par défaut « 110 ».|
   |Nom|Saisissez **allowrdpall**.|
   
6. Sélectionnez **Ajouter**.

### Créez deux machines virtuelles sur le réseau virtuel que vous avez créé précédemment.

1. Dans le portail, recherchez et sélectionnez **Machines virtuelles**.

2. Dans **Machines virtuelles**, sélectionnez **+ Créer**, puis **Machine virtuelle Azure**.
   
3. Dans **Créer une machine virtuelle**, entrez ou sélectionnez les informations suivantes dans l’onglet **Informations de base** :

   |Paramètre|Valeur|
   |---|---|
   |**Détails du projet**|
   |Abonnement|Sélectionnez votre abonnement.|
   |Resource group|Sélectionnez **az-rg-1**.|
   |**Détails de l’instance**|
   |Nom de la machine virtuelle|Entrez **vm-1**.|
   |Région|Sélectionnez **(États-Unis) USA Est**.|
   |Options de disponibilité|Dans le menu déroulant Zone de disponibilité, sélectionnez **Aucune redondance d’infrastructure requise**.|
   |Type de sécurité|Dans le menu déroulant Type de sécurité, sélectionnez **Standard**.|
   |Image|Dans le menu déroulant Image, sélectionnez **Windows Server 2022 Datacenter: Azure Edition - x64 Gen2**.|
   |Architecture de machine virtuelle|Utilisez le paramètre par défaut « x64 ».|
   |Exécuter avec la remise Azure Spot|Laissez le paramètre par défaut non coché.|
   |Taille|Utilisez le paramètre par défaut « Standard_D2s_v3-2 vcpus, 8 Go de mémoire ».|
   |**Compte administrateur**|
   |Type d'authentification|Sélectionnez **Mot de passe**.|
   |Nom d’utilisateur|Saisissez **Tenantadmin1**.|
   |Mot de passe|Saisissez **Superuser#150**.|
   |Confirmer le mot de passe|Saisissez à nouveau **Superuser#150.**|
   |**Règles des ports d’entrée**|
   |Aucun port d’entrée public|Sélectionnez **Aucun**.|
 
4. Sélectionnez **Suivant : Disques**, puis **Suivant : Réseaux**.

5. Sur la page **Mise en réseau**, vérifiez ou entrez les informations suivantes :

   |Paramètre|Valeur|
   |---|---|
   |**Interface réseau**|
   |Réseau virtuel|Sélectionnez **vnet-1**.|
   |Sous-réseau|Sélectionnez **par défaut (10.0.0.0/24)** .|
   |Adresse IP publique|Utilisez le paramètre par défaut « nouvelle adresse IP publique ».|
   |Groupe de sécurité réseau de la carte réseau|Sélectionnez **Aucun**.|
   
6. Sélectionnez l’onglet **Vérifier + créer**, ou sélectionnez le bouton **Vérifier + créer** situé au bas de la page.

7. Sélectionnez **Créer**. Le déploiement de la machine virtuelle peut prendre quelques minutes.
  
   - Créez la deuxième machine virtuelle.

   - Répétez les étapes précédentes pour créer une deuxième machine virtuelle nommée **vm-2**.

   - Attendez que le déploiement des machines virtuelles soit terminé avant de passer à la section suivante.

### Associer des interfaces réseau à un groupe de sécurité d'application

>**Remarque** : lorsque vous avez créé les machines virtuelles, Azure a créé une interface réseau pour chacune d’elles et l’a attachée à celle-ci. Ajoutez l’interface réseau de chaque machine virtuelle à l’un des groupes de sécurité d’application que vous avez créés précédemment :

1. Dans la zone de recherche située en haut du portail, entrez **Machine virtuelle**. Sélectionnez **Machines virtuelles** dans les résultats de la recherche.

2. Sélectionnez **vm-1**.
 
3. Sélectionnez **Mise en réseau** dans la section de **vm-1**.

4. Sélectionnez **Groupes de sécurité d’applications** dans la section **Mise en réseau** de **vm-1. Sélectionnez **+ Ajouter des groupes de sécurité d’applications**.

5. Dans le modèle **Ajouter des groupes de sécurité d’applications**, sélectionnez **asg-mgmt** dans le menu déroulant **Groupes de sécurité d’applications**, puis cliquez sur le bouton **Ajouter** en bas de la page du modèle.

![image](https://github.com/MicrosoftLearning/Secure-Azure-with-Microsoft-Defender-Cloud-Compliance-Controls/assets/91347931/dd17aeba-8e16-431b-b921-527367fea484)

6. Répétez les étapes précédentes pour **vm-2**, en sélectionnant **asg-web** dans le modèle **Groupes de sécurité d’application**.

> **Résultats** : vous avez créé une infrastructure de réseau virtuel et filtré le trafic réseau avec un groupe de sécurité réseau via le portail Azure.

> **Remarque** : ne supprimez pas les ressources de ce labo, car vous en aurez besoin dans les exercices suivants : Exercice 05 - Activer l’accès juste-à-temps sur des machines virtuelles, Exercice 06a - Configurer un pare-feu et des réseaux virtuels dans Key Vault.
