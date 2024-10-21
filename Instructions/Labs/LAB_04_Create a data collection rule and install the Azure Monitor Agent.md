---
lab:
  title: "Exercice\_04\_- Créer une règle de collecte de données et installer l’agent Azure Monitor"
  module: Module 05 - Create a data collection rule and install the Azure Monitor Agent
---


>**Remarque** : pour suivre ce labo, vous devez disposer d’un [abonnement Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) où vous disposez de droits d’accès administratif. 


Les règles de collecte de données spécifient les données à collecter, tandis que l’agent Azure Monitor applique ces règles pour collecter des journaux et des mesures à partir de machines virtuelles dans Azure, d’autres clouds ou localement. Ensemble, ils permettent une surveillance cohérente et centralisée dans plusieurs environnements différents.

---

## Tâches d'apprentissage

- Créer et définir une règle de collecte de données.

- Sélectionner les ressources cibles pour la collecte de données.

- Installez l’agent Azure Monitor.
  
- Configurer les sources et les destinations de données.

- Sélectionner les types de sources de données et les données à collecter.

- Choisir une destination pour la remise des données.

## Instructions de l’exercice 

### Créer et définir une règle de collecte de données.

>**Remarque** : créez votre règle de collecte de données dans la même région que votre espace de travail Log Analytics ou votre espace de travail Azure Monitor de destination. Vous pouvez associer la règle de collecte de données à des machines ou à des conteneurs depuis tout abonnement ou groupe de ressources dans le locataire.

1. Dans la zone de recherche située en haut du portail, entrez les **règles de collecte de données**. Sélectionnez les **règles de collecte de données** dans les résultats de la recherche.
  
2. Sélectionnez **+ Créer**.

![image](https://github.com/user-attachments/assets/99b9ac51-f2f4-466f-80bb-79d74874b573)

3. Sur la page **Informations de base** du panneau **Créer une règle de collecte de données**, spécifiez les paramètres suivants (conservez les valeurs par défaut pour les autres paramètres) :

    |Paramètre|Valeur|
    |---|---|
    |**Détails de la règle**|
    |Nom de la règle|**dcr-1**|
    |Abonnement|nom de l’abonnement que vous utilisez dans ce labo|
    |Resource group|**az-rg-1**|
    |Région|**USA Est**|
    |Type de plate-forme|**Windows**|
    |Point de terminaison de collecte de données|*Conservez la valeur par défaut « Aucun »*|

![image](https://github.com/user-attachments/assets/35c527cf-499d-44b9-966f-0114b8643ef2)

4. Cliquez sur le bouton étiqueté **Suivant : Ressources >** pour continuer.
   
5. Sur la page **Ressources**, sélectionnez **+ Ajouter des ressources**.
  
>**Remarque** : l’agent Azure Monitor sera automatiquement installé sur les machines virtuelles (ressources) sélectionnées pour collecter les données.

![image](https://github.com/user-attachments/assets/47174eb4-4343-49a2-b49d-e9dee76787e4)

6. Dans le modèle **Sélectionner une étendue**, cochez la case **Abonnement** dans l’**Étendue**.

![image](https://github.com/user-attachments/assets/2215e8cd-5047-4fc6-91ba-b2c645571bbd)

7. En bas du modèle **Sélectionner une étendue**, cliquez sur **Appliquer**.
  
8. En bas de la page **Ressources**, sélectionnez **Suivant : collecter et remettre >**. 

![image](https://github.com/user-attachments/assets/717226c3-5ce0-454f-93a4-11b0e67d5a23)

9. Sur la page **Collecter et remettre**, cliquez sur **+ Ajouter une source de données**.

![image](https://github.com/user-attachments/assets/0809cf5b-a460-40d1-8508-e42ba7ce78c1)

10. Dans le modèle **Ajouter une source de données**, sous **Type de source de données**, sélectionnez les paramètres suivants.
    
    |Paramètre|Valeur|
    |---|---|
    |**Ajouter une source de données**|
    |Sélectionnez le type de source de données et les données à collecter pour vos ressources.|
    |Type de source de données*|**Journaux des événements Windows**|
    |Configurer les journaux et les niveaux d’événements à collecter|
    |Application|**Critique**, **Erreur**, **Avertissement**|
    |Sécurité|**Audit réussi**, **Échec de l’audit**|
    |System|**Critique**, **Erreur**, **Avertissement**|

![image](https://github.com/user-attachments/assets/5bc891ea-8cef-4baa-95c4-a432364179b1)

11. En bas du modèle **Ajouter une source de données**, sélectionnez **Suivant : destination > **.
   
12. Dans le modèle **Ajouter une source de données**, dans l’onglet **Destination**, sélectionnez les paramètres suivants.
    
    |Paramètre|Valeur|
    |---|---|
    |**Ajouter une source de données**|
    |Destination|**+ Ajouter une destination**|
    |Type de destination|**Journaux Azure Monitor**|
    |Abonnement|Sélectionnez votre abonnement.|
    |Détails de la destination|**azwrkspc1a (az-rg-1**)

![image](https://github.com/user-attachments/assets/e00c17c8-5a70-4caa-8504-92f482cc5e57)

13. En bas du modèle **Ajouter une source de données**, sélectionnez **Ajouter une source de données**.

![image](https://github.com/user-attachments/assets/4277089c-971c-4334-a49d-6ac6bfe93ff4)

14. En bas de la page **Collecter et remettre**, sélectionnez **Vérifier et créer**.

![image](https://github.com/user-attachments/assets/0235fed9-6309-444c-9269-b9dbd1118b63)

15. En bas de la page **Vérifier et créer**, sélectionnez **Créer**.

> **Résultats** : vous avez créé une règle de collecte de données et installé l’agent Azure Monitor.
