# Elaboration de la documentation

La rédaction de la documentation se décompose en 4 étapes distinctes :

 * la _rédaction_ : phase durant laquelle le document est écrit. Le rédacteur termine cette tâche lorsqu'il considère la documentation prête à être publiée.
 * la _relecture_ : le relecteur assure un contrôle du document
 * l'_approbation_ : le rédacteur en chef autorise la publication du document
 * la _publication_ : le document est intégré dans le processus de build public

### les documents, leur découpe et leur gestion

Les documents Easybook sont découpés en chunk. 
Dans le cadre de la documentation Dynacase, nous nommerons les chunk des _sections_. Nous travaillerons donc sur des sur des _sections_.
Habituellement, il existe une version d'un document pour une version d'un module (ou de de Dynacase Platform). Le document a donc une version identique à celle du module. Le document vit en parallèle au module au travers d'_éditions_. L'édition est matérialisée par un nombre croissant de 1 à n.
Pour chacune des versions de Core → une version du manuel → n édition.


Ils sont gérés en configuration sous [Github][github].
Il existe une _branche_ Git pour chaque version du document.
Un édition est un matérialisée sous Git par un _tag_ posé lors de sa publication.


### La rédaction

Le rédacteur travaille sur un _fork_ local de la branche de la version concernée. La branche locale de travail est nommée <version>/relecture. Cette branche est buildée et publiée sous [documentation, relecture][doc-review].

Le rédacteur note les points à compléter, à vérifier ou toute partie rédigée comme étant à préciser, à valider d'un point de vue contenu à l'aide de la classe `fixme`, par exemple `<span class="fixme">à compléter</span>` donne <span class="fixme">à compléter</span>. Ils doivent être traités avant la relecture. La mise en place des moyens nécessaires à leur traitement est fait lors des comités de rédaction.

Lorsque le rédacteur considère la section terminée, il fait une pull-request de sa branche locale <version>/relecture vers la branche Anakeen/<version> et demande une relecture au relecteur. Si aucun relecteur n'est désigné, le rédacteur en chef en désigne un.

Suite à la demande du rédacteur, elle doit être réalisée dans un laps de temps raisonnable afin que le rédacteur reste 'dans le bain'. La relecture étant une tâche courte -de l'ordre de l'heure-, elle doit pouvoir être intercalée rapidement dans le flux des travaux du relecteur. En cas de difficulté à assurer cette fluidité, rédacteur et relecteur peuvent en référer au rédacteur en chef.

### La relecture

Chaque tâche de relecture produit une fiche de relecture qui doit être nommée en fonction de la section relue, de la version du document et de son édition. 

La tâche de relecture ne consiste pas à ré-écrire une section -qui est sensée être publiable-. Le relecteur vérifie la complétude, la compréhension, la forme et le respect du règles de rédaction. S'il considère que la section qu'il doit relire n'est pas publiable, il le signale eu rédacteur en chef.

Lors de la relecture, les éléments portant sur la structure ou le fonds du document doivent obligatoirement figurer dans la fiche de relecture. Les remarques de forme, de formulation peuvent être faites dans le texte lui-même, directement dans le fichier source au moyen de la class *`remark`*. <span class="remark">Les normes de codage doivent être respectées <span class="remark">hors sujet</span></span>. Dans l'exemple précédent, le texte a été encadré par une balise `<span class"remark">`, qui a pour effet de mettre en évidence la partie sur laquelle porte la remarque. L'utilisation, imbriquée dans la première, d'une seconde balise `<span class="remark">` permet de noter la remarque. Les corrections orthographiques et grammaticales peuvent être faites directement dans le fichier source.


Le traitement des remarques peut nécessiter des aller-retours qui sont gérés directement entre le relecteur et le rédacteur.

En cas de difficulté pour traiter une remarque, elle est abordée en comité de rédaction. Le rédacteur en chef statue ou organise son traitement.

Lorsque toutes les remarques sont traitées, prises en compte ou ou rejetées, le rédacteur le signale en comité de rédaction. 

Le  rédacteur est responsable de la relecture et de la prise en compte des remarques. En cas de difficulté il peut faire intervenir à tout moment le rédacteur en chef.

Le rédacteur en chef contrôle la fiche de relecture, approuve le document en acceptant la pull request. La section est intégré dans la version publiable du document.
 

### remarque sur le code

Dans le cadre de la rédaction de manuels, des remarques sur le logiciel peuvent être faites : nommage, pertinence, etc. Ces remarques sont enregistrées sur le tracker développement sous la forme d'une *NDLR* -note de la rédaction- pour le projet concerné. Une NDLR décrit la remarque du rédacteur -où relecteur- et est traitée par l'équipe de développement en donnant lieu si nécessaire à des demandes anomalie/évolution.



[doc-review]: https://eec.anakeen.com/documentation/relecture/
[github]: https://github.com/Anakeen/dynacase-doc-core-reference/
[^1]: la balise `<div>` peut aussi être utilisée.
