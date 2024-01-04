---
lab:
  title: "Exercice\_03b\_: activer l’accès juste-à-temps sur les machines virtuelles"
  module: Module 03 - Configure just-in-time (JIT) VM access in Defender for Cloud
---


>**Remarque** : pour suivre ce labo, vous devez disposer d’un [abonnement Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) où vous disposez de droits d’accès administratif. 


Vous pouvez utiliser l’accès juste-à-temps (JAT) de Microsoft Defender pour le cloud pour protéger vos machines virtuelles Azure contre l’accès réseau non autorisé. Souvent, les pare-feu contiennent des règles d’autorisation qui laissent vos machines virtuelles vulnérables aux attaques. JAT vous permet d’autoriser l’accès à vos machines virtuelles uniquement lorsque l’accès est nécessaire, sur les ports nécessaires et pendant la période nécessaire. 

---

## Tâches d'apprentissage

- Activez JAT sur vos machines virtuelles depuis le portail Azure.

- Demandez l’accès à une machine virtuelle sur laquelle l’accès JAT est activé depuis le portail Azure.

## Instructions de l’exercice 

### Activer l’accès JAT sur vos machines virtuelles à partir des machines virtuelles Azure

>**Remarque** : vous pouvez activer l’accès JAT sur une machine virtuelle depuis les pages des machines virtuelles Azure sur le portail Azure.

1. Sur le Portail Azure, repérez et sélectionnez **Machines virtuelles.**
   
2. Sélectionnez la machine virtuelle que vous souhaitez protéger à l’aide de l’accès JAT.

3. Dans le menu, sélectionnez **Configuration**.

4. Sous **Accès juste-à-temps**, sélectionnez **Activer l’accès juste-à-temps**.

5. Sous **Accès juste-à-temps à la machine virtuelle,** cliquez sur le lien intitulé **Ouvrir Microsoft Defender pour le cloud.**

6. Par défaut, l’accès juste-à-temps pour la machine virtuelle utilise les paramètres suivants :

   - Machines Windows
   
     - Port RDP : 3389
     - Accès maximal autorisé : trois heures
     - Adresses IP sources autorisées : toutes les adresses IP

   - Machines Linux
     - Port SSH : 22
     - Accès maximal autorisé : trois heures
     - Adresses IP sources autorisées : toutes les adresses IP
   
7. Par défaut, l’accès juste-à-temps pour la machine virtuelle utilise les paramètres suivants :

   - Dans l’onglet **Configuré**, cliquez avec le bouton droit sur la machine virtuelle à laquelle vous souhaitez ajouter un port, puis sélectionnez Modifier.
  
 ![image](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Defender-for-Cloud-regulatory-compliance-controls/assets/91347931/66cf98b6-2ce0-43c7-a7be-b5d69bcfac1d)




   - Sous **JIT VM access configuration** (Configuration de l’accès juste-à-temps à la machine virtuelle), vous pouvez soit modifier les paramètres existants d’un port déjà protégé, soit ajouter un nouveau port personnalisé.
   - Lorsque vous avez fini de modifier les ports, sélectionnez **Enregistrer**.   

### Demandez l’accès à une machine virtuelle prenant en charge l’accès JAT depuis la page de connexion de la machine virtuelle Azure.

>**Remarque** :  lorsque l’accès JAT est activé pour une machine virtuelle, vous devez demander cet accès pour vous y connecter. Vous pouvez demander l’accès selon l’une des méthodes prises en charge, quelle que soit la façon dont vous avez activé l’accès JAT.
   
1. Dans le portail Azure, ouvrez la page des machines virtuelles.

2. Sélectionnez la machine virtuelle à laquelle vous souhaitez vous connecter, puis ouvrez la page **Se connecter**.

   - Azure vérifie si l’accès JAT est activé sur cette machine virtuelle.

        - S’il n’est pas activé pour la machine virtuelle, vous êtes invité à le faire.
    
        - S’il est activé, sélectionnez **Demander l’accès** pour transmettre une demande d’accès avec l’adresse IP, la plage de temps et les ports de la requête qui ont été configurés pour cette machine virtuelle.

![image](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Defender-for-Cloud-regulatory-compliance-controls/assets/91347931/7e454150-bc04-47bc-afa1-e0a1e8af17f9)






> **Résultats** : vous avez étudié différentes méthodes pour activer l’accès JAT sur vos machines virtuelles et savoir comment demander l’accès aux machines virtuelles sur lesquelles il est activé dans Microsoft Defender pour le cloud.
