# Gestion des sources

Utilisation de [github](https://github.com/Anakeen) pour les développements de dynacase

## Présentation

Github est, à tout points de vue, un hébergeur de repo git traditionnel. Il est donc possible de:

 * cloner un repo git
 * puller depuis un repo git
 * pusher vers un repo git
 * etc.

Sa seule différence est qu'en plus de l'hébergement des repos, github offre une interface web.
Cette interface permet de :

* gérer les autorisations
    * chaque utilisateur peut être placé dans plusieurs groupes ("teams")
    * chaque team est liée à un ensemble de repos avec un de ces droits:
        * pull only
        * push & pull
        * push, pull & administrative
* gérer un workflow de contributions: l'interface simplifie:
    * le fork
    * les demandes de pull
    * la consultation (et la récupération) des commits du "[réseau](#le-réseau)" et des diffs

## Quelques notions

### Le repositoy

Le repository est un repository git ordinaire. Il peut soit être

public
:   il est alors visible (et clonable) par toute personne allant sur github

privé
:   il n'est alors visible (et éventuellement clonable) que par les membres des teams ayant suffisamment de privilèges

### le fork

Lorsqu'un utilisateur a la possibilité de voir un repo, il a directement la possibilité de le forker, via un simple bouton sur l'interface.
Cette action va créer dans son compte un clone du repo initial.

Cette action est à la base de tout workflow mis en place sur github: une fois un repo forké, l'utilisateur peut travailler en toute liberté sur sa copie. Il a ensuite, toujours via un simple bouton sur l'interface, la possibilité de solliciter les mainteneurs du repo d'origine pour intégrer ses changements: c'est la "[demande de pull](#demande-de-pull)".

### Le réseau

C'est l'ensemble de tous les repos obtenus par des forks successifs.
C'est à dire que chaque fois qu'un utilisateur forke un repo d'un reseau, son fork devient membre du réseau.

Si le repo à l'origine du réseau est privé, alors tout le réseau est privé.

### La demande de pull

Lorsqu'un utilisateur veut voir ses changements de code intégrés au repo de départ, il fait une "demande de pull".
Il va alors préciser quelle est la branche qu'il propose, et vers quelle branche il propose ses corrections.

Cette demande de pull va générer une notification chez l'ensemble des membres ayant le droit de pusher sur le repo concerné.
Ils pourront alors, via l'interface:

1. Faire une "revue":
    * voir le résumé de ces changements (commits et fichiers impactés)
    * voir le diff complet
    * commenter la demande de pull
        * de façon gobale,
        * ou directement sur certaines lignes des fichiers impactés
2. accepter ou refuser les changements

Note: la partie "revue" peut être itérative: les commentaires permettent de réelles discussions
avec l'ensemble des utilisateurs ayant le droit de voir le réseau.

## Concrêtement

### Organisation Github

Pour chacun des modules Dynacase, il existe un dépôt Github nommé *dynacase-<module>*, par exemple dynacase-core, dynacase-dashboard.

A chaque version du module correspond deux branches :

* *<version>* : branche _stable_ de la version
* *<version>-integration* : branche d'intégration de la version

Une révision est un tag sur la branche.

### Comment travailler

Le développeur doit :

1. avoir un compte Github :)
2. lire la doc
3. faire un fork perso de la branche correspondant à la version du module sur lequel il souhaite contribuer
4. travailler encore et toujours
5. faire un _pull request_ de sa branche vers la branche d'intégration

#### travailler encore et toujours




<div class="fixme">


## Le workflow proposé pour débuter

### Point de départ

Partons de la situation suivante:

* [L'*organisation* Anakeen](https://github.com/organizations/Anakeen/) a un repo *dynacase3*.\
  Ce repo est public (Ce qui veut dire que, comme dans le modèle actuel,
  tout le monde peut voir les sources et les cloner, travailler dessus dans son coin,
  et éventuellement proposer des corrections de son cru).\
  Il est composé comme suit:
    * branches:
        * master
        * next-release
        * next-release-integration
    * tags
        * 3.0 -> pointe vers la dernière version stable 3.0.*
        * 3.0.18,
        * 3.0.17
        * ...
* la *team "dynacase 3 - admin"* a les droits *push, pull & administrative* sur ce repo.
  Elle est composée de 
    * Eric,
    * Marc
* la *team "dynacase 3 - workers[^dynacase3-workers]"* a les droits *push & pull* sur ce repo.
  Elle est composée de 
    * Eric,
    * Marc,
    * Jerome,
    * Arnaud,
    * Clément,
    * Charles,
    * Matthieu

