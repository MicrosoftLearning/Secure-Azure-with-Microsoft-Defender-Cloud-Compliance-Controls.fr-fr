---
lab:
  title: "Excercice\_01\_: configuration des fonctionnalités de sécurité renforcée pour les serveurs de Microsoft\_Defender pour le cloud"
  module: Module 02 - Enable Defender for Cloud on Your Azure Subscription
---


>**Remarque** : pour suivre ce labo, vous devez disposer d’un [abonnement Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) où vous disposez de droits d’accès administratif. 


L’objectif principal de cet exercice est de fournir une expérience pratique de la configuration et de l’activation du Plan 2 de Microsoft Defender pour serveurs dans un abonnement Azure. Cela vous permettra de surveiller et de protéger vos ressources cloud contre les menaces de sécurité. 

---

## Tâches d'apprentissage

- Configuration des fonctionnalités de sécurité renforcée pour les serveurs de Microsoft Defender pour le cloud
  
- Passer en revue les fonctionnalités de sécurité renforcée pour le Plan 2 de Microsoft Defender pour serveurs

## Instructions de l’exercice

### Configuration des fonctionnalités de sécurité renforcée pour les serveurs de Microsoft Defender pour le cloud

1. Connectez-vous dans le [menu du portail Azure.](https://portal.azure.com/)

2. Dans le portail Azure, dans la zone de texte Rechercher des ressources, des services et des documents située en haut de la page du portail Azure, saisissez **Microsoft Defender pour le cloud** et appuyez sur la touche **Entrée**.

3. Dans **Microsoft Defender pour le cloud**, dans le **panneau de gestion**, accédez aux **paramètres d’environnement**. Développez les dossiers des paramètres d’environnement jusqu’à ce que la section **abonnement** s’affiche, puis cliquez sur l’**abonnement** pour afficher les détails.

   ![image](https://github.com/user-attachments/assets/32d2168e-458f-4872-9bf8-e8f050f24751)
   
3. Dans le panneau **Paramètres**, sous **plans Defender**, développez **Protection de la charge de travail du cloud**.

4. Dans la liste **Plan de protection de charge de la charge de travail du cloud**, sélectionnez **Serveurs**. À droite de la page, remplacez le **Statut** **Désactivé** par **Activé**, puis cliquez sur **Enregistrer.**

5. Pour passer en revue les détails du **Plan 2 de Microsoft Defender pour serveurs**, sélectionnez **Modifier le plan >**.

   Remarque : l’activation du plan Serveurs de la Protection de la charge de travail du cloud active également le Plan 2 de Microsoft Defender pour serveurs.

   ![image](https://github.com/user-attachments/assets/869a38e4-464e-4be0-b02e-ce1b96f02978)
   
> **Résultats** : vous avez activé le Plan 2 de Microsoft Defender pour serveurs pour votre abonnement.