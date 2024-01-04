---
lab:
  title: "Exercice\_05a\_-\_Configurer le pare-feu et les réseaux virtuels Key Vault"
  module: Module 05 - Configure Azure Key Vault networking settings
---


>**Remarque** : pour suivre ce labo, vous devez disposer d’un [abonnement Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) où vous disposez de droits d’accès administratif. 


Vous pouvez utiliser le portail Azure pour configurer les paramètres de mise en réseau Azure Key Vault, en vue de leur emploi avec d’autres applications et services Azure. 

---

## Tâches d'apprentissage

- Créez un coffre de clés à l’aide du portail Azure.

- Ajoutez un réseau virtuel existant à un pare-feu et à des règles de réseau virtuel.

- Configurez un réseau virtuel et un sous-réseau pour autoriser l’accès à un coffre de clés.

## Instructions de l’exercice 

### Utilisez le Portail Azure pour créer une instance Azure Key Vault.

1. Démarrez une session de navigateur et connectez-vous au [menu du Portail Azure.](https://portal.azure.com/)
   
2. Dans la zone Rechercher du Portail Azure, entrez **Key Vault.**

3. Dans la liste des résultats, choisissez **Key Vault**.

4. Dans la section Key Vault, choisissez **Créer.**

5. Sous l’onglet **De base** de **Créer un coffre de clés**, entrez ou sélectionnez les informations suivantes :
   
   |Paramètre|Valeur|
   |---|---|
   |**Détails du projet**|
   |Abonnement|Sélectionnez votre abonnement.|
   |Groupe de ressources|Entrez **azure-rg-1.** Sélectionnez **OK**.|
   |**Détails de l’instance**|
   |Nom du coffre de clés|Entrez **AZAPLKeyVault.**|
   |Région|Sélectionnez **USA Est**.|
   |Niveau tarifaire|Valeur système par défaut **Standard**|
   |Jours de conservation des coffres supprimés|Valeur système par défaut **90**|

7. Sélectionnez l’**onglet Vérifier + créer** ou sélectionnez le bouton bleu Vérifier + créer en bas de la page.
  
8. Sélectionnez **Créer**.

### Configurez les paramètres de pare-feu et de réseau virtuel Key Vault.

1. Dans la zone Rechercher du Portail Azure, entrez **Key Vault.**

2. Accédez au coffre de clés que vous avez créé précédemment.

3. Sélectionnez **Mise en réseau**, puis l’onglet **Pare-feu et réseaux virtuels**.

4. Sous Autoriser l’accès à partir de, sélectionnez **Autoriser l’accès public à partir de réseaux virtuels et d’adresses IP spécifiques.**

5. Dans la section Réseaux virtuels, sélectionnez + **Ajouter un réseau virtuel,** puis sélectionnez + **Ajouter des réseaux virtuels existants.**

6. Dans le modèle Ajouter des réseaux, sélectionnez votre réseau virtuel créé précédemment dans les listes déroulantes **Réseaux virtuels** et **Sous-réseaux**.

7. Au bas du modèle Ajouter des réseaux, cliquez sur **Ajouter.**

  > **Résultats** : vous avez créé un coffre de clés et configuré des paramètres de pare-feu et de réseau virtuel Key Vault sur le portail Azure.
