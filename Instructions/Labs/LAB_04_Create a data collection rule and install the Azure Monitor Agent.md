---
lab:
  title: "Exercice\_04\_- Créer une règle de collecte de données et installer l’agent Azure Monitor"
  module: Module 05 - Collect guest operating system monitoring data from Azure and hybrid virtual machines using Azure Monitor Agent
---


>**Remarque** : pour suivre ce labo, vous devez disposer d’un [abonnement Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) où vous disposez de droits d’accès administratif. 


Les règles de collecte de données spécifient les données à collecter, tandis que l’agent Azure Monitor applique ces règles pour collecter des journaux et des mesures à partir de machines virtuelles dans Azure, d’autres clouds ou localement. Ensemble, elles permettent une surveillance cohérente et centralisée dans différents environnements.

---

## Tâches d'apprentissage

- Créer et définir une règle de collecte de données.

- Sélectionner les ressources cibles pour la collecte de données.

- Installez l’agent Azure Monitor.
  
- Configurer les sources et les destinations de données.

- Sélectionner les types de sources de données et les données à collecter.

- Choisir une destination de remise des données

## Instructions de l’exercice 

### Créez et définissez une règle de collecte de données et installez l’agent Azure Monitor.

>**Remarque** : créez la règle de collecte de données dans la même région que votre espace de travail Log Analytics ou Azure Monitor. Vous pouvez l’associer à des machines ou à des conteneurs à partir de tout abonnement ou groupe de ressources dans le locataire. L’agent Azure Monitor sera automatiquement installé sur les ressources virtuelles Azure.

1. Démarrez une session de navigateur et connectez-vous au [menu du Portail Azure.](https://portal.azure.com/)
  
3. Dans la zone de recherche située en haut du portail, saisissez **règles de collecte de données**. Sélectionnez **Règles de collecte de données** dans les résultats de la recherche.
  
4. Sur la page **Règles de collecte de données**, sélectionnez **+ Créer**.
  
    ![image](https://github.com/user-attachments/assets/a472bc6f-fa96-4615-a67c-c99e8b9ce7a4)

5. Sur la page **Informations de base** du panneau **Créer une règle de collecte de données**, spécifiez les paramètres suivants (conservez les valeurs par défaut pour les autres paramètres) :

    |Paramètre|Valeur|
    |---|---|
    |**Détails de la règle**|
    |Nom de la règle|**dcr-1**|
    |Abonnement|Sélectionnez votre abonnement.|
    |Groupe de ressources|**az-rg-1**|
    |Région|**USA Est**|
    |Type de plate-forme|**Windows**|
    |Point de terminaison de collecte de données|Utilisez le paramètre par défaut « Aucun ».|

   ![image](https://github.com/user-attachments/assets/6c63c48f-f7a9-4fb2-8fc0-e22084cd5013)

6. Cliquez sur le bouton en bas de la page **Informations de base** intitulé **Suivant : Ressources >** pour continuer.
   
7. Sur la page **Ressources**, sélectionnez **+ Ajouter des ressources**.

   ![image](https://github.com/user-attachments/assets/7e45996b-478b-4be4-9df3-df6127da6cb4)

8. Dans le modèle **Sélectionner une étendue**, cochez la case **Abonnement** dans l’**Étendue**.

   ![image](https://github.com/user-attachments/assets/0d228e47-039e-4418-ae66-025957e368bc)

9. En bas du modèle **Sélectionner une étendue**, cliquez sur **Appliquer**.
  
10. En bas de la page **Ressources**, sélectionnez **Suivant : Collecter et remettre >**.

    ![image](https://github.com/user-attachments/assets/95556211-654f-4810-98a0-5cd8fac13bff)  

11. Sur la page **Collecter et remettre**, cliquez sur **+ Ajouter une source de données**.

    ![image](https://github.com/user-attachments/assets/8274b0c1-8617-4889-9aef-78e050f2bd00)

12. Dans le modèle **Ajouter une source de données**, dans **Type de source de données**, sélectionnez les paramètres suivants :
    
    |Paramètre|Valeur|
    |---|---|
    |**Ajouter une source de données**|
    |Sélectionnez le type de source de données et les données à collecter pour vos ressources.|
    |Type de source de données*|**Journaux des événements Windows**|
    |Choisissez « De base » pour activer la collecte des journaux d’événements.|
    |Configurez les niveaux et les journaux d’événements à collecter :|
    |Application|**Critique**, **Erreur**, **Avertissement**|
    |Sécurité|**Audit réussi**, **Échec de l’audit**|
    |System|**Critique**, **Erreur**, **Avertissement**|

    ![image](https://github.com/user-attachments/assets/33039994-0613-40f4-9c55-03f795b38b9b)

13. En bas du modèle **Ajouter une source de données**, sélectionnez **Suivant : destination > **.

14. Dans le modèle **Ajouter une source de données**, dans l’onglet **Destination**, sélectionnez les paramètres suivants.
    
    |Paramètre|Valeur|
    |---|---|
    |**Ajouter une source de données**|
    |Destination|**+ Ajouter une destination**|
    |Type de destination|**Journaux Azure Monitor**|
    |Abonnement|Sélectionnez votre abonnement.|
    |Détails de la destination|**azwrkspc1a (az-rg-1**)|

     ![image](https://github.com/user-attachments/assets/dc2d2906-4a57-4df9-a33c-fd6ae34a8457)

15. En bas du modèle **Ajouter une source de données**, sélectionnez **Ajouter une source de données**.

16. En bas de la page **Collecter et remettre**, sélectionnez **Examiner et créer**.

    ![image](https://github.com/user-attachments/assets/4277089c-971c-4334-a49d-6ac6bfe93ff4)

17. En bas de la page **Examiner et créer**, sélectionnez **Créer**.

    ![image](https://github.com/user-attachments/assets/b532f92e-af10-4b4d-bb52-10d15ad38d4a)

> **Résultats** : vous avez créé une règle de collecte de données et installé l’agent Azure Monitor.
