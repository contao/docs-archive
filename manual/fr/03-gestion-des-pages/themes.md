## Thèmes

Bien que le gestionnaire de thèmes est une nouvelle fonctionnalité de la version 
2.9, il est en fait juste une interface améliorée pour quelque chose qui faisait 
déjà partie de Contao. Une design de site internet se compose généralement de 
feuilles de style, de modules front office, de présentations de page, de 
fichiers et de modèles que vous pouvez gérer dans le back office de Contao. Le 
gestionnaire de thème ne change pas cette approche du tout, il ajoute juste une 
option pour exporter et importer ces ressources.


### Thèmes par opposition aux modèles du front office

La principale différence entre les [thèmes][1] et les modèles du front office 
est qu'un modèle du front office contient un exemple de site internet 
entièrement préconfiguré, y compris un exemple de structure de site, d'articles, 
d'éléments de contenu et même d'utilisateurs et de groupes d'utilisateurs. Un 
thème, en revanche, ne contient que le design du site internet et peut donc être 
importé sans risque de perdre toutes les données existantes.

![](images/gestionnaire-theme.jpg?raw=true)


### Composants d'un thème

Un thème est un groupe de [feuilles de style][2], de [modules front office][3] 
et de [présentations de page][4], qui sont tous stockés dans la base de données 
et automatiquement reconnus par l'exportateur de thème. Vous en apprendrez plus 
sur ces éléments dans les chapitres suivants. Un thème inclut habituellement des 
images et d'autres fichiers à partir du répertoire des fichiers et des modèles 
personnalisés en option à partir du répertoire des modèles. Toutefois, ces 
ressources ne sont pas automatiquement liées avec le thème et doivent donc être 
ajoutées dans la configuration du thème pour y être inclues dans l'exportation.

![](images/parametres-theme.jpg?raw=true)


### Exportation et importation d'un thème

Pour exporter un thème, cliquez simplement sur le bouton d'exportation et 
télécharger le fichier .cto en local sur votre ordinateur. Bien que .cto est une 
extension de fichier propriétaire pour les thèmes de Contao, le fichier est en 
fait une archive ZIP qui peut être extraite avec chaque programme qui traite les 
fichiers .zip. Pour réimporter un thème, téléversez le fichier .cto dans votre 
installation de Contao, ouvrez le gestionnaire de thèmes et cliquez sur "Import 
de thème". Vous pouvez importer plusieurs thèmes à la fois. Une fois 
l'importation terminée, vous pouvez associer une ou plusieurs présentations de 
page du nouveau thème dans la structure de site.


[1]: https://contao.org/en/contao-themes-and-templates.html
[2]: ../03-gestion-des-pages/feuilles-de-style.md#feuilles-de-style
[3]: ../03-gestion-des-pages/modules.md#modules
[4]: ../03-gestion-des-pages/presentations-de-page.md#pr%C3%A9sentations-de-page