---
lab:
  title: "Exercice\_05b\_-\_Configurer la gestion de la récupération Azure\_Key\_Vault avec la protection contre le vidage et la suppression réversible"
  module: Module 05 - Perform soft-delete and purge protection key vault recovery
---


>**Remarque** : pour suivre ce labo, vous devez disposer d’un [abonnement Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) où vous disposez de droits d’accès administratif. 


La protection contre le vidage vise à éviter la suppression de votre coffre de clés et de vos clés, secrets et certificats par une personne malveillante en interne. Considérez-la comme une corbeille dotée d’un verrou basé sur la durée. Vous pouvez récupérer des éléments à tout moment pendant la période de rétention configurable. Vous ne pouvez pas supprimer définitivement ou vider un coffre de clés tant que la période de rétention n’est pas écoulée. Une fois la période de rétention écoulée, le coffre de clés ou l’objet de coffre de clés est vidé automatiquement.

---

## Tâches d'apprentissage

- Vérifiez si la suppression réversible est activée sur un coffre de clés et activez la suppression réversible.

- Répertoriez, récupérez ou videz un coffre de clés supprimé de manière réversible.

- Répertoriez, récupérez ou videz les secrets, les clés et les certificats supprimés de manière réversible.

## Instructions de l’exercice 

### Vérifier si la suppression réversible est activée sur un coffre de clés et activer la suppression réversible

1. Démarrez une session de navigateur et connectez-vous au [menu du Portail Azure.](https://portal.azure.com/)
   
2. Sélectionnez votre coffre de clés.

3. Cliquez sur le panneau **Propriétés**.

4. Vérifiez si la case d’option en regard de l’option de suppression réversible est paramétrée sur **Activer la protection contre le vidage.**

5. Si la suppression réversible n’est pas activée sur le coffre de clés, cliquez sur la case d’option pour activer la suppression réversible, puis sur **Enregistrer.**

![image](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/06131a60-7f00-4764-a424-87ea41a78394)


### Répertoriez, récupérez ou videz un coffre de clés supprimé de manière réversible.

1. Démarrez une session de navigateur et connectez-vous au [menu du Portail Azure.](https://portal.azure.com/)
   
2. Cliquez sur la barre de recherche en haut de la page.

3. Recherchez le service **Key Vault**. Ne cliquez pas sur un coffre de clés individuel.

4. En haut de l’écran, cliquez sur l’option « Gérer les coffres supprimés ».

5. Un volet contextuel s’ouvre sur le côté droit de l’écran.

6. Sélectionnez votre abonnement.

7. Si votre coffre de clés a été supprimé de manière réversible, il apparaît dans le volet contextuel à droite.

8. S’il y a trop de coffres, vous pouvez soit cliquer sur « Charger plus » en bas du volet contextuel, soit utiliser l’interface CLI ou PowerShell pour extraire les résultats.

9. Une fois que vous avez trouvé le coffre que vous souhaitez **récupérer** ou **vider,** cochez la **case** correspondante.

10. Sélectionnez l’option Récupérer en bas du volet contextuel si vous souhaitez récupérer le coffre de clés.

11. Sélectionnez l’option Vider si vous souhaitez supprimer définitivement le coffre de clés.

![image](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/f41c0673-3832-4d3f-8b05-48e46e6c2282)


### Répertoriez, récupérez ou videz les secrets, les clés et les certificats supprimés de manière réversible.

1. Démarrez une session de navigateur et connectez-vous au [menu du Portail Azure.](https://portal.azure.com/)
   
2. Sélectionnez votre coffre de clés.

3. Sélectionnez le panneau correspondant au type de secret que vous souhaitez gérer (clés, secrets ou certificats).

4. En haut de l’écran, cliquez sur « Gérer les clés/secrets/certificats supprimés ».

5. Un volet contextuel s’affiche sur le côté droit de l’écran.

6. Si votre secret, clé ou certificat ne figure pas dans la liste, il n’a pas été supprimé de manière réversible.

7. Sélectionnez le secret, la clé ou le certificat que vous souhaitez gérer.

8. Sélectionnez l’option de récupération ou de vidage en bas du volet contextuel.

![image](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/dab95f78-1642-4883-b56f-70e1e5320d45)


  > **Résultats** : vous avez exécuté la gestion de la récupération Azure Key Vault avec la protection contre le vidage et la suppression réversible sur le portail Azure.
