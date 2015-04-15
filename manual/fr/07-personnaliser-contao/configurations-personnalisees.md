## Configurations personnalisées

La configuration de Contao est définie dans un grand tableau divisé en trois 
sections : la configuration du système, la configuration du conteneur de données 
et la configuration de la langue. Le tableau de configuration est construit au 
moment de l'exécution et ne contient que les parties nécessaires à la génération 
d'une page donnée. Contao ne perd pas de temps et de mémoire à "parser" de 
nombreux fichiers de configurations redondants. 


### Personnaliser la configuration du système

La configuration du système est enregistrée dans les fichiers `config.php` des 
différents modules de Contao. Si vous voulez la personnaliser, ajoutez vos 
modifications dans le fichier `system/config/localconfig.php`, afin qu'elles ne 
soient pas écrasées à la prochaine mise à jour. La plupart des paramètres 
peuvent être configurés dans le module Configuration du back office et seront 
écrits automatiquement dans le fichier de configuration; vous aurez donc 
rarement besoin de le modifier manuellement. 


``` {.php}
// Désactive le créateur d'extension
unset($GLOBALS['BE_MOD']['devtools']['extension']);

### INSTALL SCRIPT START ###
$GLOBALS['TL_CONFIG']['debugMode'] = false;
$GLOBALS['TL_CONFIG']['displayErrors'] = false;
```

Pensez à mettre vos modifications au-dessus de la ligne `INSTALL SCRIPT START`; 
À défaut, elles seront supprimées par le module de configuration. Et 
**n'utilisez jamais le fichier `config.php` pour stocker des paramètres de 
configuration**, car ce fichier peut être écrasé lors des mises à jour ! 


### Personnaliser la configuration du conteneur de données

Contao utilise le [tableau conteneur de données (DCA)][1] pour stocker les 
métadonnées relatives aux tables. La configuration du conteneur de données 
est enregistrée dans les dossiers `dca` des divers modules de Contao. Faites vos 
modifications dans le fichier `system/config/dcaconfig.php` afin qu'elles ne 
soient pas écrasées à la prochaine mise à jour. 

``` {.php}
// Rend obligatoire le champ company dans la table des membres
$GLOBALS['TL_DCA']['tl_member']['fields']['company']['eval']['mandatory'] =
true;

// Vérifie que les noms de company ne comprennent que des caractères 
alphanumériques
$GLOBALS['TL_DCA']['tl_member']['fields']['company']['eval']['rgxp'] = 'alnum';

// N'autorise que les administrateurs à utiliser les éléments de contenu de 
type "includes"
if (!BackendUser::getInstance()->isAdmin)
{
    unset($GLOBALS['TL_CTE']['includes']);
}
```

Comme vous pouvez le voir, le fichier `dcaconfig.php` est un bon endroit pour 
enregistrer de petites modifications concernant la configuration de Contao. Pour 
faire de nombreux changements, pensez plutôt à les inclure dans une extension 
personnalisée, afin de ne pas en perdre la trace.


### Personnaliser les libellés et les traductions

Les libellés et les traductions sont enregistrés dans les dossiers `languages` 
des différents modules de Contao. Chaque langue est identifiée par son [code 
ISO-639-1][2]. Appliquez vos modifications dans le fichier 
`system/config/langconfig.php` afin qu'elles ne soient pas écrasées à la 
prochaine mise à jour. 

``` {.php}
// Modifie un libellé pour toutes les langues
$GLOBALS['TL_LANG']['MSC']['goBack'] = '«';

// Modifie un libellé pour une seule langue
if ($GLOBALS['TL_LANGUAGE'] == 'de')
{
    $GLOBALS['TL_LANG']['tl_layout']['column'] = 'Bereich';
}
elseif ($GLOBALS['TL_LANGUAGE'] == 'fr')
{
    $GLOBALS['TL_LANG']['tl_layout']['column'] = 'Section';
}
```

Bien entendu, les modifications du tableau de langues peuvent aussi être 
incluses dans un module personnalisé, ce qui est recommandé lorsqu'il y en 
a beaucoup. 


[1]: 06-Data-Container-Arrays.md
[2]: http://fr.wikipedia.org/wiki/Liste_des_codes_ISO_639-1