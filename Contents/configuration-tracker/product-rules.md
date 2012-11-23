# Règles produits Anakeen

## Compatibilités

### Dynacase Platform

Une montée en version doit garantir une compatibilité avec les données existantes. Pour cela, la mise à jour d'un produit Dynacase doit assurer la migration des données si nécessaire. Cette migration doit être automatisée. Il est accepté que les migrations lors d'une montée en version nécessite une intervention humaine.

### Dynacase Control

Une seule version de Dynacase Control est utilisable à un instant donnée. il doit donc :

* être compatible avec les versions supportées 
* permettre la montée en versionvers la première version supportée depuis la version précédente

## Obsolescence

L'obsolecence concerne toutes parties visibles des produits : interface homme-machine pour les utilisateurs, API et modules pour les intégrateurs.

Les règles de communication des obsolescences doivent permettre aux utilisateurs et intégrateurs de les identifier, anticiper et organiser les changements nécessaires pour les prendre en compte.

Lors de l'annonce de la sortie d'une version, ou rapidemment suite à sa sortie, les obsolescences sont présentées.

L'obsolescence annoncée sur une version V peut être applicable à la version[^1] :

* V+1 si la solution de remplacement est connue et utilisable en version V;
* > V+1 dans les autres cas.

Anakeen s'engage à diffuser au plus tôt les informations nécessaires pour traiter les futures obsolesnces.

## Processus développement 

### Modification du produit

La modification du produit est concerne toutes les parties visibles du produit : les IHM, les API de programmation et divers format de paramétrage, la documentation, etc.

Toutes les modifications de produit sont validées par la direction technique. 


[^1]: version minimale d'application
