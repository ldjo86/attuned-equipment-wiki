[Accueil du wiki](Home.md) · [Sommaire du dépôt](../README.md) · [Annexes](../ANNEXES.md)

<a name="page-reliques-et-butin"></a>

# Reliques et butin

Attuned Equipment ajoute deux formes de découverte : **10 reliques nommées**, chacune accompagnée d’un récit, et des **livres ou tomes supplémentaires** attribués par des événements de génération de butin. Ces deux systèmes ont des tirages distincts.

<a name="page-reliques-et-butin-où-trouver-les-reliques-"></a>

## Où trouver les reliques ?

Les pourcentages ci-dessous s’appliquent à un tirage de la table de butin du coffre concerné, pas à l’ensemble d’une structure. Les pools de reliques effectuent au plus un tirage et leurs entrées ont le même poids.

| Table de coffre | Chance d’une relique | Répartition |
| --- | --- | --- |
| Ancienne cité | 25 % | Deux reliques : 12,5 % chacune |
| Trésor de bastion | 25 % | Le Serment des Cendres : 25 % |
| Pyramide du désert | 15 % | Le Soleil Enseveli : 15 % |
| Cité de l’End | 35 % | Six reliques : 35 % / 6, soit environ 5,833 % chacune |

Le pack remplace réellement **quatre tables de coffres Minecraft** : `ancient_city`, `bastion_treasure`, `desert_pyramid`, `end_city_treasure`. Il conserve une liste de butin dans chacune et y ajoute un pool de reliques. Un autre datapack qui remplace les mêmes tables peut entrer en conflit ; ces remplacements ne sont pas une injection universelle à fusion automatique.

<a name="page-reliques-et-butin-les-dix-reliques"></a>

### Les dix reliques

| Relique | Objet de base | Coffre | Chance individuelle | Enchantements initiaux |
| --- | --- | --- | --- | --- |
| L'Ancre des Étoiles | Pioche en diamant | Cité de l’End | 5,833 % | `minecraft:efficiency` III, `minecraft:unbreaking` II |
| Le Serment des Cendres | Hache en or | Trésor de bastion | 25 % | `minecraft:sharpness` III, `minecraft:unbreaking` III |
| La Moisson des Échos | Houe en diamant | Ancienne cité | 12,5 % | `minecraft:efficiency` III, `minecraft:unbreaking` II |
| Les Pas du Retour | Bottes en diamant | Cité de l’End | 5,833 % | `minecraft:feather_falling` IV, `minecraft:protection` II |
| Le Dernier Pont | Épée en diamant | Cité de l’End | 5,833 % | `minecraft:sharpness` III, `minecraft:unbreaking` II |
| La Veille Silencieuse | Plastron en diamant | Cité de l’End | 5,833 % | `minecraft:protection` III, `minecraft:unbreaking` II |
| Heaume de la Cartographe | Casque en diamant | Cité de l’End | 5,833 % | `minecraft:protection` III, `minecraft:respiration` II |
| Le Soleil Enseveli | Pelle en fer | Pyramide du désert | 15 % | `minecraft:efficiency` II, `minecraft:unbreaking` II |
| Le Vœu du Silence | Bottes en diamant | Ancienne cité | 12,5 % | `minecraft:feather_falling` III, `minecraft:protection` II |
| Grèves du Pèlerin du Vide | Jambières en diamant | Cité de l’End | 5,833 % | `minecraft:protection` III, `minecraft:unbreaking` II |

<a name="page-reliques-et-butin-lhistoire-héritée"></a>

## L’histoire héritée

**Neuf reliques commencent avec un historique Attuned déjà rempli à 100**. Pour les armes et outils, il s’agit de 100 utilisations ; pour les armures, de 100 points d’XP d’armure. Ce bonus appartient à l’objet : il n’ajoute pas 100 points d’expérience Minecraft au joueur.

Toutes ces reliques suivies commencent à l’évolution 0. Le plafond initial est III pour les huit objets en diamant, et V pour Le Soleil Enseveli en fer. Les critères d’histoire et la forge restent nécessaires pour appliquer les évolutions.

