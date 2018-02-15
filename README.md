# Protocal

Création d'un protocole d'échange d'une requête commune et synchrone venant deux serveurs vers un serveur maître.

Ce protocole est défini en utilisant le langage et les outils de la suite AVISPA.

## Première version du protocole

Cette première version est la première définition de notre protocole, il s'agit d'une vision et d'une représentation naïve du sujet. Nous verrons donc par la suite comment nous avons amélioré cette version. 

* S ------- {Ns.S}_PKc ------------> C
* S <------ {Ns.Nc}_PKs ------------ C
* S ------- {Nc}_PKc --------------> C
* S <------ {OK}_PKs --------------- C
* S ------- {Mess1}_PKc -----------> C
* S <------ {Mess1.Mess2}_PKs ------ C
* S ------- {OK.Mess1.Mess2}_PKc --> C
* S -------------- {Mess1.Mess2}_PKm ------------> M
* S <------------- {OK.rep}_PKs ------------------ M 

Cette première version est présente dans le fichier 

``` 
protocol_v1.hlpsl
``` 

