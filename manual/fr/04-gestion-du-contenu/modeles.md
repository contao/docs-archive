## Modèles

Un modèle est principalement composé de codes HTML et PHP. Il est utilisé pour 
structurer une partie du contenu d'un module ou d'un élément de contenu, etc.
Par exemple, le modèle `news_full.html5` affiche le contenu complet d'une
actualité alors que le modèle `news_short.html5` affiche seulement une partie
de ce contenu.

Les modèles se trouvent dans leurs propres modules. Par exemple,
`news_full.html5` se trouve sous `system/modules/news/templates/news`.

Si vous modifiez ce fichier directement dans ce dossier, il sera remplacé la
prochaine fois que vous mettrez à jour Contao et **vous perdrez** toutes vos
modifications. Pour éviter cela, Contao vous permet de modifier les modèles
directement à partir du back office. Dans ce cas, le fichier est dupliqué et vos
modifications seront conservées lors de chaque mise à jour.

![](images/modeles.jpg?raw=true)

Créez un nouveau dossier et ajoutez-y un ou plusieurs modèles que vous souhaitez
modifier. Par la suite, n'oubliez pas de joindre le dossier au thème comme
expliqué dans le paragraphe [Composants d'un thème][8].

Un modèle peut être une partie de la structure d'un module, d'un élément de
contenu, d'un formulaire, etc. et c'est pourquoi ils sont préfixés. Ils peuvent
être facilement groupés, classés et reconnus. Par exemple : le préfixe `j_`
signifie "jQuery" et `nl_` signifie "newsletter".


[8]: 03-gestion-des-pages/themes.md#composants-dun-th%C3%A8me