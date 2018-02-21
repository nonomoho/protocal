# Protocal

Création d'un protocole d'échange d'une requête commune et synchrone venant deux serveurs vers un serveur maître.

Ce protocole est défini en utilisant le langage et les outils de la suite AVISPA.

## Création d'un plugin pour faciliter le développemnt

Nous avons remarqué qu'il y avait de nombreuses erreurs de compilation lors de l'écriture puisqu'il est difficile de ne pas se tromper dans la syntaxe avec un éditeur de texte sans coloration.
Avec Visual Studio Code (VSC) nous pouvons facilement créer un plugin pour obtenir de la coloration de nos fichiers. Grâce à la [documentation](http://www.avispa-project.org/) du projet Avispa nous avons pu nous faciliter l'écriture des protocoles et mieux comprendre la grammaire hlpsl.
L'extension est présente dans le market de VSC sous le nom de __hlpsl__.

## Première version du protocole

Cette première version est la première définition de notre protocole, il s'agit d'une vision et d'une représentation naïve du sujet. Nous verrons donc par la suite comment nous avons amélioré cette version.

```text
S ------- {Ns.S}_PKc ------------> C
S <------ {Ns.Nc}_PKs ------------ C
S ------- {Nc}_PKc --------------> C
S <------ {OK}_PKs --------------- C
S ------- {Mess1}_PKc -----------> C
S <------ {Mess1.Mess2}_PKs ------ C
S ------- {OK.Mess1.Mess2}_PKc --> C
S -------------- {Mess1.Mess2}_PKm ------------> M
S <------------- {OK.rep}_PKs ------------------ M
```

Cette première version est présente dans le fichier _protocol_v1.hlpsl_

### Choix pour la première version

Nous avons choisi de faire communiquer d'abord les deux premiers serveurs Shell et Code (S et C) pour construire le message.

```text
S ------- {Ns.S}_PKc ------------> C
S <------ {Ns.Nc}_PKs ------------ C
S ------- {Nc}_PKc --------------> C
```

Les deux serveurs commencent par s'identifier à l'aide de nonces et des clefs publics.

```text
S <------ {OK}_PKs --------------- C
S ------- {Mess1}_PKc -----------> C
S <------ {Mess1.Mess2}_PKs ------ C
S ------- {OK.Mess1.Mess2}_PKc --> C
```

Lorsque les deux serveurs ce sont identifiés, c'est à dire à la réception du OK venant de C, ils construisent ensemble le message à envoyer au serveur Master (M).

```text
S -------------- {Mess1.Mess2}_PKm ------------> M
S <------------- {OK.rep}_PKs ------------------ M
```

C'est le serveur S qui est en charge de communiquer avec le serveur M. S envoie donc le message complet créé précédement et attend la réponse de M.

### Points à améliorer à la v1

* Les premiers échanges peuvent être intégrer à la construction du message
* La réponse n'est connu que par le serveur "Shell" et non par "Code"
* Ajouter des "goals" : secret et witness / request
* Nous ne nous sommes pas encore posé toutes les questions de sécurité puisque nous n'avons pas encore d'intru.

## Deuxième version du protocole

Correction des messages (on a changé de méthode d'envoi)

Création du rôle session et ajout des  sessions
Création des goals (secrecy nonces)

On a supp le M dans shell et code car pas utilisé et comme full example on va faire un truc badass avec un unique master masterisé

### Points à améliorer à la v2

* Le protocole n'est pas safe sur un test simple (avec une session comprenant un intrus)
* Faire plus de tests (avec des sessions différentes)
* Il faut créer un deuxième goal (authentication par exemple) -- Amélioration de la V3