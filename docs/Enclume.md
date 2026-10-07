[Accueil du wiki](Home.md) · [Sommaire du dépôt](../README.md) · [Annexes](../ANNEXES.md)

<a name="page-enclume"></a>

# Enclume Attuned

L'enclume Attuned permet de **valider un palier d'histoire sur un objet**, avec un coût en lapis et en niveaux d'expérience. Son résultat dépend de l'objet inséré et de son histoire.

Les indications ci-dessous viennent du code de la **v0.17.1**. Les gestes et les transactions n'ont pas été testés dans une partie Minecraft pendant cette analyse.

<a name="page-enclume-installer-et-ouvrir-la-station"></a>

## Installer et ouvrir la station

Placez une enclume normale, ébréchée ou endommagée, puis regardez-la à proximité. La routine de station effectue une recherche devant les yeux du joueur toutes les cinq ticks, par pas de 0,25 bloc jusqu'à environ cinq blocs. Elle transforme l'enclume trouvée en station Attuned. L'interaction avec une enclume appelle également cette recherche.

La station est représentée techniquement par un wagonnet à coffre immobilisé affichant une enclume. **Ouvrez sa base** pour accéder à l'inventaire à trois lignes. Une enclume vanilla regardée peut ainsi être convertie automatiquement ; cette station utilise son propre fonctionnement pour les paliers d'histoire.

**Sources du ZIP :** `data/attuned/function/station/tick.mcfunction`, lignes 1–9 ; `function/station/scan.mcfunction`, lignes 1–4 ; `function/station/create.mcfunction`, lignes 1–4 ; `function/station/init.mcfunction`, lignes 1–7 ; `function/anvil/open.mcfunction`, lignes 1–4 ; `advancement/interaction/use_anvil.json`.

<a name="page-enclume-placer-lobjet-et-le-lapis"></a>

## Placer l'objet et le lapis

Comptez les colonnes de gauche à droite et les lignes du haut vers le bas.

| Emplacement | Rôle |
| --- | --- |
| Deuxième ligne, deuxième colonne | Objet à faire évoluer — case 11 en comptant depuis 1 |
| Deuxième ligne, quatrième colonne | Lapis ou blocs de lapis — case 13 |
| Deuxième ligne, huitième colonne | Aperçu du résultat et confirmation — case 17 |
| Troisième ligne, colonnes 1 à 5 | Sélection des paliers I, II, III, IV ou V |
| Troisième ligne, colonne 6 | Sélection automatique du prochain palier non réclamé |
| Troisième ligne, colonne 7 | Information descriptive sur l'histoire de l'objet |
| Troisième ligne, colonne 8 | Instructions |
| Troisième ligne, colonne 9 | Récupérer l'enclume après avoir vidé la station |

Placez votre objet suivi et le lapis demandé dans les deux cases d'entrée. Survolez le résultat pour vérifier le bonus et son prix. Cliquez sur le résultat pour valider : le jeton de résultat est remplacé par l'objet amélioré dans le curseur ou l'emplacement depuis lequel il a été sélectionné.

L'objet doit déjà être suivi par Attuned. Une armure doit donc avoir été portée, un outil ou une arme utilisé ou initialisé, ou provenir d'une recette Attuned compatible. L'insertion d'un objet quelconque dans la station ne l'initialise pas automatiquement.

**Sources du ZIP :** `data/attuned/function/station/cart_tick.mcfunction`, lignes 3–9 ; `function/station/render_controls.mcfunction`, lignes 1–48 ; `function/station/render.mcfunction`, lignes 1–6 ; `function/station/evaluate.mcfunction`, lignes 5–22 ; `function/station/read_token.mcfunction`, lignes 1–7 ; `function/station/claim.mcfunction`, lignes 8–10.

<a name="page-enclume-coût-des-niveaux-dexpérience"></a>

## Coût des niveaux d'expérience

| Palier choisi | Niveaux du joueur consommés |
| --- | ---: |
| I | 3 |
| II | 3 |
| III | 4 |
| IV | 4 |
| V | 4 |

Il s'agit de **niveaux** du joueur, pas des points d'histoire présents sur l'objet. L'histoire reste acquise. Un cycle complet I à V coûte 18 niveaux répartis sur cinq transactions, auxquels s'ajoute le lapis.

<a name="page-enclume-coût-du-lapis"></a>

## Coût du lapis

Le coût dépend du **bonus sélectionné**. Par exemple, une épée ayant surtout combattu dans le Nether peut recevoir Lame infernale dès son premier palier : le prix du lapis correspond alors à Lame infernale, même si le prix en niveaux est celui du palier I.