| Relique suivie | Historique de départ ajouté |
| --- | --- |
| L’Ancre des Étoiles | 100 utilisations, 80 pierres, 20 minerais |
| La Moisson des Échos | 100 utilisations |
| Le Dernier Pont | 100 utilisations |
| Le Soleil Enseveli | 100 utilisations |
| Les Pas du Retour | 100 XP, 80 segments de marche, 12 chutes comptées |
| La Veille Silencieuse | 100 XP, 80 coups reçus, 30 coups de projectile |
| Heaume de la Cartographe | 100 XP, 60 coups reçus, 25 coups de projectile |
| Le Vœu du Silence | 100 XP, 100 segments accroupis |
| Grèves du Pèlerin du Vide | 100 XP, 100 segments de marche, 30 segments de sprint |

**Le Serment des Cendres est l’exception volontaire.** Cette hache en or porte son nom, son récit et ses enchantements, mais ne reçoit ni le suivi d’histoire artificiel, ni les 100 unités héritées. Cette différence est également annoncée dans `INSTALLATION_v0.17.1.txt`.

Les données sont fusionnées dans plusieurs étapes `set_custom_data` : il faut lire toutes les fonctions de la table, dans l’ordre. Par exemple, `relics/anchor_of_stars.json`, lignes 11–17, initialise d’abord le suivi puis y ajoute les 100 utilisations et les compteurs de minage.

<a name="page-reliques-et-butin-récits-des-reliques"></a>

## Récits des reliques

<a name="page-reliques-et-butin-lancre-des-étoiles"></a>

### L'Ancre des Étoiles

> Les bâtisseurs creusaient pour ancrer leur cité.<br> Sous la pierre pâle, ils ne trouvèrent que le vide.<br> Le maître posa sa pioche : « Alors, nous flotterons. »<br> La première tour tient toujours.

<a name="page-reliques-et-butin-le-serment-des-cendres"></a>

### Le Serment des Cendres

> Le gardien jura de ne jamais abandonner le trésor.<br> Quand les remparts brûlèrent, il ouvrit les portes.<br> Son clan valait plus que tout l'or du bastion.<br> La hache resta pour témoigner de son choix.

<a name="page-reliques-et-butin-la-moisson-des-échos"></a>

### La Moisson des Échos

> Avant le silence, ces salles abritaient des jardins.<br> Une jardinière coupa les racines noires chaque nuit.<br> Au matin, elles avaient appris le bruit de ses pas.<br> Elle laissa son outil et partit sans un mot.

<a name="page-reliques-et-butin-les-pas-du-retour"></a>

### Les Pas du Retour

> Le mousse sautait de coque en coque, au-dessus du vide.<br> Il promettait de revoir les pluies de son village.<br> Ses bottes furent retrouvées au bord d'un portail.<br> Peut-être a-t-il enfin tenu parole.

<a name="page-reliques-et-butin-le-dernier-pont"></a>

### Le Dernier Pont

> Nara tint le pont de purpur jusqu'à l'aube.<br> Derrière elle, les derniers exilés embarquèrent.<br> Le navire revint. Sa gardienne, jamais.<br> Sur la lame : « Qu'un autre trouve le retour. »

<a name="page-reliques-et-butin-la-veille-silencieuse"></a>

### La Veille Silencieuse

> Ce plastron protégea le veilleur du dernier quai.<br> Il allumait une lanterne pour les vaisseaux perdus.<br> Quand le ciel se tut, il resta à son poste.<br> Le métal garde encore la chaleur de la flamme.

<a name="page-reliques-et-butin-heaume-de-la-cartographe"></a>

### Heaume de la Cartographe

> Ilyne comptait les îles, jamais les jours.<br> Chaque entaille désignait un port disparu.<br> La dernière pointe vers une étoile immobile.<br> Personne n'a retrouvé cette route.

<a name="page-reliques-et-butin-le-soleil-enseveli"></a>

### Le Soleil Enseveli

