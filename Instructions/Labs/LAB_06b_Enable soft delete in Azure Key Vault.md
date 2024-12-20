---
lab:
  title: Exercice 06b - Activer la suppression réversible dans Azure Key Vault
  module: Module 07 - Configure Azure Key Vault networking settings
---


>**Remarque** : pour suivre ce labo, vous devez disposer d’un [abonnement Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) où vous disposez de droits d’accès administratif. 


La suppression d’un coffre de clés sur lequel la suppression réversible n’est pas activée supprime définitivement tous les secrets, toutes les clés et tous les certificats qui y stockés. La suppression accidentelle d’un coffre de clés peut entraîner la perte définitive des données. La suppression réversible vous permet de récupérer un coffre de clés supprimé accidentellement, pendant une période de conservation configurable.

---

## Tâches d'apprentissage

- Vérifiez si la suppression réversible est activée sur un coffre de clés et activez la suppression réversible.

## Instructions de l’exercice 

### Vérifier si la suppression réversible est activée sur un coffre de clés et activer la suppression réversible

1. Démarrez une session de navigateur et connectez-vous au [menu du Portail Azure](https://portal.azure.com/).
  
2. Dans la zone de recherche située en haut du portail, entrez **Coffres de clés**. Sélectionnez **Coffres de clés** dans les résultats de la recherche.
   
3. Accédez au coffre de clés que vous avez créé précédemment.

4. Dans le panneau **Paramètres**, sélectionnez **Propriétés**.

5. Vérifiez si la case d’option en regard de la suppression réversible est définie sur **Activer la protection contre le vidage (appliquer une période de rétention obligatoire pour les coffres et les objets de coffre supprimés).**

6. Si la suppression réversible n’est pas activée sur le coffre de clés, cliquez sur la case d’option **Activer la protection contre le vidage (appliquer une période de rétention obligatoire pour les coffres et les objets de coffre supprimés)** pour activer la suppression réversible, puis cliquez sur **Enregistrer.**

   ![image](https://github.com/user-attachments/assets/8cc1d810-5a15-43fb-9dd8-1484af65897e)

> **Résultats** : vous avez activé la suppression réversible, garantissant ainsi que les ressources supprimées sont conservées pendant 90 jours (par défaut) et que vous pouvez les récupérer et donc annuler leur suppression via le Portail Azure.
