---
lab:
  title: "Exercice 04\_:\_Configurer et intégrer un agent Log Analytics et un espace de travail dans Microsoft Defender pour le cloud"
  module: Module 05 - Configure and integrate a Log Analytics agent and workspace in Defender for Cloud
---


>**Remarque** : pour suivre ce labo, vous devez disposer d’un [abonnement Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) où vous disposez de droits d’accès administratif. 


Defender pour le cloud collecte des données à partir de vos machines virtuelles Azure, groupes de machines virtuelles identiques, conteneurs IaaS et ordinateurs autres qu’Azure (y compris localement) pour contrôler les menaces et vulnérabilités de sécurité. Certains plans Defender nécessitent des composants de surveillance pour collecter des données à partir de vos charges de travail. Quand l’agent Log Analytics est activé, Defender pour le cloud déploie l’agent sur toutes les machines virtuelles Azure prises en charge et toutes celles nouvellement créées. 

---

## Tâches d'apprentissage

- Utilisez les valeurs par défaut de l’agent Log Analytics pour votre type d’agent.

- Sélectionnez votre espace de travail.
  
- Définissez le niveau des données d’événement de sécurité à stocker au niveau de l’espace de travail.

## Instructions de l’exercice 

### Configurez l’intégration à l’agent Log Analytics.

>**Remarque** : lorsque l’agent Log Analytics est activé, Defender pour le cloud le déploie sur toutes les machines virtuelles Azure prises en charge et toutes celles nouvellement créées. 

1. Démarrez une session de navigateur et connectez-vous au [menu du Portail Azure.](https://portal.azure.com/)
   
2. Dans le menu de Defender pour le cloud, ouvrez **Paramètres de l’environnement**.

4. Sélectionnez votre abonnement.

5. Dans la colonne Paramètres et surveillance de la couverture des plans Defender, sélectionnez **Paramètres et surveillance.**

7. Sur la ligne Log Analytics, dans la colonne Configuration, cliquez sur **Modifier la configuration.**

8. Dans le modèle de configuration d’approvisionnement automatique, effectuez les actions suivantes :

   - Sous Sélection de l’espace de travail, cliquez sur **Espace de travail personnalisé.**

   - Cliquez sur le **menu déroulant** et **sélectionnez** votre espace de travail créé précédemment.

   - Sous **Stockage des événements de sécurité**, cliquez sur le **menu déroulant** et sélectionnez **Tous les événements.**

   - Au bas du modèle d’approvisionnement automatique, cliquez sur **Appliquer.**
   
![image](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/c1c812e7-b5ca-4caa-b8e6-34a6e4b325fd)




> **Résultats** : vous avez configuré l’agent et l’espace de travail Log Analytics dans Microsoft Defender pour le cloud.
