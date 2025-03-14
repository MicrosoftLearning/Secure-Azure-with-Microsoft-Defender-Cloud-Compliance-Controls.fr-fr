---
lab:
  title: Exercice 06a – Configurer les paramètres de mise en réseau Azure Key Vault
  module: Module 07 - Configure Azure Key Vault networking settings
---


>**Remarque** : pour suivre ce labo, vous devez disposer d’un [abonnement Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) où vous disposez de droits d’accès administratif. 


Vous pouvez utiliser le portail Microsoft Azure pour la configuration des paramètres de mise en réseau d’Azure Key Vault pour un fonctionnement avec d’autres applications et services Azure. 

---

## Tâches d'apprentissage

- Créez un coffre de clés à l’aide du portail Azure.

- Ajoutez un réseau virtuel existant à un pare-feu et à des règles de réseau virtuel.

- Configurez un réseau virtuel et un sous-réseau pour autoriser l’accès à un coffre de clés.

## Instructions de l’exercice 

### Utilisez le Portail Azure pour créer une instance Azure Key Vault.

1. Démarrez une session de navigateur et connectez-vous au [menu du Portail Azure.](https://portal.azure.com/)
  
2. Dans la zone de recherche située en haut du portail, entrez **Coffres de clés**. Sélectionnez **Coffres de clés** dans les résultats de la recherche.

3. Dans la liste des résultats, choisissez **Coffres de clés**.

4. Dans la section Key Vault, choisissez **Créer.**

5. Sous l’onglet **De base** de **Créer un coffre de clés**, entrez ou sélectionnez les informations suivantes :
   
   |Paramètre|Valeur|
   |---|---|
   |**Détails du projet**|
   |Abonnement|Sélectionnez votre abonnement.|
   |Resource group|Entrez **azure-rg-1.**|
   |**Détails de l’instance**|
   |Nom du coffre de clés|Le nom du coffre doit contenir uniquement des caractères alphanumériques et des tirets, et ne doit pas commencer par un chiffre. *Exemple : az-securevault150*|
   |Région|Sélectionnez **USA Est**.|
   |Niveau tarifaire|Utilisez le paramètre par défaut « Standard ».|
   |Jours de conservation des coffres supprimés|Utilisez le paramètre par défaut « 90 ».|

6. Sélectionnez l’**onglet Vérifier + créer** ou sélectionnez le bouton bleu Vérifier + créer en bas de la page.
  
7. Sélectionnez **Créer**.

### Configurez les paramètres de pare-feu et de réseau virtuel Key Vault.

1. Dans la zone de recherche du Portail Azure, entrez **Coffres de clés.**

2. Accédez au coffre de clés que vous avez créé précédemment.

3. Sélectionnez **Paramètres**, puis **Mise en réseau**, puis l’onglet **Pare-feux et réseaux virtuels**.
   
4. Sous Autoriser l’accès à partir de, sélectionnez **Autoriser l’accès public à partir de réseaux virtuels et d’adresses IP spécifiques.**

5. Dans la section Réseaux virtuels, sélectionnez + **Ajouter un réseau virtuel,** puis sélectionnez + **Ajouter des réseaux virtuels existants.**

6. Dans le modèle **Ajouter des réseaux**, sélectionnez le réseau virtuel que vous avez créé précédemment dans les listes déroulantes **Réseaux virtuels** et **Sous-réseaux**.

7. Au bas du modèle **Ajouter des réseaux**, sélectionnez **Activer**, puis cliquez sur **Ajouter**. 

8. En bas de la page **Pare-feux et réseaux virtuels**, sélectionnez **Appliquer**.

  > **Résultats** : vous avez créé un coffre de clés et configuré des paramètres de pare-feu et de réseau virtuel Key Vault sur le portail Azure.
