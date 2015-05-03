## Personnaliser l'éditeur de texte riche (TinyMCE)

Cette page explique comment personnaliser TinyMCE et sauvegarder les 
modifications afin qu'elles ne soient pas écrasées par la prochaine mise à 
jour de Contao. Notez que, par défaut, Contao n'inclut pas tous les plugins 
de TinyMCE; si vous souhaitez utiliser un plugin particulier qui ne fait pas 
partie de la distribution de Contao, il vous faut donc le télécharger à partir 
du [site du projet TinyMCE][1], et le mettre dans le répertoire 
`assets/tinymce/plugins`. 

![](images/rich-text-editor.jpg)

L'image ci-dessus montre le fichier de configuration de l'éditeur de texte 
riche `system/config/tinyMCE.php`. Pour créer un fichier de configuration 
personnalisé, copiez simplement ce fichier et renommez-le, par exemple en 
`tinyCustom.php`. Faites ensuite vos modifications et sauvegardez le nouveau 
fichier. Il reste encore à adapter la [configuration du conteneur de données][2] 
dans le fichier `system/config/dcaconfig.php` et indiquer à Contao à quels 
champs le fichier personnalisé de configuration s'applique. 

```php
// Utilisation d'une configuration personnalisée de l'éditeur de texte riche 
pour les éléments textes
$GLOBALS['TL_DCA']['tl_content']['fields']['text']['eval']['rte'] =
'tinyCustom';
```


[1]: http://tinymce.moxiecode.com
[2]: ../07-personnaliser-contao/configurations-personnalisees.md#personnaliser-la-configuration-du-conteneur-de-donn%C3%A9es
