---
lab:
  title: "Exercice\_04\_: créer une règle de collecte de données et installer l’agent Azure Monitor"
  module: Module 05 - Create a data collection rule and install the Azure Monitor Agent
---


>**Remarque** : pour suivre ce labo, vous devez disposer d’un [abonnement Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) où vous disposez de droits d’accès administratif. 


Les règles de collecte de données spécifient les données à collecter, tandis que l’agent Azure Monitor applique ces règles pour collecter des journaux et des métriques à partir de machines virtuelles dans Azure, d’autres clouds ou localement. Ensemble, ils permettent une surveillance cohérente et centralisée dans différents environnements.

---

## Tâches d'apprentissage

- Créer et définir une règle de collecte de données

- Sélectionner les ressources cibles pour la collecte de données
  
- Configurer les sources et destinations de données

- Sélectionner les types de sources de données et les données à collecter

- Choisr une destination de remise des données

## Instructions de l’exercice 

### Créer et définir une règle de collecte de données

>**Remarque** : créez votre règle de collecte de données dans la même région que votre espace de travail Log Analytics ou votre espace de travail Azure Monitor de destination. Vous pouvez associer la règle de collecte de données à des machines ou à des conteneurs depuis tout abonnement ou groupe de ressources dans le locataire. 
   
1. Dans la zone de recherche située en haut du portail, entrez les règles de collecte de données. Sélectionnez les règles de collecte de données dans les résultats de la recherche.

2. Sélectionnez **+ Créer**.

![image](https://github.com/user-attachments/assets/e428c441-9d8d-4460-acd9-a97e2aa2b5af)

3. Sous l’onglet **Informations de base** du volet **Règle de collecte de données**, spécifiez les paramètres suivants (laissez les valeurs par défaut des autres paramètres) :

    |Paramètre|Valeur|
    |---|---|
    |**Détails de la règle**|
    |Nom de la règle|**dcr-1**|
    |Abonnement|nom de l’abonnement Iginte que vous utilisez dans ce labo|
    |Resource group|**az-rg-1**|
    |Région|**USA Est**|
    |Type de plate-forme|**Windows**|
    |Point de terminaison de collecte de données|*Conservez la valeur par défaut Aucun*|

![image](https://github.com/user-attachments/assets/eee884f6-b20f-4d51-9310-6e755746ed9a)   

4. Cliquez sur le bouton étiqueté **Suivant : Ressources >** pour continuer.

5. Sous l’onglet Ressources, sélectionnez **+ Ajouter des ressources**.
  
>**Remarque** : l’agent Azure Monitor sera automatiquement installé sur les machines virtuelles (ressources) sélectionnées pour collecter les données.
   
![image](https://github.com/user-attachments/assets/619106b4-7f5e-44dd-98c7-129689ab89c0)

6. Dans le modèle Sélectionner une étendue, cochez la case **Abonnement Ignite** dans la sélection de l’étendue, puis cliquez sur **Appliquer.**

![image](https://github.com/user-attachments/assets/c95b76cd-1515-47a5-b07b-02dcb28c0bf3)


8. Sélectionnez **Revoir + créer**.








> **Résultats** : vous avez créé une règle de collecte de données et installé l’agent Azure Monitor.
