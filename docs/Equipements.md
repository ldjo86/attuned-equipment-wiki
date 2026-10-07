[Accueil du wiki](Home.md) · [Sommaire du dépôt](../README.md) · [Annexes](../ANNEXES.md)

<a name="page-equipements"></a>

# Équipements

Attuned Equipment attache une histoire à chaque objet suivi : son utilisation, ses évolutions, ses bonus et ses exploits voyagent avec cet objet. Une épée nouvellement fabriquée ne récupère donc pas l'expérience d'une autre épée du même joueur.

Cette page décrit les données de l'archive **v0.17.1**. Les valeurs sont issues d'une analyse statique du datapack ; elles ne constituent pas un essai en jeu.

<a name="page-equipements-les-12-familles-suivies"></a>

## Les 12 familles suivies

| Famille | Comment commencer le suivi | Compteur principal |
| --- | --- | --- |
| Épée | Utiliser une épée reconnue en main principale, ou ouvrir une table de forge avec elle | Utilisations |
| Pioche | Utiliser une pioche reconnue en main principale, ou ouvrir une table de forge avec elle | Utilisations, minerais et roche |
| Hache | Utiliser une hache reconnue en main principale, ou ouvrir une table de forge avec elle | Utilisations, bûches et combats |
| Pelle | Utiliser une pelle reconnue en main principale, ou ouvrir une table de forge avec elle | Utilisations, terrain, sable et neige |
| Houe | Utiliser une houe reconnue en main principale, ou ouvrir une table de forge avec elle | Utilisations et cultures |
| Arc | Tirer avec l'arc en main principale ; les arcs Attuned fabriqués sont déjà suivis | Tirs et éliminations |
| Arbalète | Utiliser l'arbalète en main principale ; les arbalètes Attuned fabriquées sont déjà suivies | Utilisations de l'arbalète et éliminations |
| Bouclier | Fabriquer le bouclier Attuned ; pour un bouclier vanilla, l'initialisation est notamment disponible en ouvrant une table de forge avec lui en main principale | Blocages comptabilisés |
| Casque | Porter la pièce dans son emplacement d'armure | Expérience d'armure |
| Plastron | Porter la pièce dans son emplacement d'armure | Expérience d'armure |
| Jambières | Porter la pièce dans son emplacement d'armure | Expérience d'armure |
| Bottes | Porter la pièce dans son emplacement d'armure | Expérience d'armure |

Les armes et outils en bois, pierre, fer, diamant et netherite ont des initialisations explicites. Les outils et armes en cuivre natifs sont pris en charge par l'overlay destiné aux versions qui les possèdent. Dans les versions antérieures, l'étape cuivre de la reforge emploie un objet de base en fer. Les outils et épées en or n'ont pas les mêmes chemins d'initialisation et de progression : ne leur attribuez pas automatiquement les possibilités des arcs en or.

Le trident, la masse, la canne à pêche et d'autres objets peuvent apparaître dans les menus d'enchantement. Cela ne leur donne pas pour autant une histoire d'équipement à cinq évolutions : la station accepte seulement les douze types du tableau. Voir [Enchantements](Enchantements.md).

**Sources du ZIP :** `data/attuned/function/tick.mcfunction`, lignes 10–45 ; `function/history/use/*`, lignes 2–5 ; `function/history/bow_shot.mcfunction`, lignes 1–3 ; `function/forge/open.mcfunction`, lignes 4–32 ; `function/armor/scan.mcfunction`, lignes 2–14 ; `function/station/evaluate.mcfunction`, lignes 8–22. Les chemins `function/...` de cette page sont relatifs à `data/attuned/`.

<a name="page-equipements-arcs-et-arbalètes-par-matériau"></a>

## Arcs et arbalètes par matériau

Le matériau modifie notamment la durabilité. L'expérience et les enchantements apportent leurs propres effets : une durabilité plus élevée ne signifie pas, à elle seule, un multiplicateur de dégâts de projectile.

| Matériau | Ingrédient de matériau | Durabilité de l'arc | Durabilité de l'arbalète | Potentiel d'un exemplaire fabriqué directement |
| --- | --- | ---: | ---: | --- |
| Bois / objet vanilla initialisé | Recette vanilla | Valeur de base vanilla | Valeur de base vanilla | V |
| Pierre | Pierre `cobblestone` | 448 | 540 | V |
| Cuivre | Lingots de cuivre | 512 | 620 | V |
| Fer | Lingots de fer | 640 | 760 | V |
| Or | Lingots d'or | 416 | 500 | II |
| Diamant | Diamants | 896 | 1 050 | III |
| Netherite | Lingots de netherite | 1 152 | 1 350 | II |

