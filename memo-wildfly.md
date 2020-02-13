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
- L'annotation `@Local` indique que le service est appelé depuis la même instance de JVM. Elle se met sur la classe ou l'interface de l'implémentation du service.
- L'annotation `@Remote` indique que le service est appelé en dehors de la JVM.  Elle se met sur la classe ou l'interface de l'implémentation du service. C'est ce qui est exposé à l'extérieur du système. Le consommateur du service doit avoir confiance envers le service.
- L'annotation `@Stateless` est la plus utilisée car elle est moins couteuses sur la machine. Le service est partagé par tous les consommateurs. Elle se met sur la classe ou l'interface qui expose le service.
- L'annotation `@Statefull` stocke toutes les informations en mémoire. Il y a une notion de permanence. Elle se met sur la classe ou l'interface qui expose le service.
- Une classe peut à la fois porter l'annotation `@Stateless` ou `@Statefull` et l'annotation `@Local` ou `@Remote`.
- L'annotation `@EJB` se met sur un membre d'une classe service. Cela indique au serveur d'application de générer automatiquement une instance. Inutile de l'instancier manuellement avec `new`.
- DTO (ou Data Transfer Object) est également appelé POJO (ou Plain Old Java Object). C'est une classe utilisée pour le transfert d'objet.
- Un Manager est une classe qui manipule les données. Il doit être mis en local.

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
- Vous êtes désormais connecté à Wildfly. La section `Deployments` indique quels projets sont déployés dans Wildfly.

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

## Télécharger un modèle de projet vide pour Wildfly

Parfois vous ne pourrez pas générer automatique de projet Wildfly. Vous pouvez télécharger un modèle tout prêt sur Internet. Un modèle de projet Wildfly est appelé un archétype.

- Allez à l'adresse suivante : [https://github.com/wildfly/wildfly-archetypes/](https://github.com/wildfly/wildfly-archetypes/).
- Dans la page, cliquez sur le menu déroulant `Branch: master`. Cliquez sur l'onglet `Tags` puis sélectionnez `18.0.0.Final`.
- Cliquez sur le bouton `Clone or download` et copiez l'[URI fournie](https://github.com/wildfly/wildfly-archetypes.git).

## Importer l'archétype de projet Wildfly dans Eclipse 

- Dans Eclipse, cliquez sur le menu `File -> Import...`.
- Sélectionnez l'option `Git -> Projects from Git` puis cliquez sur `Next`.
- Sélectionnez l'option `Clone URI` puis cliquez sur `Next`.
- Dans le champ `URI`, collez l'URI récupéré dans la section précédente puis cliquez sur `Next`.
- Laissez les options par défaut et cliquez sur `Next`.
- Dans le champ `Directory`, sélectionnez un emplacement vide puis cliquez sur `Next`.
- A la fin du téléchargement du projet, vérifiez que le sélecteur `Import as general project` est sélectionné puis cliquez sur `Next`.
- Dans le champ `Project name`, définissez un nom de projet puis cliquez sur `Finish`.

Le projet apparait dans le panneau `Project Explorer`.

## Définir la version de Wildfly et la nature du projet

- Faites un clic droit sur le projet et choisissez l'option `Team -> Switch To -> Other...`.
- Sélectionnez l'option `Tags -> 18.0.0.Final` puis cliquez sur le bouton `Check Out`.
- Cliquez sur le bouton `Close`.
- Faites un clic droit sur le projet et choisissez l'option `Configure -> Convert to Maven Project`.

## Tester l'archétype

- Faites un clic droit sur le projet et choisissez l'option `Run As -> Maven build...`.
- Dans le champ `Goals`, saisissez `clean install` puis cliquez sur `Run`.
- Vous pouvez désormais utiliser cet archétype en tant que squelette de base de votre projet Java EE.

## Créer un projet de base avec Eclipse

Vous pouvez créer un squelette de base pour votre projet Java EE directement depuis Eclipse.

- Cliquez sur le menu `File -> New -> Other...`.
- Sélectionnez l'option `Maven -> Maven Project` puis cliquez sur `Next`.
- Laissez les options par défaut et cliquez sur `Next`.
- Dans le champ `Filter` saisissez `wildfly`.
- Dans la colonne `ArtifactId` sélectionnez `wildfly-jakartaee-ear-archetype` et de version `18.0.0.Final` puis cliquez sur `Next`.
- Dans le champ `GroupId`, saisissez le nom du package de votre projet.
- Dans le champ `ArtifactId`, saisissez le nom de votre projet.
- Cliquez sur le bouton `Finish`.
- Quatre nouveaux projets apparaissent dans le panneau `Project Explorer`. Les projets `-ear`, `-ejb` et `-web` sont des projets virtuels qui font référence au projet principal (le projet sans extension). Ces projets contiennent chacun un fichier `pom.xml` qui hérite du fichier `pom.xml` du projet général.

**Remarque :** Si `wildfly-jakartaee-ear-archetype` n'apparait pas dans la liste, suivez la procédure suivante :
- Cliquez sur le bouton `Add archetype`.
- Dans le champ `GroupId`, saisissez `org.wildfly.archetype`.
- Dans le champ `ArtifactId`, saisissez `wildfly-jakartaee-ear-archetype`.
- Dans le champ `Archetype Version`, saisissez `18.0.0.Final`.
- cliquez sur `Next`.

## Déployer un projet sur Wildfly

- Dans l'onglet `Servers` de la perspective `JBoss`, faites un clic droit sur le serveur et sélectionnez `Add and Remove...`.
- Sléectionnez le projet `-ear` à gauche que vous souhaitez ajouter au serveur et cliquez sur le bouton `Add` pour le faire passer à droite. Cliquez ensuite sur le bouton `Finish`.
- Dans le dossier `standalone` où vous avez décompressé Wildfly, le projet doit apparaitre.

**Attention !** Lorsque vous faites une modification du projet à déployer, vous devez à nouveau le déployer sur le serveur. Dans le panneau `Servers`, dépliez le serveur et faites un clic droit sur le projet déployé dans la liste. Choisissez l'option `Full Publish`.
