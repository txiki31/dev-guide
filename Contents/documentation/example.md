# Conseil d'utilisation markdown


## Chapitrage

Les niveaux de chapitre suivant sont **utilisables**.  
L'indentation de structure est de 4 espaces sans tabulation.  
La syntaxe `# ## ###` doit être utilisée (bug sur les syntaxes `=======`).


# Premier niveau {#level1}
~~~
...
# Premier niveau qsqsdqsd  {#level1}
...
~~~

[Retour vers le premier niveau](#level1)

## Second niveau    {#level2}
~~~
...
## Second niveau  {#level2}
...
~~~

[Retour vers le second niveau](#level2)

### Troisieme niveau
~~~
...
### Troisième niveau
...
~~~

**Les niveaux de chapitre 4, 5 et 6 sont à proscrire pour améliorer la lisibilité des documents.**




## Insertion de code

Le code peut-être inséré `en ligne`, pour cela utiliser la syntaxe \`...texte...\`.  
~~~
Le code peut-être inséré `en ligne`, pour cela utiliser la syntaxe `...texte...`.  
~~~
**Cette notation est réservée au code : commande, nom de fichier, etc... et an aucun cas pour des mises en évidence.**



Les blocs de code sont déclarés en précisant le langage [cf.  GeSHi highlighting library](http://qbnz.com/highlighter/).

    [php]
    function connect(&$dsn, $persistent = false)
    {
        if (is_array($dsn)) {
            $dsninfo = &$dsn;
        } else {
            $dsninfo = DB::parseDSN($dsn);
    ...

…


    [code]
    [php]
    <?php
    function connect(&$dsn, $persistent = false)
    {
        if (is_array($dsn)) {
            $dsninfo = &$dsn;
        } else {
            $dsninfo = DB::parseDSN($dsn);
    ...	





## Les listes et autres énumération


Les simples énumérés :
                     
-   un premier item  
-   un second item  
                    
                    
-   un item avec bloc de texte 

    Avec un block de texte.  
	Et une autre ligne.  
	Avec encore une autre ligne
	
-   un nième item

    * une entrée de niveau 2
	- une entrée de niveau 2

        - une entrée de niveau 3
		* une entrée de niveau 3

<div class="fixme">il faut compléter ici</div>
<span class="fixme">il faut compléter ici aussi</span>

Voila les conventions de préfixe utilisés dans Dynacase :

set
:   stocke/enregistre la valeur fourni

get                     
:   retourne une unique valeur/élément

is / has
:   est si la condition est vrai 
    et retourne le résultat du test

check
:   vérifie que la condition est satisfaite et
    retourne une exception si ça n'est pas le cas

list
:   retourne une/liste de valeur élément

\*
:   éxecute l'opération demandée


### Les constantes

Les constantes doivent toujours être en majuscules. Les constantes true,
false et null font exception à la règle des majuscules, et doivent
toujours être en minuscules. Les define sont à proscrire, il est
recommandé d'utiliser des constantes de classe.

### Les variables globales

Les variables globales sont fortement déconseillées, lorsqu'elles sont
nécessaires, elles doivent être prefixées par \_ et en majuscule.

## Structures de contrôles

### Parenthèses

Les instructions de contrôle doivent avoir un espace entre le mot clé de
l'instruction et la parenthèse ouvrante, afin de les distinguer des
appels de fonctions.

    [php]
    <?php
    if ((condition1) || (condition2)) {
        action1;
    } elseif ((condition3) && (condition4)) {
        action2;
    } else {
        defaultaction;
    }
    ?>

    <?php
    switch (condition) {
    case 1:
        action1;
        break;
    case 2:
        action2;
        break;
    default:
        le job par defaut;
        break;
    }
    ?>

### Accolades

Il faut toujours utiliser des accolades, même dans les situations où
elles sont techniquement optionnelles. Leur présence augmente la
lisibilité du code et réduit le risque d'erreur logique lors de l'ajout
de nouvelles lignes de code.

### Opérateur ternaire

Les opérateurs ternaires ne devraient être utilisés que dans les
conditions suivantes:

-   un opérateur ternaire doit être écrit sur une seul ligne de code
-   on ne doit pas imbriquer les opérateurs ternaires
-   les opérateurs ternaires doivent donc être réservé à des tests
    simples et à l'initialisation des variables.

### Priorité des opérateurs

L'utilisation de la seule priorité des opérateurs est déconseillées, il
est recommandé d'utiliser des parenthèses pour augmenter la lisibilité
du code.

Par exemple : préférez `if (($x || $y) && ($z && (!$w)))` à `if ($x || $y && $z && !$w)`.


## Classes

### Saut de ligne

Les déclaration de classes ouvrent l'accolade sur une nouvelle ligne.

    [php]
    <?php
    class FooBar
    {

        //... et le code vient ici

    }
    ?>

### Visibilité

Toutes les fonctions et les membres d'une classe doivent indiquer leur
visibilité. Le mot clef var est donc proscrit. Les attributs de classe
doivent être définis soit en protected soit en private. L'accès en est
limité via des getteurs et des setteurs. L'utilisation des méthodes
magiques **set et**get est découragée.

### Définition

Les attributs de classe doivent être déclarés.

### Valeur par défaut

Toutes les variables de classe doivent être initialisé soit à une valeur
par default, soit à la valeur null.

## Fonctions

### Indentation et argument

La déclaration des fonctions respecte l'indentation du style "K&R".

    [php]
    <?php
    function connect(&$dsn, $persistent = false)
    {
        if (is_array($dsn)) {
            $dsninfo = &$dsn;
        } else {
            $dsninfo = DB::parseDSN($dsn);
        }

        if (!$dsninfo || !$dsninfo['phptype']) {
            return $this->raiseError();
        }

        return true;
    }
    ?>

### Ordre des arguments

Les arguments possédant des valeurs par défaut vont à la fin de la liste
des arguments.

### Appel de fonction

Les fonctions doivent être appelées sans espace entre le nom de la
fonction, la parenthèse ouvrante, et le premier paramètre ; avec un
espace entre la virgule et chaque paramètre et aucun espace entre le
dernier paramètre, la parenthèse fermante et le point virgule. Voici un
exemple : <?php
$var = foo($bar, $baz, $quux);
?>

Comme montré ci-dessus, il doit y avoir un espace de chaque côté du
signe égal utilisé pour affecter la valeur de retour de la fonction à
une variable.

### Typage des arguments

Les arguments dans les fonctions doivent être typés excepté pour les cas
où ce n'est pas possible (type de base array, string, int etc...).

### Retour de méthode

_Préfixe_                  
:   _Retour si l'éxécution est conforme_

set                      
:   l'objet courant ($this)

get                      
:   type d'élément indiqué dans le return

is / has                 
:   booléen

check                    
:   l'objet courant (`$this`) si l'assertion est validée

list                     
:   array

\*                       
:   l'objet courant (`$this`)

**Une méthode doit toujours retourner le même type de données** (pas de
méthode retournant une string et un array suivant que le résultat est
unique ou multiple par exemple).

### Retour d'erreur et exception

Une méthode doit retourner une exception si les contraintes sur les
paramètres d'entrée ne sont pas validées et que cela va entrainer un
dysfonctionnement.

    [php]
    /**
     * test for example
     *
     * @param int $x must be > 0 and be odd
     * @return float
     */
    public static function mySqrt($x) {
        if ($x < 0) {
            throw new dcp\Exception(sprintf("need to be positive : %d found",$x));
        }
        if ($x%2 == 0) {
            dcp\Context::setError(sprintf(_("need to be odd: %d found"),$x));
            return null;
        }
        return sqrt($x);
    }

Toute méthode ayant annoncé un type de retour non vide doit retourner
"null" si le résultat ne peut être retourné mais que cela ne provoque
pas de dysfonctionnement. De plus un message doit être indiqué (via la
méthode setError) pour expliquer pourquoi le retour n'a pu être fait.

La fonction appelante peut alors utiliser la méthode
getLastErrorMessage() si elle veut voir une éventuelle erreur.

    [php]
    $c=dcp\MyClass::mySqrt($x) ;
    if ($c === null) {
        $err=dcp\Context::getLastErrorMessage();
    }

## Documentation

### Généralités

Tous les fichiers de code source doivent contenir le bloc de
commentaires d'en-tête : Un bloc de commentaire "page-level" en début de
chaque fichier, et un bloc de commentaires "class-level" juste au dessus
de chaque classe.

### Bloc classe level

    [php]
    /**
     * Description courte de la classe
     *
     * Description plus détaillée de la classe (si besoin en est)...
     *
     * @brief NomCatégorie
     * @class NomPaquetage
     * @author Equipe de dev <dev@anakeen.com>
     **/

### Bloc function level

    [php]
    /**
     * Description courte de la fonction
     *
     * Description plus détaillée de la fonction (si besoin en est)...
     *
     * @param type $parameter Description.
     *
     * @return type Description Si la méthode ne retourne pas de valeur, il faut utiliser void comme type.
     * @throws \qualified\Class Description.
     **/

### Bloc var level

    [php]
    /**
     * Description courte de la variable de classe
     *
     * Description plus détaillée de la variable de classe (si besoin en est)...
     *
     * @var type Description.
     **/

### Variable type

Type de variables qui peuvent être utilisés dans des docBlock :

integer 
: Integer type variable (non-floating-point positive or
    negative number).
	
float
:   Float type (point number).

boolean 
:   Logical type (true or false).
   
string 
:   String type (any value in "" or ' ').
   
array 
:   Array type.
   
ClasseName 
:   Object type : il faut indiquer explicitement le type
    d'objet attendu.
   
resource :
:   Resource type (for example, the result of
    mysql\_connect()).
   
callback 
:   Used for anonymous functions, or objects that implement
    \_\_invoke(), or array style callbacks.
   
mixed 
:   Pseudo type with undefined (or multiple) types.
   
void 
:   Pseudo type (i.e. null, a function returns nothing)

### Balises

@brief 
:   correspond au package physique (webinst)
   
@class 
:   correspond à l'élément en cours de développement
    dynacasePlatformCore etc... (les noms sont indiqués sur le bug
    tracker)
   
@author 
:   Equipe de dev <dev@anakeen.com>

## Namespace

### Namespace
x
Le namespace doit être déclaré juste après le tag PHP d'ouverture.

    [php]
    <?php

    namespace dcp\util;

**Voir le découpage en namespace**

## Gestion des erreurs

### Niveau d'erreur

Le code doit être E\_STRICT compatible. Cela signifie qu'il ne doit pas
produire de warning ou d'erreur quand le niveau de rapport d'erreur de
php est au niveau E\_STRICT.
