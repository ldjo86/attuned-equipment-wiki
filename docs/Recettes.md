[Accueil du wiki](Home.md) · [Sommaire du dépôt](../README.md) · [Annexes](../ANNEXES.md)

<a name="page-recettes"></a>

# Recettes

Le datapack v0.17.1 ajoute **15 recettes** : six arcs, six arbalètes, deux boucliers façonnés et une amélioration de bouclier en netherite. Chaque recette produit un objet. Les objets gardent l’identifiant Minecraft de leur famille et reçoivent des composants personnalisés pour le matériau, la durabilité, l’aspect et l’histoire.

<a name="page-recettes-arcs--six-matériaux"></a>

## Arcs : six matériaux

Chaque arc demande **3 unités du matériau choisi et 3 ficelles**. Dans la grille, `M` représente le matériau et `F` une ficelle ; « — » représente une case vide.

| Colonne gauche | Colonne centrale | Colonne droite |
| --- | --- | --- |
| — | M | F |
| M | — | F |
| — | M | F |

| Objet | Matériau M | Durabilité maximale | Potentiel initial |
| --- | --- | --- | --- |
| Arc en cuivre | Lingot de cuivre | 512 | V |
| Arc en diamant | Diamant | 896 | III |
| Arc en or | Lingot d’or | 416 | II |
| Arc en fer | Lingot de fer | 640 | V |
| Arc en netherite | Lingot de netherite | 1152 | II |
| Arc en pierre | Pierres (cobblestone) | 448 | V |

<a name="page-recettes-arbalètes--six-matériaux"></a>

## Arbalètes : six matériaux

Chaque arbalète demande **3 unités du matériau choisi, 2 ficelles et 1 crochet**. `M` désigne le matériau, `F` la ficelle et `C` le crochet.

| Colonne gauche | Colonne centrale | Colonne droite |
| --- | --- | --- |
| M | — | M |
| F | C | F |
| — | M | — |

| Objet | Matériau M | Durabilité maximale | Potentiel initial |
| --- | --- | --- | --- |
| Arbalète en cuivre | Lingot de cuivre | 620 | V |
| Arbalète en diamant | Diamant | 1050 | III |
| Arbalète en or | Lingot d’or | 500 | II |
| Arbalète en fer | Lingot de fer | 760 | V |
| Arbalète en netherite | Lingot de netherite | 1350 | II |
| Arbalète en pierre | Pierres (cobblestone) | 540 | V |

Le « potentiel initial » est la limite enregistrée lors de la fabrication de l’objet. Il ne donne pas immédiatement ce niveau d’évolution. Un objet fabriqué directement en diamant ou en netherite a ici un potentiel initial plus réduit que les recettes de départ en pierre, cuivre ou fer.

<a name="page-recettes-bouclier-en-fer"></a>

## Bouclier en fer

Il demande **6 lingots de fer et 1 planche** de n’importe quel bois reconnu par `#minecraft:planks`. Sa durabilité est **600** et son potentiel initial va jusqu’à **IV**.

| Colonne gauche | Colonne centrale | Colonne droite |
| --- | --- | --- |
| Fer | Planche | Fer |
| Fer | Fer | Fer |
| — | Fer | — |

<a name="page-recettes-bouclier-en-diamant"></a>

## Bouclier en diamant

Il demande **6 diamants et 1 lingot de fer**. Sa durabilité est **850** et son potentiel initial va jusqu’à **III**. Le fichier enregistre explicitement une origine « diamant direct ». Le texte de l’objet invite à commencer par un bouclier en fer pour atteindre l’évolution IV.

| Colonne gauche | Colonne centrale | Colonne droite |
| --- | --- | --- |
| Diamant | Fer | Diamant |
| Diamant | Diamant | Diamant |
| — | Diamant | — |

<a name="page-recettes-amélioration-du-bouclier-en-netherite"></a>

## Amélioration du bouclier en netherite

À la table de forge, la recette associe :

| Emplacement | Ingrédient |
| --- | --- |
| Modèle | Modèle de forge d’amélioration en netherite |
| Base | Bouclier |
| Ajout | Lingot de netherite |

La recette applique au résultat l’apparence de bouclier en netherite, une durabilité maximale de **1150** et une rareté épique. Dans la base du pack, l’apparence passe par `custom_model_data: 10016` ; à partir de l’overlay 61, elle passe par `item_model: attuned:shield/netherite`. Son filtre de base accepte l’identifiant `minecraft:shield` ; il ne teste pas uniquement les boucliers en diamant. Les conditions d’origine et d’évolution du système de forge restent documentées dans la page consacrée aux boucliers : cette recette ne suffit pas, à elle seule, à définir leur potentiel d’histoire.

Source : `data/attuned/recipe/shield/netherite_upgrade.json`, ensemble du fichier. Les fonctions de synchronisation du bouclier traitent ensuite son matériau.

<a name="page-recettes-ce-que-couvre-ce-catalogue"></a>

## Ce que couvre ce catalogue

Les paliers d’histoire, les réparations et les changements de matériau commandés par les menus de forge sont des fonctions de jeu, distinctes de ces 15 recettes JSON. Leur absence du tableau ne signifie pas qu’ils sont absents du datapack.

Les overlays fournissent les mêmes 15 recettes, avec des composants adaptés aux versions. Les quantités, motifs, durabilités et potentiels ci-dessus sont conservés. Les boucliers reçoivent aussi des composants `repairable` et `enchantable` à partir de l’overlay 57 : fer réparable au lingot de fer, enchantabilité 14 ; diamant réparable au diamant, enchantabilité 12 ; netherite réparable au lingot de netherite, enchantabilité 10. Le [catalogue CSV](../catalogues/recettes.csv) donne les quantités, durabilités, potentiels et identifiants ; le [catalogue JSON](../catalogues/recettes.json) conserve la base et les six variantes d’overlay pour chacune.

Sources : `data/attuned/recipe/bow/*.json`, `data/attuned/recipe/crossbow/*.json`, `data/attuned/recipe/shield/*.json`, et leurs copies dans `overlay_57` à `overlay_94`. Les noms français proviennent du pack de ressources associé.
