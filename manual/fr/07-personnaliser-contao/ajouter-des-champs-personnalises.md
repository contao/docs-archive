## Ajouter des champs personnalisés

Imaginons que vous souhaitiez ajouter un numéro de client à la table des 
membres. L'ajout d'un champ personnalisé à une table de Contao nécessite de 
modifier plus d'un fichier, il est donc préférable d'ajouter un module 
personnalisé dans le répertoire `system/modules`. Gardez en mémoire que les 
modules sont chargés en suivant l'ordre alphabétique, n'appelez donc pas votre 
extension `custom` si vous souhaitez redéfinir les configurations de 
l'extension `news`.


### Étendre le DCA (tableau conteneur de données)

Créez le fichier `dca/tl_member.php` dans le répertoire de votre module et 
ajoutez-y les métadonnées pour le nouveau champ, afin que Contao sache comment 
le gérer.

À partir de la version 3 de Contao, vous pouvez également spécifier directement 
les champs correspondants et leur configuration pour la base de données dans le 
tableau conteneur de données sous `sql`. Les détails SQL ne sont pas envoyés à 
la base de données, mais sont utilisés pour calculer la différence entre les 
spécifications de Contao et les tables existantes.

```php
// Modification de la palette
$GLOBALS['TL_DCA']['tl_member']['palettes']['default'] = str_replace
(
    'company',
    'customer_number,company',
    $GLOBALS['TL_DCA']['tl_member']['palettes']['default']
);

// Ajoute les métadonnées du champ
$GLOBALS['TL_DCA']['tl_member']['fields']['customer_number'] = array
(
    'label'     => &amp;$GLOBALS['TL_LANG']['tl_member']['customer_number'],
    'exclude'   => true,
    'inputType' => 'text',
    'eval'      => array('mandatory'=>true, 'rgxp'=>'digit', 'maxlength'=>8),
    'sql'       => "varchar(8) NOT NULL default ''"
);
```

Si vous ne comprenez pas le code ci-dessus, il peut être utile de relire le 
chapitre sur les [tableaux conteneurs de données][1].

Après l'ajout ou la modification d'un champ dans le tableau conteneur de 
données, vous devriez utiliser l'[outil d'installation de Contao][2] afin de 
mettre à jour les tables de votre base de données.


### Ajouter une traduction

Créez le fichier `languages/en/tl_member.php` dans le répertoire de votre 
module, et ajoutez-y les libellés anglais pour votre nouveau champ :

```php
$GLOBALS['TL_LANG']['tl_member']['customer_number'] = array
(
    'Customer number',
    'Please enter the 8-digit customer number.'
);
```

Dans le module membres, vous pouvez désormais saisir un numéro de client qui 
peut contenir jusqu'à 8 caractères numériques. Si le champ n'est pas saisi, ou 
contient un caractère non numérique, Contao refusera d'enregistrer la valeur 
et affichera un message d'erreur à la place. 


[1]: ../06-tableaux-conteneurs-de-donnees/README.md
[2]: ../01-installation/installer-contao.md#l-outil-d-installation-de-contao