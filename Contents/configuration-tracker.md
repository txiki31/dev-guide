# Organisation du développement

L'ensemble des développements Dynacase et de ses modules produisent des versions successives.
Une version est définie par l'ensemble des anomalies ou évolutions qu'elle intègre.

Pour gérer de manière cohérente cela, et assurer une traçabilité des travaux réalisés sur les différentes versions des modules, nous utilisons une gestion de configuration [git](http://git-scm.com/) couplée à un outil de suivi de demandes [redmine](http://www.redmine.org/).

Ce chapitre décrit l'organisation du développemengt et fixe les règles de gestion de configuration du produit.

## Nommage des versions et release

Les produits sont Dynacase Platform et Dynacase Control.
Chaque produit est découpé en module, en particulier dans le cas de Dynacase Platform.

Il existe donc des *versions* du produit et des *versions* de module. 
La version du produit pouvant être vue comme un inventaire des versions des modules qui le compose.

Les versions sont notées *X.Y*.   

Pour un module, et par conséquence pour le produit auxquel il appartient, il peut être nécessaire de produire des versions intermédiaire ou version de maintenance.
Ces versions intermédiaires sont nommées *release*. Elles sont notée X.Y.*R*, X.Y étant la version.

La release d'une module est incrémentée lors d'une nouvelle publication de ce module.
La release d'un produit est incrémentée dès que la release d'un des modules le composant est incrémentée.

Pour le produit, ce nommage est décidé par la direction générale.  
Pour les modules, c'est la direction technique qui donne les numéros de version.
Les releases produit et module sont incrémentées par décision de la direction technique.

Pour les modules, il existe la notion de buildid noté X.Y.R-*buildid*.   
Chaque nouvelle release est publiée avec un buildid égal à *0*.  
Il est possible de publier un module avec un simple incrément du buildid. Cela signifie qu'il n'y pas eu de modification du source du module, mais seulement un modification lors de sa production : gestion des dépendances par exemple.  
Lors du process de développement d'un module la gestion du *buildid* est sous la responsabilité du release manager du module.


## Version et contenu

Toute modification du source[^1] doit être issue d'une demande [redmine]. La prise en compte d'une demande est une décision de la direction technique.
Chaque release d'un module est décrite par une entrée dans la roadmap du module sur le suivi de demandes.

La première release d'une version produit au travers de ses modules peut intégrer des demandes de type *évolution* ou *anomalie*.

Les releases suivantes produit et module, n'intègre que des corrections d'anomalie.

Un nouveau module peut lui être intégré sur une release du produit.

Ce fonctionnement garantie la stabilité en terme, de fonctionnement mais surtout, de périmêtre fontionnel du module et de la version.


## Évolution vs anomalie

Une anomalie est une modification du source du module n'ayant pas d'impact sur les interfaces de programmation, les interfaces utilisateur ou le fonctionnement de Dynacase.  

la logique de gestion des versions et release permet de garantir que pour une version du produit, il n'y aura pas de travaux de réécriture de code entraîné par la modification de l'interface de programmation, de l'algorithmie ou de l'interface utilisateur.

Le type de demande *amélioration* est introduit pour permettre l'intégration sur une version d'une évolution mineure n'ayant toujours pas d'impact api, ihm ou algorithmique.

## Publication

La publication d'une version du produit permet de builder l'ensemble des modules la composant et la mettre à jour sur les espaces EEC.

Les espaces EEC public sont mis à jour lorsqu'une version du produit a plus de 6 mois.

Les espaces EEC privés des contractants EEC sont mis à jour avec la dernière version.

La publication est sous la responsabilité du directeur technique et est systématique annoncée par la diffusion d'une mail à tous les reponsables de contrats EEC et interlocuteurs techniques désignés. Ce mail présente les changements réalisés.

Il existe un dépôt par version. Seule la dernière release est présente dans le dépôt.

[^1]: il s'agit ici de source au sens large, c'est à dire de l'ensemble des éléments nécessaires à la production d'un module : code, procédure de build, documentation, etc.