> Un fossoyeur refusa d'enterrer le nom de sa reine.<br> Il traça sa vie sur les marches du temple.<br> Le sable effaça les mots, mais épargna son outil.<br> Chaque grain porte peut-être un fragment du récit.

<a name="page-reliques-et-butin-le-vœu-du-silence"></a>

### Le Vœu du Silence

> Le sonneur comprit trop tard ce qui répondait.<br> Il enveloppa ses bottes et descendit seul.<br> La cloche ne sonna plus jamais.<br> Dans le cuir subsiste une poussière de bronze.

<a name="page-reliques-et-butin-grèves-du-pèlerin-du-vide"></a>

### Grèves du Pèlerin du Vide

> Un pèlerin traversa cent îles sans chercher d'or.<br> Il portait les noms de ceux restés derrière.<br> Au dernier sanctuaire, il grava : « Je me souviens. »<br> Le voyage attend désormais d'autres pas.

<a name="page-reliques-et-butin-livres-et-tomes-dans-les-structures"></a>

## Livres et tomes dans les structures

Le pack possède **24 branches de génération de bonus**, chacune attachée à un advancement `player_generates_container_loot`. Lorsqu’un événement correspondant se produit, un entier de 1 à 100 choisit soit un livre/tome, soit aucune récompense. Les plages sont disjointes : il y a au plus **un livre supplémentaire par déclenchement**.

Le pack tente d’insérer la récompense dans le conteneur visé. Si aucun conteneur approprié n’est trouvé ou si l’insertion échoue, une fonction de secours donne le livre au joueur. Ce mécanisme n’est pas un remplacement de toutes les tables de butin : seules les quatre tables de reliques citées plus haut sont remplacées.

Le déclencheur concerne la génération du contenu, pas chaque réouverture d’un coffre déjà rempli. Les branches des coffres-forts des épreuves sont présentes dans les fichiers, mais leur déclenchement via cet événement n’a pas été validé en jeu ; leurs pourcentages restent ceux des fonctions prévues.

