[Accueil du wiki](Home.md) · [Sommaire du dépôt](../README.md) · [Annexes](../ANNEXES.md)

<a name="page-forge"></a>

# Forge et changement de matériau

La table de forge change le **matériau** de certains équipements existants. L'enclume Attuned valide séparément leurs **évolutions d'histoire**. Dans la v0.17.1, passer un arc de bois à pierre ne forge plus automatiquement le palier I : les deux opérations ont leurs conditions et leurs dépenses.

<a name="page-forge-ouvrir-le-menu"></a>

## Ouvrir le menu

Tenez l'objet suivi en main principale, puis utilisez une table de forge. Un menu est proposé selon son type et son matériau. Dans les versions anciennes, il utilise des messages cliquables ; dans les versions dotées de dialogues, il utilise ces dialogues. La session de forge dure **100 ticks**, soit environ cinq secondes à 20 ticks par seconde. Après une opération, la session est fermée : rouvrez la table pour la suivante.

Les opérations listées ci-dessous prélèvent les matériaux dans l'inventaire du joueur. Elles ne demandent pas de niveaux d'XP, sauf la capacité spéciale Volée décrite plus bas.

**Sources du ZIP :** `data/attuned/advancement/interaction/use_smithing_table.json`, lignes 3–20 ; `function/forge/open.mcfunction`, lignes 32–69 ; `function/tick.mcfunction`, lignes 12 et 16 ; `function/forge/process.mcfunction`, lignes 1–23 ; `overlay_88/data/attuned/function/forge/open.mcfunction`, lignes 35–74.

<a name="page-forge-arcs-et-arbalètes"></a>

## Arcs et arbalètes

| Transition | Histoire minimale sur le même objet | Coût |
| --- | ---: | --- |
| Bois → pierre | 25 tirs/utilisations | 2 pierres `cobblestone` |
| Pierre → cuivre | 100 | 2 lingots de cuivre |
| Cuivre → fer | 250 | 2 lingots de fer |
| Fer → diamant | 500 | 2 diamants |
| Diamant → netherite | Aucun nouveau seuil de tir contrôlé par cette fonction | 1 modèle d'amélioration en netherite + 1 lingot de netherite |

Les quatre premières opérations demandent aussi que le déblocage naturel de l'arc (`steady_hand`) ou de l'arbalète (`mechanism`) ait été enregistré. Ces marqueurs s'obtiennent par les premières utilisations. Posséder un enchantement du même nom par un autre moyen ne remplace pas forcément ce marqueur d'histoire.

L'or est une branche de fabrication directe à potentiel II. Aucune chaîne de reforge depuis ou vers l'or n'est proposée par ces fonctions.

**Sources du ZIP :** `data/attuned/function/forge/to_{stone,copper,iron,diamond}.mcfunction`, lignes 1–13 ; `function/forge/crossbow_to_{stone,copper,iron,diamond}.mcfunction`, lignes 1–13 ; `function/forge/to_netherite.mcfunction`, lignes 1–12 ; `function/forge/crossbow_to_netherite.mcfunction` ; `function/history/check_bow_unlocks.mcfunction`, lignes 1–3 ; `function/history/increment_crossbow_shots.mcfunction`, lignes 1–9.

<a name="page-forge-épées-pioches-haches-pelles-et-houes"></a>

## Épées, pioches, haches, pelles et houes

| Transition | Condition | Coût |
| --- | --- | --- |
| Bois → pierre | Déblocage d'histoire du bois, obtenu à 25 utilisations | 2 pierres `cobblestone` |
| Pierre → cuivre | Déblocage d'histoire de la pierre, obtenu à 100 utilisations | 2 lingots de cuivre |
| Cuivre → fer | Déblocage d'histoire du cuivre, obtenu à 250 utilisations | 2 lingots de fer |
| Cuivre ou fer → diamant à l'évolution II | Évolution II déjà forgée | 2 diamants |
| Cuivre ou fer → diamant à l'évolution III | Évolution III déjà forgée | 3 diamants |
| Cuivre ou fer → diamant à l'évolution IV | Évolution IV déjà forgée | 4 diamants |
| Diamant → netherite | Transformation de forge vanilla | Objet diamant + modèle d'amélioration en netherite + lingot de netherite |

