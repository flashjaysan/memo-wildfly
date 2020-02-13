# Mémo Wildfly

## Définitions

- Un serveur d'application Java EE fournit toutes les implémentations des diverses spécifications de Java EE.
  - IBM propose Websphere.
  - Sun puis Oracle proposent Glassfish (qui est également l'implémentation de référence des spécifications).
  - Redhat propose JBOSS et Wildfly.
- Une servlet est un serveur HTTP. Tomcat fait partie de cette catégorie.
- Les API de la spécification Java EE se groupent en trois catégories :
  - Les composants : EJB, servletes, JSP.
  - Les services : JDBC, JTA/JTS, JNDI, JCA, JAAS.
  - La communication : RMI-IIOP, JMS, Java mail.
- Un EJB (ou Entreprise Java Bean) est une classe qui décrit ce qu'elle peut faire.
- Un EJB de session est une interface qui présente des services qui peuvent être consommés localement (avec l'annotation `@Local`) ou à distance (avec l'annotation `@Remote`). Les services sont sans état (avec l'annotation @Stateless) ou avec sauvegarde de l'état (avec l'annotation @Statefull).
- L'annotation `@Local` indique que le service est appelé depuis la même instance de JVM.
- L'annotation `@Remote` indique que le service est appelé en dehors de la JVM. C'est ce qui est exposé à l'extérieur du système. Le consommateur du service doit avoir confiance envers le service.
- L'annotation `@Stateless` est la plus utilisée car elle est moins couteuses sur la machine. Le service est partagé par tous les consommateurs.
- L'annotation `@Statefull` stocke toutes les informations en mémoire. Il y a une notion de permanence.
- DTO (ou Data Transfer Object) est également appelé POJO (ou Plain Old Java Object). C'est une classe utilisée pour le transfert d'objet.
- Un Manager est une classe qui manipule les données.

**Conseils :**

- On ne fournit jamais la structure des entités aux utilisateurs.
- Il faut laisser un maximum la main au serveur.
- Il faut préférer la gestion automatique des transactions.

## Principe de déploiement de Java EE

- Un JAR (ou Java ARchive) est une bibliothèque de classes.
- Un WAR (ou Web ARchive) est destiné au web et peut contenir des JAR.
- Un EAR (Entreprise ARchive) est le modèle entreprise et peut contenir des JAR et des WAR.

Dans un Tomcat, les JAR ne sont pas exécutés.

Pour déployer un projet, il faut déposer l'EAR sur le serveur d'application.

Pour JBOSS, pour le démarrage, on peut être en mode *domain* ou en mode *standalone*.

- Le mode *domain* indique qu'il y a un serveur maître et deux esclaves.
- Le mode *standalone* indique qu'il n'y a qu'un serveur.

## Installer et démarrer Wildfly directement

- Téléchargez la version 18 de Wildfly sur [le site officiel](https://wildfly.org/downloads/).
- Décompressez l'archive à l'emplacement de votre choix. Prenez soin de noter cet emplacement.
- Pour lancer le serveur d'application sur Windows, exécutez le fichier `standalone.bat` situé dans le dossier `bin`.
- Pour fermer le serveur, appuyez sur `CTRL+C` puis saisissez `O` et validez.

## Créer un compte administrateur pour Wildfly

- Sur Windows, placez-vous dans le dossier `bin` de Wildfly puis dans la barre d'adresse de l'explorateur de fichiers, saisissez `cmd` puis validez. Cela ouvre une console à cet emplacement. Exécutez le fichier `add-user.bat`.
- Saisissez `a` pour ajouter un compte administrateur (*Management User*) puis validez.
- Saisissez le nom d'utilisateur du compte puis validez.
- Saisissez un mode de passe pour ce compte puis validez.
- Si besoin confirmez ou recommencez en suivant les recommendations.
- Saisissez un nom de groupe à associer au compte ou laissez le champ vide puis validez.
- Saisissez `yes` pour finaliser la création du compte.
- Saisissez `yes` à la dernière question (je ne sais pas trop ce que ça fait).

## Se connecter à l'administration du serveur via navigateur

- Démarrez Wildfly.
- Utilisez votre navigateur pour vous rendre à l'adresse `localhost:9990/console`.
- Saisissez l'identifiant et le mot de passe du compte administrateur puis validez.

## Installer le plugin Wildfly dans Eclipse

- Cliquez sur le menu `Help -> Eclipse Marketplace...`.
- Dans l'onglet `Search`, dans le champ `Find`, Saisissez `` puis cliquez sur le bouton `Go`.
- Cliquez sur le bouton `Install` du plugin `JBoss Tools 4.13.0.Final`.
- Une fois l'installation terminée, fermez la fenêtre.

## Configurer Eclipse pour Wildfly

- Cliquez sur le menu `Window -> Preferences`.
- Dans le menu `Web Services -> Server and Runtime`, sélectionnez `Wildfly 18` dans le menu déroulant `Server runtime`.
- Sélectionnez `JBossWS` dans le menu déroulant `Web service runtime`.

## Ouvrir la perspective JBOSS

- Cliquez sur le menu `Window -> Perspective -> Other Perspective -> Other...`.
- Sélectionnez `JBoss` puis cliquez sur le bouton `Open`.

## Sélectionner le serveur d'application Wildfly

- Dans l'onglet `Servers`, cliquez sur le texte `No servers are available.Click this link to create a new server...` ou faites un clic droit dans la fenêtre et choisissez `New -> Server` pour associer un nouveau serveur d'application à Eclipse.
- Sélectionnez `Wildfly 18` puis cliquez sur le bouton `Next`.
- cliquez sur le bouton `Next`.
- Si la fenêtre vous demande de sélectionner un runtime, cliquez sur le bouton `Browse` de la section `Home Directory` et sélectionnez l'emplacement (le dossier racine) où vous avez décompressé l'archive Wildfly.
- Cliquez sur le bouton `Finish`.

## Démarrer Wildfly depuis Eclipse

- Dans l'onglet `Servers` de la perspective `JBoss`, faites un clic droit sur le serveur Wildfly et sélectionnez `Start` ou cliquez sur le bouton en forme de flèche verte dans la fenêtre.
- Pour stopper le serveur, faites un clic droit sur le serveur et sélectionnez `Stop` ou cliquez sur le bouton en forme de carré rouge dans la fenêtre.

## Déployer un projet sur Wildfly




