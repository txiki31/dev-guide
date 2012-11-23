# Comment tester {#dev-guide:comment-tester}

## les TAUFU ou Tests AUtomatisés Fonctionnel Unitaire

Pour chacun des modules dynacase, une série de tests automatisés doit être produite. Ces tests sont écrits afin qu'ils soient évalués avec le logiciel PHPUnit.

Ces tests écrit contiennent le code des tests ainsi que les données nécessaires aux tests. 

L'ensemble des données nécessaire au test (code + données) sont présents dans les sources du module. Le répertoire Test à la racine des sources du module contiendra les tests.

Si un module contient un répertoire Test, le lancement de la génération du module construira deux fichiers webinst : un pour le module (original) et un pour les tests. Ainsi il sera possible d'installer ou non les tests automatisés liés au module.

Ce module de test doit être installé sur un contexte vierge dédié aux tests ou sur un contexte de développement. Il ne doit pas être installé sur un serveur en production. Son rôle est de tester les développements d'un module dynacase. Il n'a pas pour rôle de tester une configuration en production. 

### Qu'est ce qu'un test

Le test sert à vérifier un comportement d'une fonctionnalité ou d'une méthode de classe. 
Un test fait partie d'un ensemble de test appelé "suite de tests".
Cette suite regroupe un ensemble de test portant sur une même fonctionnalité ou sur une classe particulière.

Exemple de suite de test : "Gestion de contenu de dossier". Cette suite comprend les tests suivants :

* test d'insertion d'un document sans contrainte
    * jeux d'essai avec des documents non dossier, des documents dossier, des document révisé, des documents avec cycle de vie
    * vérification sur le nombre de document insérés
    * vérification sur les identifiants des documents insérés
* test d'insertion de documents par lot
    * lots de 0, 1, 5 , 10 et 100 documents
* test d'enlèvement d'un document
    * après insertion , enlèvement
* test de déplacement d'un document d'un dossier vers un autre
* test de nettoyage de document
* test des cas d'erreurs
    * identifiants non existants
    * contrainte de type

### Comment écrire un test

Si aucun test n'est encore écrit pour un module, le répertoire Test doit avoir la structure suivante :


    Test/
       Makefile
       info.xml.in (description du module de test)
       control/
          Makefile
          PU_suite_<Module>.php   (suite dédiée au module) -
                                   Il est possible d'avoir plusieurs suites si les
                                   tests sont très nombreux
          PU_test_<Module>_<description1>.php  test d'une fonctionnalité de la suite
          PU_test_<Module>_<description2>.php  test d'une fonctionnalité de la suite
       
       input/
          Makefile
          PU_data_<Module>_<Family1>.ods   // données d'entrées de tests 
                                             (csv/ods ou xml)
          PU_data_<Module>_<Family2>.csv
          PU_data_<Module>_<Users>.csv
          PU_data_<Module>_<Misc data>.xml
       reference/
          Makefile
          PU_reference_<Module>_<ref1>.xml  // données de références pouvant
                                             servir de comparaison
    
### Classe de test

Une suite de tests portant sur les documents est une classe dérivée de la classe `PHPUnit_Framework_TestDocument`.

     require_once 'PU_Framework_TestDocument.php';
    
     class TestSearch extends PHPUnit_Framework_TestDocument
     {
       
        /**
         * test basic search criteria
         * @dataProvider loginCriteria
         */
        public function testBasicSearch($criteria, $arg, $family)
        {
            require_once "FDL/Class.SearchDoc.php";
            $s = new SearchDoc($this->dbaccess, $family);
            $s->addFilter($criteria, $arg);
            $s->setObjectReturn(true);
            $s->search();
            
            $err = $s->getError();
            $this->assertEmpty( $err, sprintf("Search error %s %s", $criteria, $arg));
        
        }  
		
        public function loginCriteria()
        {
            return array(
                array(
                    "us_login ~* '%s'",
                    "Garfield",
                    "IUSER"
                ),
                array(
                    "us_mail='%s'",
                    "Léopol",
                    "IUSER"
                )
            );
        }
    }

Cette classe contient un ensemble de méthodes commençant par *`test`*. Chaque méthode commençant par `test` est considérée comme une méthode de test et est appelée lors du lancement de la campagne de test. 

Une méthode de test doit :

* importer les données de tests
* exécuter les méthodes à tester
* rendre compte des résultats

Les données de test sont déclarées par le commentaire `@dataProvider` qui fait référence à une méthode qui retourne les données de test.

<div class="remark"><span class="remark"> pas comprendre moi :p </span>Ces données peuvent faire référence à des fichiers d'importation contenant des familles ou des documents. Il est à la charge de la méthode de test de lancer l'importation des fichiers. </div>

Toutes les données insérées dans la base de données sont effacés après le passage d'un test. Chaque test travaille sur une base de données identique.

Les compte-rendus des résultats de test se font à l'aide des méthodes `assert*` de la classe `PHPUnit_Framework_Assert`.

### Ajouter un test à une suite existante

Les classes de tests sont enregistrées dans le répertoire test. Pour ajouter un test, il faut ajouter une méthode dans la classe de la suite de test correspondante. Cette méthode, comme toute méthode de test, doit commencer par `test`.

### Créer une nouvelle suite de tests

Afin de créer une nouvelle suite de test, il faut créer une nouvelle classe dans le répertoire `test`. Cette classe doit hériter de `FrameworkDcp`.

Il faut ensuite déclarer cette suite dans la classe `TestSuiteDocument`. Le nom du fichier est `PU_` suivi du nom de la classe. PU indique PhpUnit. La déclaration se fait en ajoutant l'appel à addTestSuite dans la méthode `Suite`.

     public static function suite() {
         $suite = new FrameworkDcp('Package');
  
         $suite->addTestSuite('TestDocument');
         $suite->addTestSuite('TestFolder');
         $suite->addTestSuite('TestSearch');
         //add next suite here
  
         return $suite;
     }

### Comment lancer un test ?

Les tests sont lancés à l'aide du programme phpUnit. Ce programme est disponible à partir de pear PHP. La version à utiliser est la version 3.5 ou supérieure.

Si vous venez de créer ou de modifier un test, il faut publier votre test sur votre contexte Dynacase de test. Ensuite vous vous connectez sur ce contexte et vous pouvez lancer l'ensemble des tests à l'aide la commande suivante.
   
     www-data@luke:~$ phpunit DCPTEST/PU_dcp.php  2>/dev/null 
     PHPUnit 3.5.7 by Sebastian Bergmann. 
       
     ............IIII.............................. 
      
     Time: 3 seconds, Memory: 19.00Mb 
       
     OK, but incomplete or skipped tests! 
     Tests: 46, Assertions: 111, Incomplete: 4. 

Il est aussi possible de ne lancer qu'une suite particulière :


     www-data@luke:~$ phpunit DCPTEST/PU_test_dcp_search.php 2> /dev/null 
     PHPUnit 3.5.7 by Sebastian Bergmann. 
     
     ................ 
     
     Time: 3 seconds, Memory: 15.25Mb 
     
     OK (16 tests, 37 assertions) 

Il est aussi possible de lancer les tests via l'application web. L'application `DCPTEST` contient une seule action qui lance l'ensemble des tests.

### Outillage

PhpCodeSniffer
:    <span class="fixme">à compléter</span>

phpBeautifier
:    <span class="fixme">à compléter</span>

phpUnit
:    <span class="fixme">à compléter</span> 

intégration eclipse
:    <span class="fixme">à compléter</span> 

## les TAI ou Tests Automatisés d'Interface 

<span class="fixme">à compléter</span>
