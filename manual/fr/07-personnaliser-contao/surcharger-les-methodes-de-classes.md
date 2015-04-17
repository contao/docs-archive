## Surcharger les méthodes de classes

Imaginons que vous vouliez modifier le comportement du module de navigation pour 
qu'il soit toujours visible, même en l'absence de sous-pages, alors que le 
module ne serait normalement pas affiché. Dans ce cas, une note doit informer 
l'utilisateur qu'il n'y a pas de sous-pages. Bien entendu, nous allons faire en 
sorte de conserver au maximum la classe originale de navigation, afin que les 
futures mises à jour ne nécessitent pas de maintenance. Les classes de modules 
et d'éléments de contenu peuvent être assignées dynamiquement dans la 
configuration du système de Contao, ce qui vous permet de les remplacer 
facilement par vos propres versions. 


### Créer une classe personnalisée

Le comportement de la classe de navigation par défaut correspond assez bien à ce 
que nous voulons, sauf que la méthode `generate()` cache le module lorsqu'il n'y 
a pas de sous-pages. Il suffit donc de modifier cette méthode particulière, et 
la meilleure façon de le faire est d'étendre la classe originale en la 
supplantant. Pour ce faire, créez un nouveau fichier 
`xcustom/ModuleMyNavigation.php` et définissez la classe personnalisée 
`ModuleMyNavigation` :

``` {.php}
// xcustom/ModuleMyNavigation.php
class ModuleMyNavigation extends ModuleNavigation
{
    public function generate()
    {
        // Exécute la méthode originale
        $buffer = parent::generate();

        if (empty($buffer))
        {
            $buffer = 'There are no subpages';
        }

        return $buffer;
    }
}
```


### Enregistrer une classe personnalisée

Les classes de modules et d'éléments de contenu peuvent être assignées 
dynamiquement dans la configuration du système de Contao, ce qui vous permet de 
les remplacer facilement par vos propres versions. Les noms des classes de 
modules sont enregistrés dans le tableau global `FE_MOD`. 

``` {.php}
// xcustom/config/config.php
$GLOBALS['FE_MOD']['navigationMenu']['navigation'] = 'ModuleMyNavigation';
```

Grâce à la configuration dynamique, Contao charge automatiquement la nouvelle 
classe à la requête suivante, et le module de navigation affichera le message 
"There are no subpages" au lieu de ne rien afficher du tout. La modification 
supporte les mises à jour sans nécessiter de maintenance. 
