---
lab:
  title: "Exercice\_03a\_: activer Defender pour le cloud sur votre abonnement Azure"
  module: Module 03 - Set up Microsoft Defender for Cloud
---


>**Remarque** : pour suivre ce labo, vous devez disposer d’un [abonnement Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) où vous disposez de droits d’accès administratif. 


L’objectif principal de cet exercice est de fournir une expérience pratique en configuration et en activation de Microsoft Defender pour le cloud dans le cadre d’un abonnement Azure. Cela vous permettra de surveiller et de protéger vos ressources cloud contre les menaces de sécurité. 

---

## Tâches d'apprentissage

- Mettez à jour votre abonnement pour bénéficier de Microsoft Defender pour le cloud.
  
- Déployez Microsoft Monitoring Agent sur les machines nécessaires pour obtenir une couverture complète.

## Instructions de l’exercice

### Mettre à niveau Microsoft Defender pour le cloud

1. Connectez-vous dans le [menu du portail Azure.](https://portal.azure.com/)

2. Dans le portail Azure, dans la zone de texte Rechercher des ressources, des services et des documents en haut de la page Portail Azure, tapez Microsoft Defender pour le cloud et appuyez sur la touche Entrée.

3. Dans le panneau **Microsoft Defender pour le cloud**, **Prise en main**, accédez à l’**onglet Mettre à niveau**. Faites défiler la page jusqu’à ce que la section **Sélectionner des abonnements et des espaces de travail à protéger avec des fonctionnalités de sécurité améliorées** soit visible.

4. Activez le plan Microsoft Defender en sélectionnant votre **abonnement** et l**espace de travail Log Analytics** que vous avez créé dans le module 02.

5. Cliquez sur le bouton **Mettre à niveau** au bas de la page.
   
    ![image](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/256bd584-b04f-4d5b-81a7-c83dd1af3b4f)
   
6. Dans le panneau **Microsoft Defender pour le cloud**, **Prise en main**, accédez à l’onglet **Installer des agents**, puis faites défiler la page vers le bas.

    ![image](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/8120ec8f-23dc-4636-bc45-b415c7894b8c)

7. Cochez la case associée à l’abonnement sur lequel les agents seront installés, puis cliquez sur **Installer les agents.**

### Différentes options s’offrent à vous pour mettre à niveau votre abonnement Azure afin de bénéficier de Microsoft Defender pour le cloud.

1. Accédez à **Microsoft Defender pour le cloud** et, dans le volet de navigation de gauche sous la section Administration, cliquez sur **Paramètres d’environnement**.
   
2. Dans le panneau **Microsoft Defender pour le cloud, paramètres d’environnement**, cliquez sur **Développer tout,**. Faites ensuite défiler la page vers le bas jusqu’à ce que votre abonnement s’affiche, puis cliquez sur l’abonnement concerné.

3. Dans le panneau **Paramètres, plans Defender**, sélectionnez **Activer tous les plans** et cliquez sur **Enregistrer.**

   ![image](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Defender-for-Cloud-regulatory-compliance-controls/assets/91347931/4b684851-98ae-4720-a3e3-afa99aab8c43)




   

   
> **Résultats** : vous avez mis à niveau votre abonnement Azure et activé Defender pour le cloud pour celui-ci.