| Structure / coffre | Chance totale d’un bonus (%) | Répartition des bonus |
| --- | --- | --- |
| Ancienne cité | 26 | Manuscrit de Furtivité 8 %; Manuel : Second souffle 5 %; Manuel : Entrave 4 %; Tome de Vitalité 3 %; Manuel : Riposte 3 %; Manuel : Garde abyssale 3 % |
| Autres coffres de bastion | 16 | Traité des Âmes 5 %; Manuel : Lame infernale 4 %; Manuel : Bastion 4 %; Tome de Vigueur 3 % |
| Trésor de bastion | 23 | Traité des Âmes 7 %; Manuel : Lame infernale 6 %; Manuel : Bastion 5 %; Manuel : Second souffle 3 %; Tome de Vitalité 2 % |
| Trésor enfoui | 15 | Manuel : Garde abyssale 8 %; Tome de Vitalité 4 %; Manuel : Endurance 3 % |
| Pyramide du désert | 13 | Manuel : Longue portée 4 %; Manuel : Pas léger 4 %; Manuel : Impact 3 %; Tome de Vigueur 2 % |
| Cité de l’End | 19 | Manuel : Longue portée 5 %; Manuel : Allonge 4 %; Manuel : Second souffle 4 %; Codex du Raccommodage 3 %; Tome de Vigueur 3 % |
| Igloo | 9 | Manuel : Second souffle 4 %; Manuel : Endurance 3 %; Tome de Vitalité 2 % |
| Temple de la jungle | 14 | Manuel : Bûcheron 4 %; Manuel : Moisson 4 %; Manuel : Siphon 3 %; Manuel : Entrave 3 % |
| Mine abandonnée | 15 | Manuel : Excavation 5 %; Manuel : Allonge 4 %; Manuel : Endurance 4 %; Manuel : Bûcheron 2 % |
| Forteresse du Nether | 20 | Traité des Âmes 6 %; Manuel : Lame infernale 7 %; Manuel : Siphon 4 %; Manuel : Endurance 3 % |
| Avant-poste de pillards | 22 | Manuel : Impact 4 %; Manuel : Bastion 4 %; Manuel : Riposte 3 %; Manuel : Mécanisme rapide 3 %; Manuel : Perforation renforcée 3 %; Manuel : Volée 2 %; Manuel : Siège 3 % |
| Portail en ruine | 11 | Manuel : Lame infernale 5 %; Manuel : Longue portée 3 %; Manuel : Endurance 3 % |
| Trésor d’épave | 11 | Manuel : Garde abyssale 6 %; Manuel : Pas léger 3 %; Codex du Raccommodage 2 % |
| Donjon | 11 | Tome de Vitalité 3 %; Manuel : Siphon 3 %; Manuel : Endurance 3 %; Manuel : Exécution 2 % |
| Bibliothèque de forteresse | 19 | Codex du Raccommodage 4 %; Manuel : Exécution 3 %; Manuel : Longue portée 3 %; Manuel : Second souffle 3 %; Manuel : Endurance 3 %; Manuel : Allonge 3 % |
| Récompense de coffre-fort menaçant — à vérifier | 28 | Tome de la Rafale 8 %; Manuel : Volée 6 %; Manuel : Siège 6 %; Manuel : Second souffle 5 %; Tome de Vitalité 3 % |
| Récompense de coffre-fort — à vérifier | 23 | Tome de la Rafale 6 %; Manuel : Volée 5 %; Manuel : Siège 5 %; Manuel : Riposte 4 %; Tome de Vigueur 3 % |
| Grande ruine sous-marine | 11 | Manuel : Garde abyssale 6 %; Manuel : Moisson 3 %; Tome de Vigueur 2 % |
| Petite ruine sous-marine | 6 | Manuel : Garde abyssale 4 %; Manuel : Pas léger 2 % |
| Maison de cartographe | 8 | Tome de Vigueur 3 %; Manuel : Longue portée 3 %; Manuel : Allonge 2 % |
| Temple de village | 12 | Tome de Vitalité 4 %; Codex du Raccommodage 3 %; Manuel : Moisson 3 %; Manuel : Second souffle 2 % |
| Maison d’outilleur | 18 | Tome de Dextérité 4 %; Manuel : Excavation 4 %; Manuel : Endurance 3 %; Manuel : Allonge 2 %; Manuel : Bûcheron 3 %; Manuel : Moisson 2 % |
| Maison d’armurier d’armes | 14 | Manuel : Exécution 4 %; Manuel : Impact 3 %; Manuel : Endurance 2 %; Manuel : Lame infernale 3 %; Manuel : Siphon 2 % |
| Manoir | 24 | Manuel : Siphon 5 %; Manuel : Entrave 4 %; Manuel : Riposte 4 %; Manuel : Second souffle 3 %; Codex du Raccommodage 2 %; Manuel : Exécution 3 %; Manuel : Bastion 3 % |

<a name="page-reliques-et-butin-sources"></a>

## Sources

Les pools des reliques se trouvent à la fin de `data/minecraft/loot_table/chests/ancient_city.json`, `bastion_treasure.json`, `desert_pyramid.json` et `end_city_treasure.json`, avec leurs variantes d’overlay. Les dix objets sont définis dans `data/attuned/loot_table/relics/*.json` ; les traductions et récits proviennent de `resources.zip/assets/attuned/lang/fr_fr.json`.

Les livres/tomes sont définis dans `data/attuned/loot_table/books/*.json`. Leurs 24 chemins d’obtention relient `data/attuned/advancement/loot/*.json`, lignes 4–11, à `data/attuned/function/loot/structure/*.mcfunction`, puis à `loot/raycast.mcfunction`, lignes 1–5, et `loot/insert.mcfunction`, lignes 1–30. Le catalogue [butin-livres.csv](../catalogues/butin-livres.csv) conserve les 105 résultats possibles et chaque ligne source ; [reliques.json](../catalogues/reliques.json) conserve l’ensemble des fonctions de données personnalisées pour éviter de perdre les étapes d’initialisation.
