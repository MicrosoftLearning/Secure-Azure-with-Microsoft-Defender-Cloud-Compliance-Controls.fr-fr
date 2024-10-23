---
lab:
  title: "Exercice\_04\_: créer une règle de collecte de données et installer l’agent Azure Monitor"
  module: Module 05 - Collect guest operating system monitoring data from Azure and hybrid virtual machines using Azure Monitor Agent
---


>**Remarque** : pour suivre ce labo, vous devez disposer d’un [abonnement Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) où vous disposez de droits d’accès administratif. 


Les règles de collecte de données spécifient les données à collecter, tandis que l’agent Azure Monitor applique ces règles pour collecter des journaux et des métriques à partir de machines virtuelles dans Azure, d’autres clouds ou localement. Ensemble, ils permettent une surveillance cohérente et centralisée dans différents environnements.

---

## Tâches d'apprentissage

- Créer et définir une règle de collecte de données

- Sélectionner les ressources cibles pour la collecte de données

- Installez l’agent Azure Monitor.
  
- Configurer les sources et destinations de données

- Sélectionner les types de sources de données et les données à collecter

- Choisr une destination de remise des données

## Instructions de l’exercice 

### Créez et définissez une règle de collecte de données et installez l’agent Azure Monitor.

>**Remarque** : créez la règle de collecte de données dans la même région que votre espace de travail Log Analytics ou Azure Monitor. Vous pouvez l’associer à des machines ou à des conteneurs à partir de tout abonnement ou groupe de ressources dans le locataire. L’agent Azure Monitor sera automatiquement installé sur les ressources virtuelles Azure.

1. Dans la zone de recherche située en haut du portail, saisissez **règles de collecte de données**. Sélectionnez **Règles de collecte de données** dans les résultats de la recherche.
  
2. Sur la page **Règles de collecte de données**, sélectionnez **+ Créer**.
  
   ![image](https://github.com/user-attachments/assets/99b9ac51-f2f4-466f-80bb-79d74874b573)

3. Sur la page **Informations de base** du panneau **Créer une règle de collecte de données**, spécifiez les paramètres suivants (conservez les valeurs par défaut pour les autres paramètres) :

    |Paramètre|Valeur|
    |---|---|
    |**Détails de la règle**|
    |Nom de la règle|**dcr-1**|
    |Abonnement|Sélectionnez votre abonnement.|
    |Resource group|**az-rg-1**|
    |Région|**USA Est**|
    |Type de plate-forme|**Windows**|
    |Point de terminaison de collecte de données|Utilisez le paramètre par défaut « Aucun ».|

    ![image](https://github.com/user-attachments/assets/35c527cf-499d-44b9-966f-0114b8643ef2)

4. Cliquez sur le bouton en bas de la page **Informations de base** intitulé **Suivant : Ressources >** pour continuer.
   
5. Sur la page **Ressources**, sélectionnez **+ Ajouter des ressources**.

    ![image](https://github.com/user-attachments/assets/6aabf2c9-bea2-47c1-9b0b-bf131cdec4e3)

6. Dans le modèle **Sélectionner une étendue**, cochez la case **Abonnement** dans l’**Étendue**.

    ![image](https://github.com/user-attachments/assets/2215e8cd-5047-4fc6-91ba-b2c645571bbd)

7. En bas du modèle **Sélectionner une étendue**, cliquez sur **Appliquer**.
  
8. En bas de la page **Ressources**, sélectionnez **Suivant : Collecter et remettre >**.

    ![image](https://github.com/user-attachments/assets/717226c3-5ce0-454f-93a4-11b0e67d5a23)

9. Sur la page **Collecter et remettre**, cliquez sur **+ Ajouter une source de données**.

    ![image](https://github.com/user-attachments/assets/0809cf5b-a460-40d1-8508-e42ba7ce78c1)

10. Dans le modèle **Ajouter une source de données**, dans **Type de source de données**, sélectionnez les paramètres suivants.
    
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

    ![image](https://github.com/user-attachments/assets/5bc891ea-8cef-4baa-95c4-a432364179b1)

12. En bas du modèle **Ajouter une source de données**, sélectionnez **Suivant : destination > **.
   
13. Dans le modèle **Ajouter une source de données**, dans l’onglet **Destination**, sélectionnez les paramètres suivants.
    
    |Paramètre|Valeur|
    |---|---|
    |**Ajouter une source de données**|
    |Destination|**+ Ajouter une destination**|
    |Type de destination|**Journaux Azure Monitor**|
    |Abonnement|Sélectionnez votre abonnement.|
    |Détails de la destination|**azwrkspc1a (az-rg-1**)|

    ![image](https://github.com/user-attachments/assets/e00c17c8-5a70-4caa-8504-92f482cc5e57)

14. En bas du modèle **Ajouter une source de données**, sélectionnez **Ajouter une source de données**.

    ![image](https://github.com/user-attachments/assets/4277089c-971c-4334-a49d-6ac6bfe93ff4)

15. En bas de la page **Collecter et remettre**, sélectionnez **Examiner et créer**.

    ![image](https://github.com/user-attachments/assets/0235fed9-6309-444c-9269-b9dbd1118b63)

16. En bas de la page **Examiner et créer**, sélectionnez **Créer**.

> **Résultats** : vous avez créé une règle de collecte de données et installé l’agent Azure Monitor.
