# Règle 1 : Nommer correctement les choses

  Nommer correctement les choses signifie donner un nom suffisamment évocateur à la variable que vous vous apprêtez à déclarer, à la méthode, à la classe, à la propriété, à l'interface, bref à tous les objets que vous allez manipuler au sein de votre application.
  
  Cette activité de nommage permet de rendre son code expressif. Un code expressif raconte une histoire. 
  
  L'intérêt de raconter une histoire est qu'une relecture rapide permet de détecter très tôt les éventuelles incohérences, les éventuelles erreurs de conception , permet de se poser très rapidement les bonnes questions, permet d'échanger plus facilement avec les autres développeurs de son équipe.
    
  
  L'objectif de ce chapitre est de vous montrer les méthodes qui vous permettront de trouver le nom le plus évocateur possible pour définir une variable, une méthode ou une propriété.
  
  Trouvez le bon nom peut se révéler être une activité difficile ou chronophage. 
  
  Chaque fois que j'ai rencontré une réelle difficulté à trouver le bon nom, je me suis rendu compte que pour résoudre ce problème, il fallait modifier la conception ou les choix effectués pour développer l'application: dans tous les cas de figure il est apparu que la nouvelle conception ou les nouveaux choix étaient meilleurs que ceux initialement prévus.
  
  Autrement dit nommer correctement les choses a une vertu inédite : détecter très rapidement si un choix technique ou un choix de conception est pertinent.
  
  Si vous êtes responsable d'équipe, je vous recommande d'être à l'écoute des difficultés rencontrées par un développeur quand il doit donner un nom expressif aux différents éléments de son code : c'est un signal très fort de la présence d'un choix de conception ou d'un choix technique qui doit être retravaillé avec l'équipe.
  
  Pour nommer correctement les choses, il est nécessaires de connaître et de respecter dans un premier temps les conventions de nom qui existent au sein du Framework .Net
  
  
## Les conventions de nom du Framework .Net

L'ensemble du Framework .Net a été écrit en suivant les techniques décrites dans le livre : 

[Framework Design Guidelines : Conventions, Idioms and Patterns for Reusable .NET libraries](https://www.amazon.fr/Framework-Design-Guidelines-Conventions-Libraries/dp/0321545613)

Je recommande fortement la lecture de ce livre.

Une partie de cet ouvrage est également disponible en ligne sur [MSDN](https://msdn.microsoft.com/en-us/library/ms229042.aspx).

Chez Microsoft, tous les développeurs suivent les conventions décrites dans ce *Framework Design Guidelines*.

En tant que développeur .Net, vous allez utiliser bon nombre d'outils mis à votre disposition dans le Framework .Net.

Si vous utilisez les conventions décrites dans l'ouvrage *Framework Design Guidelines*, votre propre code semblera être une extension naturelle du Framework .Net. Vous allez pouvoir écrire votre application sous la forme d'une histoire en vous appuyant sur les mots et les verbes du Framework .Net.

La première règle à suivre concerne les conventions de nommage.
Nommer correctement les choses passe par la connaissance et la mise en pratique des conventions de nom existantes dans le Framework .Net.

Ces conventions de nom sont au nombre de deux: 
* Pascal Casing
* Camel Casing


