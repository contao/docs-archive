## Présentations de page

Les présentations de page déterminent l'agencement basique d'une page, par ex.
le nombre de colonnes ou la largeur générale, et elle définissent quels modules
de front office vont être affichés dans quelles colonnes. Elles permettent aussi
d'inclure des feuilles de style, de lier la page à un flux RSS ou Atom,
d'associer un ID Google Analytics et d'ajouter du code JavaScript qui pourrait
être requis pour contrôler des éléments interactifs ou des plugins. Le framework
CSS de Contao divise automatiquement la fenêtre du navigateur en plusieurs
sections et affiche les modules qui ont été assignés à ces sections les uns à
la suite des autres.

![](images/front-end-structure.jpg)

![](images/modules-front-office.jpg)

Cela implique que lorsque vous allez créer une présentation de page, vous devriez
déjà avoir créé toutes les feuilles de style et les modules front office que vous
voulez inclure. C'est pourquoi, il est recommandé de créer les ressources dans
l'ordre suivant :

* Créer les modules front office nécessaires
* Créer les feuilles de style nécessaires
* Optionnellement, créer des archives d'actualités ou des calendriers
* Créer une présentation de page et combiner tous les composants