| Famille | Bonus | Lapis consommé |
| --- | --- | ---: |
| Arc | Main sûre I | 3 lapis-lazuli |
| Arc | Longue portée I | 1 bloc |
| Arc | Puissance, ajout d'un niveau | 3 blocs |
| Arc | Frappe, ajout d'un niveau | 5 blocs |
| Arc | Flamme, ajout d'un niveau | 8 blocs |
| Épée | Impact I | 3 lapis-lazuli |
| Épée | Exécution I | 1 bloc |
| Épée | Siphon I | 3 blocs |
| Épée | Lame infernale I | 5 blocs |
| Épée | Entrave I | 8 blocs |
| Pioche | Endurance I / Excavation I / Allonge I / seconde Endurance / seconde Excavation | Respectivement 3 lapis-lazuli / 1 / 3 / 5 / 8 blocs |
| Hache | Endurance I / Bûcheron I / Impact I / second Bûcheron / second Impact | Respectivement 3 lapis-lazuli / 1 / 3 / 5 / 8 blocs |
| Pelle | Endurance I / Excavation I / Allonge I / seconde Endurance / seconde Excavation | Respectivement 3 lapis-lazuli / 1 / 3 / 5 / 8 blocs |
| Houe | Endurance I / Moisson I / Allonge I / seconde Moisson / seconde Endurance | Respectivement 3 lapis-lazuli / 1 / 3 / 5 / 8 blocs |
| Arbalète | Mécanisme rapide I / Perforation renforcée I / Siège I / second Mécanisme rapide / second Siège | Respectivement 3 lapis-lazuli / 1 / 3 / 5 / 8 blocs |
| Bouclier | Chaque bonus d'histoire I à IV | 1 bloc par palier |
| Armure | Tout bonus d'histoire proposé | 3 lapis-lazuli par palier |

Les variantes « seconde » ajoutent un niveau à l'enchantement correspondant. Elles donnent normalement le niveau II si le niveau I est déjà présent ; le code ajoute un niveau et ne reconstruit pas tout le reste des enchantements de l'objet.

Un cycle complet de cinq bonus pour l'arc, l'arbalète, l'épée ou un outil demande au total **3 lapis-lazuli et 17 blocs de lapis**, indépendamment de l'ordre de sélection des cinq bonus. Un cycle complet d'armure à cinq paliers demande **15 lapis-lazuli**. Le bouclier à quatre paliers demande **4 blocs**, avec 14 niveaux d'XP répartis sur les quatre transactions.

**Sources du ZIP :** `data/attuned/function/station/evaluate.mcfunction`, lignes 70–75 ; `function/station/cost.mcfunction`, lignes 1–126 ; `function/station/apply_bonus.mcfunction` ; `item_modifier/anvil/history/*.json`, fonctions `minecraft:set_enchantments` ; `function/station/claim.mcfunction`, lignes 4–12. Les totaux sont calculés à partir de ces coûts.

<a name="page-enclume-ce-que-la-station-vérifie"></a>

## Ce que la station vérifie

Le code refuse la validation dans les situations suivantes : objet absent ou non suivi, type non accepté, ancien traitement d'enclume encore marqué comme en attente, palier supérieur au potentiel, palier déjà réclamé, saut de palier, histoire insuffisante, matériau non admis, absence de nouveau bonus à attribuer, lapis incorrect ou insuffisant, ou niveaux d'XP insuffisants.

Les conditions du [bouclier](Armures-et-boucliers.md) incluent les blocages à faible santé et, pour le dernier palier, une lignée passée par la reforge diamant. Les paliers ordinaires utilisent les seuils détaillés dans [Progression et histoire](Progression-et-histoire.md).

Le bouton contient l'identifiant de la station et sa révision. Le serveur vérifie que la station correspondante se trouve à six blocs ou moins et qu'elle n'a pas changé depuis la création du bouton. La transaction revérifie ensuite les entrées. Ces contrôles sont présents dans le code ; ils ne remplacent pas un test multijoueur de concurrence et de déplacement d'objets.

**Sources du ZIP :** `data/attuned/function/station/evaluate.mcfunction`, lignes 1–76 ; `function/station/check_standard.mcfunction` ; `function/station/check_shield.mcfunction` ; `function/station/request.mcfunction`, lignes 1–8 ; `function/station/claim.mcfunction`, lignes 1–15.

<a name="page-enclume-récupérer-lenclume"></a>

## Récupérer l'enclume

Retirez tous les objets personnels et le lapis de l'inventaire, puis utilisez « Récupérer l'enclume ». Le code vérifie les 27 cases, retire la station vide et remet une enclume dans l'emplacement du bouton sélectionné. Les éléments d'interface ne sont pas comptés comme des objets personnels.

La station est invulnérable et maintenue à son point d'ancrage. Utilisez donc son bouton de récupération pour la déplacer.

**Sources du ZIP :** `data/attuned/function/station/dismantle.mcfunction`, lignes 1–35 ; `function/station/init.mcfunction`, ligne 5 ; `function/station/anchor_tick.mcfunction`, lignes 1–6.

<a name="page-enclume-limites-de-linterface-v0171"></a>

## Limites de l'interface v0.17.1

La station n'a pas d'action de réparation manuelle, de fusion de deux équipements, de renommage ou de reforge d'armure. Des fonctions d'une ancienne interface existent toujours dans l'archive, mais son contrôleur exige une session `attw_anvil_t` positive que l'ouverture actuelle ne démarre plus.

De même, l'icône « Histoire de l'objet » sert de notice dans cette interface. Elle ne lance pas le rapport détaillé de l'ancienne interface. Voir les commandes administratives pour consulter directement l'histoire.

**Sources du ZIP :** `data/attuned/function/station/request.mcfunction`, lignes 4–7 ; `function/station/render_controls.mcfunction`, lignes 43–44 ; `function/anvil/open.mcfunction`, lignes 1–4 ; `function/anvil/process.mcfunction`, lignes 1–6 et 66–68. Recherche statique sur l'ensemble des overlays : aucun démarrage positif de `attw_anvil_t`.