Le raccourci vers le diamant conserve l'évolution déjà acquise. Il ne met pas gratuitement l'objet au palier suivant. Les coûts II/III/IV concernent bien le niveau d'évolution enregistré, pas simplement le nombre d'utilisations.

Avant les versions possédant des équipements en cuivre natifs, le cuivre intermédiaire emploie une base en fer. Son identité Attuned reste « cuivre ». Après l'arrivée du cuivre natif, l'overlay correspondant utilise les objets en cuivre du jeu. La compatibilité explique cette représentation selon les versions.

**Sources du ZIP :** `data/attuned/function/forge/equipment/to_stone.mcfunction`, lignes 1–13 ; `to_copper.mcfunction`, lignes 1–13 ; `to_iron.mcfunction`, lignes 1–13 ; `to_diamond.mcfunction`, lignes 1–7 ; `to_diamond_e2.mcfunction`, lignes 1–5 ; `to_diamond_e3.mcfunction`, lignes 1–5 ; `to_diamond_e4.mcfunction`, lignes 1–5 ; `function/history/check_equipment_milestones.mcfunction`, lignes 1–4 ; `function/history/increment_uses.mcfunction`, lignes 5–6 ; `function/evolution/finalize_netherite.mcfunction` ; `function/forge/equipment/sword_stone_to_copper.mcfunction`, lignes 1–7.

<a name="page-forge-boucliers"></a>

## Boucliers

Le parcours actuel met en avant les boucliers **fer → diamant → netherite**. Les anciennes formes bois/cuivre encore présentes dans les fonctions peuvent être migrées automatiquement en fer lors du traitement des blocages.

| Opération | Conditions | Coût |
| --- | --- | --- |
| Reforge du bouclier de fer en diamant | Type bouclier, matériau fer, potentiel exactement IV, évolution au moins II | 3 diamants |
| Amélioration en netherite | Recette de forge `smithing_transform` | 1 modèle + 1 bouclier + 1 lingot de netherite |

La reforge diamant ajoute le marqueur de lignée `diamond_forged`. Celui-ci est demandé par le palier IV du bouclier. Un bouclier de diamant fabriqué directement a un potentiel III ; son passage en netherite ne lui confère donc pas automatiquement le dernier palier.

**Détail d'implémentation à connaître :** le texte de l'interface demande un bouclier de diamant pour la netherite, mais la recette accepte tout objet `minecraft:shield`, sans filtre de matériau Attuned. Contourner l'étape diamant avec cette recette n'ajoute pas le marqueur `diamond_forged` exigé par le dernier palier.

**Sources du ZIP :** `data/attuned/function/forge/shield_to_diamond.mcfunction`, lignes 1–10 ; `function/forge/shield_to_netherite.mcfunction`, ligne 1 ; `recipe/shield/netherite_upgrade.json`, champs `template`, `base`, `addition` et `result` ; `item_modifier/material/shield_diamond.json`, lignes 1–16 ; `function/station/check_shield.mcfunction`, lignes 14–17 ; `function/shield/migrate_legacy_mainhand.mcfunction`, lignes 1–4 ; `recipe/shield/diamond.json`.

<a name="page-forge-conservation-pendant-les-transformations"></a>

## Conservation pendant les transformations

La reforge des épées et outils copie l'objet entier dans un stockage temporaire, remplace son identifiant de matériau, puis remet les composants sur l'objet en main principale. Les transformations d'arcs et arbalètes modifient leurs données de matériau, leur modèle, leur nom et leur durabilité maximale. Ces chemins n'effacent pas volontairement le compteur d'histoire ou tous les enchantements.

