---
lab:
  title: "Exercice 03\_- Créer un espace de travail Log Analytics"
  module: Module 04 - Create a Log Analytics workspace
---


>**Remarque** : pour suivre ce labo, vous devez disposer d’un [abonnement Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) où vous disposez de droits d’accès administratif. 


Lorsque vous collectez des journaux et des données, les informations sont stockées dans un espace de travail. Un espace de travail a un ID d’espace de travail et un ID de ressource uniques. Le nom de l'espace de travail doit être unique au sein de votre groupe de ressources. Après avoir créé un espace de travail, configurez les sources de données et les solutions pour y stocker leurs données. 

---

## Tâche associée à la compétence

- Créez un espace de travail Log Analytics.
- Associez un groupe de ressources existant à l’espace de travail.
- Spécifiez une région précise pour déployer l’espace de travail.

## Instructions de l’exercice 

### Utilisez le menu Espaces de travail Log Analytics pour créer un espace de travail.

1. Démarrez une session de navigateur et connectez-vous au [menu du Portail Azure.](https://portal.azure.com/)
   
2. Dans la zone de recherche située en haut du portail, entrez **Espaces de travail Log Analytics**. Sélectionnez **Espaces de travail Log Analytics** dans les résultats de la recherche.

3. Sur la page **Espaces de travail Log Analytics**, sélectionnez **+ Créer**.

4. Sur la page **Informations de base** de **Créer un espace de travail Log Analytics**, saisissez ou sélectionnez les informations suivantes :
   
   |Paramètre|Valeur|
   |---|---|
   |**Détails du projet**|
   |Abonnement|Sélectionnez votre abonnement.|
   |Resource group|Entrez **azure-rg-1.**|
   |**Détails de l’instance**|
   |Nom|Entrez **azwrkspc1a.**|
   |Région|Sélectionnez **USA Est**.|

5. Sélectionnez l’onglet **Vérifier et créer** au bas de la page.
  
6. Sélectionnez **Créer**.

> **Résultats :** vous avez créé un espace de travail Log Analytics pour collecter des données à partir de ressources Azure.
