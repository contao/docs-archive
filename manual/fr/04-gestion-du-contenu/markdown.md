## Markdown

Markdown est un langage de balisage léger qui vous permet de formater du texte
avec une syntaxe simple. Il a l'avantage d'être facile à lire et à écrire et il
peut être automatiquement converti au format HTML.

Vous trouverez quelques exemples de cette syntaxe ci-dessous :

### Syntaxe

#### Paragraphes

Les paragraphes sont séparés par des sauts de ligne :

    Premier paragraphe

    Second paragraphe 


#### Titres

Il existe six niveaux de titres :

    # Titre 1
    ## Titre 2
    ### Titre 3
    #### Titre 4
    ##### Titre 5
    ###### Titre 6


#### Strong

Pour donner de l'importance à un texte :

    **strong**
    __strong__

Il sera converti en HTML avec le code suivant : `<strong>strong</strong>`


#### Emphase

Pour marquer un texte sur lequel on veut insister :

    *emphasize*
    _emphasize_

Il sera converti en HTML avec le code suivant : `<em>emphasize</em>`


#### Code

Pour marquer un morceau de code informatique :

    `monospaced font`

Il sera converti en HTML avec le code suivant : `<code>monospaced font</code>`


##### Bloc de code

Pour un bloc de code, ajoutez quatre espaces devant chaque ligne.

        monospaced font ...
        ... sur plusieurs lignes


#### Bloc de citation

Les blocs de citation peuvent être créés avec un chevron droit placé au début
de la ligne.

    > Ceci est un bloc de citation.


#### Sauts de ligne

Ajouter deux ou plusieurs espaces à la fin d'une ligne :

    Contao est un système de gestion de contenu  
    Open Source accessibles.


#### Liens

Il y a deux syntaxes pour les liens : **incorporé** et **par référence**.

Un lien incorporé est structuré comme suit :

    [Contao](https://contao.org/en)

ou avec un titre optionnel :

    [Contao](https://contao.org/en "Site officiel de Contao")

Un lien par référence est structuré comme suit :

    [Site officiel de Contao][1]
    
    [1]:https://contao.org/en

La référence peut être ajoutée n'importe où dans le document.


#### Images

Il y a également deux syntaxes pour les images comme pour les liens.

Une image incorporée est structurée comme suit :

    ![Alt texte](/chemin/vers/img.jpg "Titre facultatif")

Une image par référence est structurée comme suit :

    ![Alt texte][id]

    [id]: /chemin/vers/img.jpg "Titre facultatif"

La référence peut être ajoutée n'importe où dans le document.


#### Listes

##### Listes non ordonnées

Les listes non ordonnées utilisent des astérisques ou des traits d'union :

    * Élément de liste  
    * Élément de liste  
        * Un élément de liste imbriqué
        * Un élément de liste imbriqué
    * Élément de liste

    - Élément de liste  
    - Élément de liste  
    - Élément de liste


##### Listes ordonnées

Les listes ordonnées utilisent des numéros :

    1. Élément de liste  
    2. Élément de liste  
    3. Élément de liste


### Syntaxe étendue

Il n'est pas possible de décrire tous les éléments avec Markdown tels que des
tableaux ou des notes de bas de page par exemple. C'est pourquoi, il existe
un projet appelé "Markdown Extra" qui complète le langage de base.

Vous trouverez quelques exemples de cette syntaxe étendue ci-dessous :


#### Tableaux

Un tableau peut être créé comme ceci :

```
Premier en-tête       | Deuxième en-tête      | Troisième en-tête  
--------------------- | --------------------- | ---------------------  
Contenu de la cellule | Contenu de la cellule | Contenu de la cellule  
Contenu de la cellule | Contenu de la cellule | Contenu de la cellule  
```

Vous pouvez créer des alignements en ajoutant des deux-points :

```
Premier en-tête | Deuxième en-tête | Troisième en-tête  
:-------------- | :--------------: | ----------------:  
Gauche          | Centrer          | Droite  
Gauche          | Centrer          | Droite  
```


#### Notes de bas de page

Les notes de bas de page peuvent être créées comme ceci :

    Voici du texte avec une note de bas de page.[^1]

    [^1]: Et voilà la note de bas de page.

La référence de la note de bas de page peut être ajoutée n'importe où
dans le document.


### Compléments d'information

Pour une documentation complète concernant Markdown, veuillez s'il vous
plaît, vous référer au site officiel en suivant ce [lien][1] (en Anglais).

Pour une documentation complète concernant Markdown Extra, veuillez s'il
vous plaît, vous référer au site officiel en suivant ce [lien][2].


[1]: http://daringfireball.net/projects/markdown/syntax
[2]: https://michelf.ca/projets/php-markdown/extra/
