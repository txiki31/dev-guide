# Utilisation de doc-builder

*doc-builder* encapsule Easybook pour :

* lui ajouter un mécanisme d'intégration de la description du livre à produire.
	
  Une trame permet aux rédacteurs décrire seulement le contenu du livre.
  Les parties générale (couverture, table des matière, information sur l'édition) sont produite par doc-builder.
	  
* ajouter une nouvelle fonctionnalité automatisant la numérotation de chapitre en fonction de son positionnement dans la liste des chapitres et de préciser le niveau du chunk[^1].

_Pour installer doc-builder :_

    $ git clone gitolite@git.anakeen.com:doc-builder


_Usage :_

    /path/to/doc-builder/doc-builder

    [-b|--book <bookDir>]                          (default '.')
    [-t|--theme <themeName>]                       (default 'anakeen')
    [-O|--output <outputDir>]                      (default 'output')
    [-e|--edition <commaSeparatatedListOfEdition>] (default 'web,website')


_Configuration du document_

Pour chacun des documents, un fichier content.yml décrit le livre à produire, il contient :

* le titre du document
* le module concerné
* la version du module
* l'édition du document 
* l'url github utilisée comme lien sur le ruban `github`
* la liste des chapitre 
* la liste des annexes

Par exemple : 

    book:
       title: "Installation & Exploitation"
       module: "Dynacase Platform"
       version: "3.2"
       edition: "1"
       githubsrc: "https://github.com/Anakeen/dynacase-doc-platform-operating-manual"
       chapters: 
           - level:   "1"
             content:  "introduction.md"
           - level:   "1"
             content:  "pre-req.md" 
           - level:   "1"
             content:  "installation-control.md"
           - level:   "1"
             content:  "installation.md"
           - level:   "1"
             content:  "manage-context.md"
           - level:   "1"
             content:  "exploitation.md"
           - level:   "1"
           - number:   "7"
             content:  "postgresql-tuning.md"
           - level:   "1"
             content:  "apache2-tuning.md"
           - level:   "1"
             content:  "control-cli.md"
       appendixes:
           - number:   "A1"
             content:  "module.md"
           - number:   "A2"
             content:  "migration.md"


[^1]: un chunk est l'élément de base du découpage du livre, il correspond à un fichier.
