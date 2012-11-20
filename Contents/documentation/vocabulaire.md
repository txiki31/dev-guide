
# Guides de rédaction

## Glossaire

Ce chapitre fixe des éléments de vocabulaire utilisés dans pour l'ensemble des documentations produites.

action
:   Une action Dynacase réalise une fonction d'une application. Cette action reçoit des paramètres, réalise un traitement et retourne le résultat de ce traitement. L'action Dynacase est composée de deux parties : le traitement et la représentation du résultat du traitement. Chacune de ses deux parties est optionnelle mais il en faut au moins une des deux. Le traitement est réalisé à l'aide d'une fonction PHP qui utilise des fonctions de l'API Dynacase. La représentation est réalisée à l'aide d'un template. Ce template permet de réaliser des sorties HTML avec des parties dynamiques.

application
:   Une application Dynacase permet de couvrir une fonctionnalité spécifique, par exemple: gestion des utilisateurs, administration des contrôle qualité. Une application utilise souvent une ou plusieurs familles de document afin de réaliser leurs fonctions. Une application Dynacase est composée d'une ou plusieurs actions actions. Une application possède généralement une interface principale qui permet d'accéder à l'ensemble des actions nécessaires à l'application. Une application est accessible directement par une url directe et est considéré comme autonome vis-à-vis d'autre application.

attribut
:   Un attribut de document défini un type syntaxique (texte, nombre, date, …) ainsi que son emplacement dans la structure d'information du document.

consultation
:   Exprime la modalité permettant uniquement de consulter un document

cycle de vie
:   Le cycle de vie définit les différentes étapes du document. Le passage d'une étape à la suivante, appelé transition, est contrôlé par le cycle de vie : contrôle sur la complétude du document, contrôle de l'utilisateur agissant, etc. Les transitions peuvent agir sur le document -application de droits, modification de contenu, etc.- ou interagir avec d'autre objets Dynacase et déclencher des actions externes à Dynacase -envois de courriel par exemple. Le cycle définit aussi pour chacune des étapes les activités, rôle et état appliqués au document. eél'ensemble des activités à réaliser, les états et transitions possibles du documents. Un cycle peut être associé à un document; dans ce cas le document est soumis aux contrôles imposé par le cycle. à chaque changement d'état, l'ancien état du document est conservé afin de tracer et de pouvoir voir les informations des états précédents.

document
:   Le document Dynacase contient un ensemble structuré d'informations. Il peut être associé à un cycle de vie et porte ses propres paramètres de sécurité d'accès. Un document est toujours associé à une famille de document.

famille
:   La famille permet de donner une unité à un ensemble de document de même type sémantique (compte-rendu, facture, client, …). La famille défini la structure de l'information qui sera commune à l'ensemble des documents de cette famille. Cette structure est composée d'attributs du document. Elle défini aussi les règles de sécurités d'accès et l'accès au cycle de vie.

interface
:   L'interface Dynacase est la représentation d'une action.

lignée documentaire
:   C'est l'ensemble des révisions d'un document

modification
:   Exprime la modalité d'édition/modification d'un document

module
:   Un module Dynacase contient la définition et l'ensemble des éléments nécessaires au fonctionnement de zéro, une ou plusieurs applications. Elle contient la définition et l'ensemble des éléments nécessaires (cycle de vie, profil, ….) à l'utilisation de zéro, une ou plusieurs familles.

profil
:   Le profil d'un document décrit une matrice de droits. Les droits les plus usuel sont 'voir','modifier', 'supprimer'. Pour chacun des ces droits, le profil défini au travers de rôles quels groupes d'utilisateurs ou quels utilisateurs en particulier ont cette habilitation. Les droits des groupes sont propagés automatiquement sur les membres de groupes et des éventuels sous-groupes.Le même profil peut être partagé par plusieurs documents. Cela permet de modifier plus facilement les accès à un ensembles de document de même niveau de sécurité. Généralement, un même profil est partagé par les documents d'une même famille.