### travail seul sur une "issue[^issue-feature]"

L'issue #1234 (au sens redmine, c'est à dire anomalie ou évolution / amélioration) est affectée à Jérome.
Il a pour consigne de développer cette issue pour la prochaine release (peu importe son numéro).\
Jérome forke `anakeen/dynacase3` (dans `jerome/I-1234`).\
Pour réaliser ce fork, il se connecte à l'interface de github et, depuis son dashboard, il sélectionne
le contexte "*anakeen*"; ensuite il choisit dans la liste des repos qu'il voit le repo "*dynacase3*".
Il ne lui reste plus qu'à cliquer sur le bouton "*fork*".\
Il travaille ensuite *comme il le souhaite* sur cette issue.

En prévision de la prochaine release, Eric souhaite voir comment ce que fait Jérome pourra être intégré.
Il se connecte donc à son compte, sélectionne depuis son dashboard le contexte "*anakeen*",
puis le repo "*anakeen/dynacase3*".\
Il peut ensuite aller sur "*fork queue*" qui lui montre la liste des commits effectués sur le réseau,
et qui ne sont pas encore intégrés. pour chacun de ces commits, il a un indicateur (la couleur)
qui lui dit si le merge se ferait directement, ou s'il génèrererait des conflits.\
Note: pour le moment, cela n'est qu'une information générale, puisque Jérôme n'a pas signalé avoir terminé.

Lorsque Jérome a terminé sa correction, il pushe tous ses changements.
Il crée ensuite la branche `jerome/I-1234:I-1234-integration`.
Dans cette branche, il merge `anakeen/dynacase3:next-release-integration`, puis il la pushe[^before-pushing-integration].
Il se connecte ensuite à son interface github, et fait une demande de pull
pour intégrer `jerome/I-1234:I-1234-integration` à `anakeen/dynacase3:next-release-integration`.