Le « potentiel » est le plafond inscrit sur l'objet au départ. Un arc ayant commencé en fer, puis reforgé en diamant et en netherite, peut conserver un potentiel V. Un arc fabriqué directement en netherite commence avec un potentiel II. La progression n'est pas déterminée uniquement par le matériau visible.

<a name="page-equipements-recette-des-six-arcs-attuned"></a>

### Recette des six arcs Attuned

Chaque arc demande **3 unités du matériau et 3 ficelles**. `M` désigne le matériau du tableau et `F` une ficelle.

| Ligne de l'établi | Colonne 1 | Colonne 2 | Colonne 3 |
| --- | --- | --- | --- |
| Haut | Vide | M | F |
| Milieu | M | Vide | F |
| Bas | Vide | M | F |

<a name="page-equipements-recette-des-six-arbalètes-attuned"></a>

### Recette des six arbalètes Attuned

Chaque arbalète demande **3 unités du matériau, 2 ficelles et 1 crochet**.

| Ligne de l'établi | Colonne 1 | Colonne 2 | Colonne 3 |
| --- | --- | --- | --- |
| Haut | M | Vide | M |
| Milieu | Ficelle | Crochet | Ficelle |
| Bas | Vide | M | Vide |

Ces recettes créent un nouvel objet avec un historique vierge. Pour conserver un exemplaire existant, suivre [Forge](Forge.md).

**Sources du ZIP :** `data/attuned/recipe/bow/*.json` et `recipe/crossbow/*.json`, champs `pattern`, `key`, `result.components.minecraft:max_damage` et `result.components.minecraft:custom_data.attuned` ; `item_modifier/init/base_bow.json` et `init/base_crossbow.json`.

<a name="page-equipements-armures-et-potentiel-dorigine"></a>

## Armures et potentiel d'origine

| Matériau initial de l'armure | Potentiel enregistré |
| --- | --- |
| Cuir, mailles, or | II |
| Carapace de tortue | II |
| Cuivre, dans les versions concernées | V |
| Fer | V |
| Diamant | III |
| Netherite | II |

Ces plafonds ne garantissent pas que toutes les transitions de matériau soient actuellement accessibles dans l'interface. La reforge des armures comporte une limitation dans cette archive ; lire [Armures et boucliers](Armures-et-boucliers.md) et [Forge](Forge.md) avant de dépenser des matériaux.

**Sources du ZIP :** `data/attuned/item_modifier/init/armor/{leather,chainmail,golden,turtle,copper,iron,diamond,netherite}.json`, lignes 1–4.

<a name="page-equipements-épique-légendaire-et-conservation"></a>

## Épique, légendaire et conservation

La validation d'une évolution à la station ajoute une maîtrise et une ligne d'évolution. Les évolutions utilisent la rareté Minecraft `epic`. « Légendaire » est également un titre et un texte de présentation pour le dernier palier : ce n'est pas une cinquième valeur de rareté ajoutée au moteur du jeu.

Les bonus d'histoire sont appliqués directement à l'objet. Une reforge de matériau copie ses composants avant de changer son identité ou ses composants de matériau ; son histoire et son potentiel peuvent donc suivre l'objet. Certains chemins remplacent cependant son nom personnalisé. Il ne faut pas promettre une conservation absolue du nom choisi par le joueur ni une réparation gratuite lors de chaque reforge.

**Sources du ZIP :** `data/attuned/item_modifier/station/evolve/sword_1.json`, lignes 1–31 ; `station/evolve/sword_5.json`, lignes 1–31 ; `station/evolve/shield_4.json`, lignes 1–31 ; `function/forge/equipment/sword_wood_to_stone.mcfunction`, lignes 1–7 ; `item_modifier/evolution/sword_stone.json`, lignes 7–12.

<a name="page-equipements-pour-continuer"></a>

## Pour continuer

- [Progression et histoire](Progression-et-histoire.md) explique les seuils, la familiarité et la différence entre expérience et évolution.
- [Enclume](Enclume.md) explique comment payer et récupérer chaque palier.
- [Forge](Forge.md) donne les coûts de changement de matériau.
- [Armures et boucliers](Armures-et-boucliers.md) détaille les progressions défensives.
- [Hauts faits](Hauts-faits.md) décrit les récompenses liées aux combats et aux métiers.