représentation
:   la mise en forme des informations portées par un document pour affichage (HTML), impression (OpenText Document), échange avec un autre sysème informatique (XML, JSON) utilise une représentation du document. Cette représentation est généralement associé à un modèle qui lui confère un aspect particulier. Une représentation permet aussi masquer ou de démasquer une ou plusieurs informations par le biais des visibilités.

rôle
:   <fixme>

template
:   Le template est le modèle de représentation. Ce modèle est généralement du HTML avec des parties dynamiques qui sont construite dans le traitement de l'action. Ce modèle peut aussi être n'importe de n'importe quel type ascii tel que csv ou xml.  Le seul modèle binaire possible est le format openDocumentText. Il peut toutefois être transformé en PDF ou MS Word sous certaines conditions. Ce type de modèle permet d'avoir des représentations utilisables pour des besoins d'impressions. Ces modèles sont utilisés pour les représentations des actions et aussi pour les représentation de documents.

visibilité
:   <fixme>

workflow
:   Enchaînements de tâches, les wo

zone
:   Une zone Dynacase est une action qui ne peut pas être appelée directement depuis l'interface principale. Une zone peut être considéré comme un fragment d'action. Sa représentation est souvent un fragment HTML -le contenu d'une `<div>` ou d'une `<table>` par exemple-. La zone est réutilisable dans différentes représentations d'actions. Elle permet de réutiliser des fragments d'interface pour construire des différentes interfaces de plus haut niveau. Une zone peut elle même faire référence à d'autres zones. On peut ainsi assembler des interfaces avec des niveaux différents réutilisables.



## Points particuliers

* mail ou courriel : préférer *courriel*
* timer ou minuteur : préférer *minuteur*
* workflow ou cycle de vie : le premier désigne un ensemble, un flux de tâche alors que le second couvre les étapes parcourues par le document. Le workflow permet de dérouler le cycle de vie du document. Mais aussi, le cycle de vie du document pilote le workflow des activités. 
* les termes informatiques ou techniques doivent être transcrits tels qu'ils sont utilisés `true`/`false` (et non pas vrai/faux). Exemple : la condition est fausse si la fonction retourne `false`.
* hash = hash


## Du bon usage des .... {#dev-guide:d593d7ef-e443-4606-af57-719221248a10}

ancre/renvoi  
:   Une ancre est posé avec la syntaxe `{#<module>-<doc>:<uuid>}`

   avec l'identifiant de l'ancre composé de :
      * _module_ : nom du module en lettre minuscule, par exemple : core, documentgrid
	  * _doc_    : document : ref pour manuel de référence, exploit pour installation et expploitation
	  * _uuid_   : uuid généré avec `uuid` ou `uuidgen`
	  
   le renvoi vers une ancre est décrit avec la syntaxe `{#identifiant de l'ancre}`


bouton
:  pour représenter des boutons, utiliser la représentation `[bouton]`

code
:  le code est présenté dans des _blocs_
   
   
     [code php]
     ...
     $exemple = monCodePhp();
     ...
      
   ou en ligne avec les _graves accents_ -[ou simple opening quote, ou encore backquote, 0X60 ascii][backquote]- `if (is_array($exemple))`.
   
image
:   <span class="fixme">image</span>

    * légende / titre
	* alignement
	* capture d'écran : comment

lien
:   préférer la notation avec renvoi pour les liens -cf. [mardown links][markdow-links]- au url en ligne pour améliorer la lisibilité

menu
:   pour décrire des menus et sous-menus utiliser la notation ` items l1 > item l2 > item`

liste à puce vs liste de définition
:   la liste à puce est une énumération de mots, de proposition ou de phrase. 
    La liste de définition est une liste de terme avec pour chacun d'eux une définition. Le terme est mis en évidence.
    Pour les listes de définition, utiliser la syntaxe  [PHP Markdown Extra definition lists][php-mardown-deflist].

renvoi
:   [Voir le point sur les ancres](#dev-guide:d593d7ef-e443-4606-af57-719221248a10)


[markdow-links]: http://daringfireball.net/projects/markdown/syntax#link
[php-mardown-deflist]: http://michelf.ca/projects/php-markdown/extra/#def-list
[backquote]: http://fr.wikipedia.org/wiki/Discussion:Guillemet