Eric reçoit une notification (par mail, s'il l'a activé, et via l'interface).
Il se connecte à son compte github, et dans le contexte anakeen, sélectionne "*Pull requests*".
Il trouvera ici (éventuellement parmi d'autres) la demande de Jérome.\
Il peut alors commenter, voire demander à Matthieu de faire une relecture de code^[Note: Jérome a également
eu la possibilité de demander une relecture de code à matthieu sur n'importe lequel de ses commits].
Cette relecture de code se fait dans l'interface, sans avoir besoin de cloner / puller / fetcher quoi que ce soit.\
Une fois satisfait (éventuellement après plusieurs refus), Eric merge la demande de Jérome.

### travail à plusieurs sur une issue / un groupe d'issues

Matthieu et Charles doivent travailler respectivement sur les issues M1234 et C1234.
Comme ces issues sont fortement liées, on leur demande de travailler ensemble, et de soumettre
pour la prochaine release le résultat du merge de leur travail. Ce sera Charles qui sera responsable
de ce merge.

charles forke `anakeen/dynacase3` (dans `charles/I-C1234-M1234`),
puis il crée une branche `charles/I-C1234-M1234:IC1234`.\
Matthieu forke `charles/I-C1234-M1234` (dans `matthieu/I-C1234-M1234`),
puis il crée une branche `matthieu/I-C1234-M1234:M1234`\
Les 2 travaillent et mergent quand nécessaire, puis peuvent, au choix, se faire des pull request,
ou alors passer par l'interface offerte par "*fork queue*" pour prendre les commits un par un.

Ils suivent alors la même démarche que Jérome précédemment pour finir par proposer l'intégration de 
`charles/I-C1234-M1234:IC1234:I-C1234-M1234:IC1234-integration` dans `anakeen/dynacase3:next-release-integration`,
qui sera au final intégrée ou non par Eric.

### Publication d'une nouvelle release

#### Intégration / corrections

À un moment donné, on décide que plus aucune fonctionnalité ne sera intégrée à la prochaine release,
et on passe à l'intégration de cette prochaine release.\
Les développeurs corrigent dans leurs branches respectives leurs issues jusqu'à ce que le fonctionnement
de `anakeen/dynacase3:next-release-integration` soit satisfaisant.

#### publication

Une fois `anakeen/dynacase3:next-release-integration` prêt à être publiée,
on la merge sur `anakeen/dynacase3:master`, et on pose le tag de version, choisi à ce moment là.

## Ressources

### Remarques sur la "*fork queue*" et le "*cherry-picking*"

La fork queue est décrite [ici](https://github.com/blog/270-the-fork-queue).

Pour information, la "*fork queue*" est réellement une interface au "*[cherry-picking](http://progit.org/book/ch5-3.html#rebasing_and_cherry_picking_workflows)"*, avec les avantages et inconvénients que cela peut apporter.
Je vous invite, pour les plus courageux, à lire [ce très bon article sur la fork queue](http://rjbs.manxome.org/rubric/entry/1755), et surtout ses commentaires avant de faire un usage intensif de cette fonctionnalité trop attrayante.
Pour le résumer, le cherry-picking, même s'il ne pose pas de problème technique pour les merges
(car, contre toute attente, git s'en sort très bien avec les conflits liés au cherry-pickig, et qui en fait n'en sont pas),
crée des entrées dupliquées dans l'historique. Il est, la plupart du temps préférable d'utiliser `git merge <commit sha-1>` à la place
(pour aller plus loin, vous pouvez lire également [cet article sur les alternatives au cherry-picking](http://gitready.com/intermediate/2009/03/04/pick-out-individual-commits.html)

### Remarques et discussions sur les repo / branches de travail et le rebase

Une suggestion que je ferais est la suivante:

* les branches suivantes doivent **absolument rester stables**:
    * Anakeen/dynacase3:dev
* Les branches suivantes peuvent être rebasées à tout moment[^autre-repo-pour-rebase]
    * Anakeen/dynacase3:next-release
    * Anakeen/dynacase3:next-release-integration
    * <dev>/*
* on demande aux développeurs de systématiquement faire des `pull --rebase` (cf: http://gitready.com/advanced/2009/02/11/pull-with-rebase.html) (cela peut être ajouté a .git pour éviter les oublis)
* ca permet également le cherry-picking sans polluer l'historique.
* plutot que de merger leur travail avec `anakeen/dynacase3:next-release-integration` avant de faire une
pull request, les développeurs doivent rebaser sur `anakeen/dynacase3:next-release-integration`
(le `git pull --rebase` évoqué précédemment)

Afin de clarifier les choses, et d'éviter que d'éventuels hypothétiques contributeurs ne clonent des
trucs rebasables, on peut imaginer l'organisation des repo comme suit:

* un repo Anakeen/dynacase3 public, contenant
    * branches:
        * master
    * tags
        * 3.0 -> pointe vers la dernière version stable 3.0.*
        * 3.0.18,
        * 3.0.17
        * ...
* un repo Anakeen/dynacase3-dev, contenant
    * branches:
        * next-release
        * next-release-integration
        * \<les branches des issues une fois leur release de destination intégrée\> càd:
            * I-C1234-M1234 (récupéré depuis Charles/I-C1234-M1234/master, puis Charles/I-C1234-M1234/master est supprimé)
            * I-1234 (récupéré depuis Jerome/I-1234/master, puis Jerome/I-1234/master est supprimé)
            * ...
              Cela a le mérite de permettre facilement 
                * "l'interchangeabilité" des développeurs pour la maintenance
                * de ne pas "polluer" les repos des developpeurss avec des développements terminés
                * de mieux gérer la consommation d'espace

@Eric, @Jérome: j'attends vos retours sur cette partie.


### De très bonnes pages d'explications sur le blog github

* [Leur wiki d'aide, à parcourir](http://help.github.com/)
* [Un aperçu des branches, et de leur positionnement relatif](https://github.com/blog/611-branch-lists)
* [vue de comparaison](https://github.com/blog/612-introducing-github-compare-view)
* [vue de comparaison cross repos](https://github.com/blog/683-cross-repository-compare-view)
* [comment filtrer dans gmail les notifications de github](https://github.com/blog/695-easily-filter-notifications-by-repository)


### Quelques outils pouvant être utiles

* Des outils pour simplifier la ligne de commande quand le repo est github
    * https://github.com/defunkt/github-gem#readme
    * https://github.com/defunkt/hub#readme
* un plugin redmine pour pas devoir tout se cloner ~~à la main~~avec cron
    * http://mentalized.net/journal/2009/08/03/redmine_plugin_github_hook/

[^dynacase3-workers]: Oui, je sais, il va falloir trouver un meilleur nom...
[^issue-feature]: La notion de *feature* dont on a pu discuter avec certains va, tant que possible,
être "masquée" ici pour ne pas alourdir le workflow.
[^before-pushing-integration]: On peut prévoir ici un certain nombre de points de contrôle avant le push:
TU, si nécessaire tests d'interface, etc.

</div>