Le nom personnalisé peut être remplacé par le nom Attuned du nouveau matériau. Les commandes n'effectuent pas toutes une remise à zéro de la composante d'usure : ne considérez pas la reforge comme une réparation garantie.

La synchronisation diamant → netherite des épées et outils protège généralement le potentiel d'une lignée déjà évoluée. Un objet diamant neuf de potentiel III transformé à l'évolution 0 suit toutefois un chemin spécifique qui fixe son potentiel à II. Monter son histoire avant d'améliorer le matériau peut donc changer la marge de progression conservée.

**Sources du ZIP :** `data/attuned/function/forge/equipment/sword_to_diamond_keep_evolution.mcfunction`, lignes 1–7 ; `function/evolution/finalize_netherite.mcfunction`, lignes 1–30 ; `item_modifier/evolution/sword_sync_netherite_direct.json`, lignes 1–6 ; `sword_sync_netherite_partial.json`, lignes 1–13 ; `item_modifier/evolution/to_stone_bow.json` ; `sync_netherite_bow.json`.

<a name="page-forge-limitation-actuelle-des-armures"></a>

## Limitation actuelle des armures

L'archive contient une reforge d'armure cuivre → fer à partir de l'évolution I pour **2 lingots de fer**, puis fer → diamant aux évolutions II/III/IV pour **2/3/4 diamants**. Elle est appelée depuis l'ancien contrôleur d'enclume, dont la session n'est plus ouverte par l'interface actuelle.

Ces fonctions sont donc décrites comme **présentes mais non accessibles par le parcours normal identifié**. Ne pas présenter leur existence comme une fonctionnalité jouable vérifiée.

De plus, la sélection des menus de table de forge exclut arcs, arbalètes et boucliers des menus d'outils, mais pas les armures. Une armure suivie en cuivre, fer ou diamant peut ainsi être envoyée vers un menu d'outil. Certaines actions prélèvent leurs matériaux avant de sélectionner le type précis ; aucune branche de transformation d'armure n'est alors exécutée. **Évitez ces actions de reforge proposées sur une armure dans cette version**, tant que ce parcours n'a pas été corrigé ou validé en jeu.

**Sources du ZIP :** `data/attuned/function/forge/armor/route.mcfunction`, lignes 1–4 ; `forge/armor/to_iron.mcfunction`, lignes 1–8 ; `forge/armor/to_diamond.mcfunction`, lignes 1–6 ; `function/anvil/process.mcfunction`, lignes 1–2 et 66–68 ; `function/anvil/open.mcfunction`, lignes 1–4 ; `function/forge/open.mcfunction`, lignes 61–63 ; `function/forge/equipment/to_diamond_e2.mcfunction`, lignes 1–5 ; `function/forge/equipment/perform_to_diamond_keep_evolution.mcfunction`.

<a name="page-forge-volée-à-la-forge--ancien-marqueur-requis"></a>

## Volée à la forge : ancien marqueur requis

La forge conserve une action de Volée I pour un arc en netherite : évolution au moins III, déblocage `capstone`, marqueur `applied.longshot`, absence de `applied.volley`, **8 blocs de lapis et 10 niveaux**.

Le nouveau bonus de Longue portée posé par la station marque `applied.bow_long`, tandis que cette action teste encore `applied.longshot`. Elle n'est donc pas garantie accessible à un arc construit uniquement par le nouveau parcours. Le catalogue [Enchantements](Enchantements.md) décrit les autres voies d'acquisition de Volée ; cette divergence doit être traitée comme une limite de cette ancienne action.

**Sources du ZIP :** `data/attuned/function/forge/capstone_volley.mcfunction`, lignes 1–21 ; `item_modifier/anvil/history/bow_long.json`, champ `attuned.applied.bow_long`.
