## Utilisateurs et groupes d'utilisateurs

Contao fait une distinction entre les utilisateurs du back office 
("utilisateurs"), qui peuvent se connecter au panneau d'administration, et les 
utilisateurs front office ("membres"), qui peuvent se connecter au site 
internet. Contrairement aux administrateurs, qui ont accès à toutes les pages 
et à tous les éléments par défaut ("allow all"), les utilisateurs ne peuvent 
pas accéder à une ressource qui n'a pas été explicitement autorisée dans leur 
profil ou dans le profil de l'un des groupes d'utilisateurs auxquels ils 
appartiennent ("deny all").


### Utilisateurs

Chaque utilisateur peut être associé à plusieurs groupes d'utilisateurs et 
hérite automatiquement de leurs autorisations. Toutes les autorisations sont 
cumulatives, ce qui signifie que l'utilisateur hérite de la somme des 
permissions de tous les groupes auxquels il appartient. Si le groupe A accorde 
un certain droit, vous ne pouvez pas la révoquer dans le groupe B.


#### Pages autorisées

L'option "Pages autorisées" permet de définir quelles pages de la structure de 
site, l'utilisateur est autorisé à voir. La capture d'écran ci-dessous montre 
la structure de site telle qu'elle est perçue par Helen Lewis. Bien que le site 
internet contient beaucoup plus de pages, elle ne peut en voir que trois, parce 
que seul l'accès à la page "Courses" a été autorisé dans les paramètres du 
groupe "Editors". Notez que même si Helen Lewis est autorisée à voir trois 
pages, elle ne peut modifier que l'une d'elles !

![](images/site-structure-hlewis-fr.jpg?raw=true)

Être capable de voir une page n'inclut pas le droit de la modifier (ou de 
modifier ses articles). Rappelez-vous que [les permissions d'une page][1] sont 
définies dans la structure de site, donc pour permettre l'accès à une page à un 
utilisateur, vous devez la sélectionner dans son profil et accorder son accès 
dans la structure de site.


#### Répertoires autorisés

Semblable à l'option "Pages autorisées", l'option "Répertoires autorisés" définie 
quels répertoires un utilisateur est autorisé à voir. La capture d'écran 
ci-dessous montre le gestionnaire de fichiers tel qu'il est perçu par Helen Lewis. 
Elle n'est autorisée de voir que le répertoire "campus", alors que les 
administrateurs peuvent voir le répertoire complet des fichiers (`files`).

![](images/gestionnaire-fichiers-hlewis.jpg?raw=true)


#### Champs autorisés

Comme mentionné au début, les utilisateurs n'ont pas du tout de permissions par 
défaut ("deny all"), ce qui implique aussi qu'ils ne peuvent pas accéder aux 
champs d'un formulaire. Même s'ils sont par exemple autorisés à accéder au 
module d'actualités, le formulaire pour créer une nouvelle entrée sera vide 
jusqu'à ce que l'administrateur sélectionne un ou plusieurs champs de la table 
`tl_news` dans les paramètres du groupe.

![](images/champs-autorises.jpg?raw=true)


### Membres

La gestion des membres (utilisateurs front office) est beaucoup plus facile à
gérer que celle des utilisateurs back office, car il n'y a pas de pages ou de
champs à autoriser. La gestion des membres est principalement requise pour
contrôler l'accès aux pages protégées, qui est mis en œuvre au niveau du groupe.
En fonction de la configuration du site internet, les membres inscrits pourront 
voir des pages protégées ou accéder à des téléchargements protégés qui ne sont 
pas disponibles pour les invités.


[1]: ../03-gestion-des-pages/modules.md#controle-d-acces