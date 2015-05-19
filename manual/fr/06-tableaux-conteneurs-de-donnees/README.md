# Tableaux conteneurs de données

Les tableaux conteneurs de données ("Data Container Arrays" en Anglais, ou DCA)
sont utilisés pour stocker les métadonnées des tables. Chaque DCA décrit
une table particulière du point de vue de sa configuration, de ses relations
avec les autres tables et de ses champs. Le noyau de Contao détermine grâce à
ces métadonnées comment lister les enregistrements, comment générer les
formulaires dans le back office et comment sauvegarder les données. Les fichiers
DCA de tous les modules actifs sont chargés les uns après les autres (en
commençant par "backend", puis "frontend" et ensuite dans l'ordre alphabétique)
afin que chaque module puisse surcharger la configuration existante. Le fichier
`system/config/dcaconfig.php` est inclus à la fin.
