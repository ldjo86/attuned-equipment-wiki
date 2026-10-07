[Accueil du wiki](Home.md) · [Sommaire du dépôt](../README.md) · [Annexes](../ANNEXES.md)

<a name="page-audit-technique"></a>

# Audit technique de l’archive v0.17.1

<a name="page-audit-technique-périmètre-et-résultat"></a>

## Périmètre et résultat

Cet audit examine le datapack `Attuned_Equipment_DP_1.21.x_v0.17.1.zip` et le pack de ressources présent dans son fichier `resources.zip`. Il repose sur l’analyse des fichiers fournis, leur composition selon les overlays, la résolution des références locales et le décodage des textures. **Aucun serveur ni client Minecraft n’a été lancé.**

Les fichiers JSON examinés sont syntaxiquement valides et les références locales analysées ne présentent pas de cible absente. L’examen des transactions révèle néanmoins des problèmes de parcours de forge et d’enclume, ainsi qu’un risque d’achats successifs de tomes. Les contrôles de ressources mettent aussi en évidence le rapport de tests resté en v0.16.1, les commerces réservés à un registre de Java 26.1 et les états de tension visuellement identiques dans le RP.

Les chemins cités ci-dessous sont relatifs au ZIP du datapack ; un chemin précédé de `RP:` se trouve à l’intérieur de `resources.zip`.

<a name="page-audit-technique-priorités-de-vérification"></a>

## Priorités de vérification

| Priorité | Point | Conséquence ou action utile |
| --- | --- | --- |
| Haute | Routage d’une armure vers une reforge d’outil | Tester le prélèvement sans conversion ; filtrer le type avant paiement dans une future correction |
| Haute | Achats successifs de tomes | Vérifier qu’une interaction n’achète qu’un rang et qu’un tome existe pour chaque achat |
| Haute | Ancien parcours d’enclume sans ouverture de session | Décider quelles opérations doivent rejoindre la nouvelle station |
| À confirmer en jeu | Fractions négatives de réparation scriptée | Mesurer la durabilité avant/après sur Java, sans confondre les autres effets de réparation |
| Moyenne | Marqueur ancien requis par Volée à la forge | Harmoniser les marqueurs si cette voie doit rester accessible |
| Documentation | Validation v0.16.1, échanges dormants, modèles de tension identiques | Décrire la version actuelle avec ses limites, sans reprendre d’anciennes promesses |

Ce tableau ne représente pas une correction du datapack. Les observations décrivent l’archive fournie ; aucune fonction du pack n’a été modifiée pour produire le wiki.

<a name="page-audit-technique-résultats-chiffrés"></a>

## Résultats chiffrés

| Contrôle | Résultat | Interprétation |
| --- | ---: | --- |
| Fichiers JSON du datapack analysés | 2 367 | Inclut les copies des overlays |
| Fichiers JSON du RP analysés | 101 | Modèles, objets et langues |
| Fichiers `pack.mcmeta` analysés | 2 | Un par pack |
| Erreurs de syntaxe JSON | 0 | N’inclut pas la validation des schémas propres au jeu |
| Clés JSON dupliquées détectées | 0 | Contrôle effectué pendant l’analyse des objets JSON |
| PNG décodés | 43 sur 43 | Tous mesurent 16 × 16 pixels |
| Références de modèles locaux dans le RP | 139 | Toutes résolues |
| Références de textures locales dans le RP | 120 | Toutes résolues |
| Références vers des modèles vanilla externes au RP | 88 | Dépendances du jeu, pas fichiers manquants du pack |
| Références vers des textures vanilla externes au RP | 10 | Dépendances du jeu, non vérifiées depuis un JAR client |
| Références DP à un `item_model` Attuned | 580 occurrences, 17 identifiants | Les 17 définitions du RP existent |
| Dictionnaires Attuned | 7 × 1 469 clés | Même ensemble de clés ; 5 copies anglaises et 2 copies françaises |
| Clés Attuned `translate` trouvées littéralement dans le DP | 1 445 | Toutes présentes dans les dictionnaires |
| Textures Attuned sans référence directe dans les JSON du RP | 11 | Ressources présentes, sans usage visuel établi par ces fichiers |

Les comptes de références sont des occurrences trouvées par l’analyseur, pas des objets distincts ni des assertions de gameplay. Les références vanilla sont classées séparément : le JAR Minecraft n’a pas été fourni avec l’archive.

<a name="page-audit-technique-composition-des-overlays"></a>

### Composition des overlays

| Vue du datapack | Fichiers remplacés par l’overlay | Fichiers ajoutés | Fichiers retenus | Références locales manquantes reconnues |
| --- | ---: | ---: | ---: | ---: |
| Base, formats 48–56 | 0 | 0 | 2 719 | 0 |
| Base + `overlay_57` | 72 | 0 | 2 719 | 0 |
| Base + `overlay_61` | 301 | 0 | 2 719 | 0 |
| Base + `overlay_71` | 857 | 2 | 2 721 | 0 |
| Base + `overlay_80` | 870 | 2 | 2 721 | 0 |
| Base + `overlay_88` | 892 | 2 | 2 721 | 0 |
| Base + `overlay_94` | 903 | 2 | 2 721 | 0 |

Les fichiers retenus ne sont pas nécessairement tous chargés comme ressources en jeu. Ils comprennent par exemple les dossiers `dialog` et `villager_trade`, qui ne sont pas connus de toutes les versions visées.

La base contient 1 561 fonctions ; les overlays à partir de `overlay_71` ajoutent `localization/children.mcfunction` et `localization/children_loop.mcfunction`, portant la vue à 1 563 fonctions. Les 4 255 fichiers `.mcfunction` physiquement présents dans l’archive incluent donc de nombreuses variantes de compatibilité et ne représentent pas 4 255 fonctions actives différentes.

<a name="page-audit-technique-points-dentrée"></a>

### Points d’entrée

| Tag | Fonctions déclarées | Vérification |
| --- | --- | --- |
| `data/minecraft/tags/function/load.json` | `attuned:load`, `attuned:station/load` | Deux cibles présentes |
| `data/minecraft/tags/function/tick.json` | `attuned:tick`, `attuned:station/tick` | Deux cibles présentes |

Les catégories de références contrôlées comprennent les appels littéraux de fonctions, les fonctions de récompense et d’effets, les prédicats, les modificateurs d’objets appelés par commande, les références de tables de butin, les parents de progrès et les valeurs des tags. L’extraction de commandes reste statique ; elle ne remplace pas le parseur Brigadier ni l’exécution des macros par Minecraft.

<a name="page-audit-technique-constats-à-intégrer-dans-la-publication"></a>

## Constats à intégrer dans la publication

<a name="page-audit-technique-1-le-rapport-de-tests-ne-correspond-pas-à-la-version-de-larchive"></a>

### 1. Le rapport de tests ne correspond pas à la version de l’archive

**État : incohérence documentaire certaine.**

`VALIDATION.md`, ligne 1, annonce v0.16.1. Sa ligne 3 revendique 1 860 assertions sur douze versions de Java. `LISEZ-MOI_1.21.txt`, ligne 1, annonce aussi v0.16.1 et recommande le RP v0.16.1. `pack.mcmeta`, ligne 13, `RP:pack.mcmeta`, ligne 13, et `INSTALLATION_v0.17.1.txt`, ligne 1, indiquent v0.17.1.

**Conséquence :** ne pas présenter les 1 860 assertions comme des tests exécutés sur v0.17.1. Publier le présent résultat comme un audit statique et conserver le rapport antérieur uniquement avec son attribution de version. Un nouveau rapport de tests en jeu devra identifier l’archive testée et son empreinte.

<a name="page-audit-technique-2-les-commerces-par-fichiers-villager_trade-sont-hors-de-la-cible-121x"></a>

### 2. Les commerces par fichiers `villager_trade` sont hors de la cible 1.21.x

**État : fonctionnalité présente dans les fichiers, inactive dans les versions ciblées.**

La base contient 36 fichiers `data/attuned/villager_trade/*.json` et 7 tags dans `data/minecraft/tags/villager_trade/`. Les notes officielles [Java 26.1, « Data-driven Villager Trades »](https://www.minecraft.net/en-us/article/minecraft-java-edition-26-1) introduisent ce registre et son dossier. Ces offres ne sont donc pas une voie d’obtention utilisable dans Java 1.21.x par le simple chargement de ces fichiers.

**Conséquence :** documenter les offres comme données préparées ou héritées d’une autre édition, sans les annoncer comme une fonctionnalité jouable de ce ZIP. Leur présence ne rend pas l’ensemble du pack compatible 26.1.

<a name="page-audit-technique-3-les-états-de-tension-des-arcs-et-arbalètes-sont-identiques"></a>

### 3. Les états de tension des arcs et arbalètes sont identiques

**État : égalité des modèles confirmée statiquement.**

Pour les matériaux `stone`, `copper`, `iron`, `golden`, `diamond`, `netherite`, chacun des quatre fichiers de la famille `RP:assets/attuned/models/item/bow/<matériau>{,_pulling_0,_pulling_1,_pulling_2}.json` contient le même objet JSON. Il en va de même pour les quatre fichiers correspondants de `crossbow/`.

Les définitions modernes sélectionnent pourtant ces états. Exemple : `RP:assets/attuned/items/bow/copper.json`, lignes 10–31, sélectionne les modèles de tension selon la durée d’utilisation ; les quatre modèles concernés partagent la même texture et les mêmes transformations. Les états d’arbalète chargée avec flèche ou fusée constituent, eux, des modèles distincts avec une couche de projectile.

**Conséquence :** ne pas promettre une animation personnalisée de déformation de l’arme sur la seule base de ces noms de fichiers. Pour une future correction, fournir des modèles ou textures distincts par étape puis contrôler le rendu dans le client. Le rendu existant n’a pas été observé en jeu pendant l’audit.

<a name="page-audit-technique-4-onze-textures-personnalisées-ne-sont-pas-reliées-aux-modèles-fournis"></a>

### 4. Onze textures personnalisées ne sont pas reliées aux modèles fournis

**État : absence de référence directe dans les JSON du RP.**

- `RP:assets/attuned/textures/item/bow/` : les six fichiers `<matériau>_base.png`.
- `RP:assets/attuned/textures/item/crossbow/` : `arrow_multishot.png`, `firework_multishot.png`, `spectral_arrow.png`, `spectral_arrow_multishot.png`, `tipped_arrow_multishot.png`.

**Conséquence :** le wiki peut les montrer dans l’inventaire des fichiers, mais ne doit pas en déduire que ces variantes sont visibles en jeu. Ce constat n’est pas une erreur de chargement : les textures peuvent être conservées en réserve ou destinées à une version future.

<a name="page-audit-technique-5-les-remplacements-vanilla-ont-une-portée-globale"></a>

### 5. Les remplacements vanilla ont une portée globale

**État : choix d’implémentation à expliquer.**

Le modèle `RP:assets/minecraft/models/block/template_anvil.json`, lignes 3–6 et 44–117, utilise les textures vanilla d’enclume et de diamant pour modifier le socle. Trois PNG modifient la table d’enchantement. Six modèles d’objets vanilla sont remplacés par `overlay_legacy` sur les anciennes versions.

Le datapack remplace également `data/minecraft/loot_table/chests/end_city_treasure.json`, `ancient_city.json`, `bastion_treasure.json` et `desert_pyramid.json`, avec des variantes dans les overlays.

**Conséquence :** expliquer les conflits possibles quand un autre pack fournit ces mêmes chemins. Le RP agit sur des modèles vanilla partagés ; la personnalisation de l’enclume ne dépend pas uniquement de la conversion de chaque station par les fonctions du datapack.

<a name="page-audit-technique-6-couverture-des-langues-complète-en-clés-plus-limitée-en-variantes-régionales"></a>

### 6. Couverture des langues complète en clés, plus limitée en variantes régionales

**État : ensembles de clés cohérents ; variantes régionales dupliquées.**

Les cinq dictionnaires anglais ont la même empreinte ; les deux dictionnaires français ont la même empreinte. Chaque fichier contient 1 469 clés et aucune valeur vide. Les dictionnaires français et anglais ont les mêmes paramètres de substitution `%s` / `%d` reconnus par le contrôle complémentaire.

Les deux fichiers `RP:assets/minecraft/lang/{en_us,fr_fr}.json` ne contiennent qu’une entrée, `block.minecraft.enchanting_table`, pour son renommage global. Ce petit remplacement n’est pas dupliqué dans les autres codes de langue à cet emplacement.

**Conséquence :** annoncer deux langues avec leurs alias régionaux, sans présenter sept localisations indépendantes. La présence des clés ne certifie pas l’orthographe et la qualité de toutes les traductions.

<a name="page-audit-technique-transactions-et-parcours-de-gameplay"></a>

## Transactions et parcours de gameplay

<a name="page-audit-technique-7-routage-de-la-forge-darmure-vers-des-transactions-doutils"></a>

### 7. Routage de la forge d’armure vers des transactions d’outils

**État : chemin problématique confirmé dans le code ; conséquence à reproduire en jeu.**

`data/attuned/function/forge/open.mcfunction`, lignes 61–63, sélectionne des menus génériques pour un objet Attuned en cuivre, fer ou diamant en excluant seulement l’arc, l’arbalète et le bouclier. Une armure suivie peut donc entrer dans ces menus. Les transactions de conversion en diamant contrôlent le matériau et l’évolution, prélèvent les diamants, puis ne distribuent la conversion qu’aux types `sword`, `pickaxe`, `axe`, `shovel` et `hoe`.

Par exemple, une armure en fer d’évolution II peut atteindre une route qui consomme **2 diamants** sans appliquer une conversion d’armure. Les variantes de coût III et IV sont également concernées par le même dispatch. Une vérification en monde de test reste nécessaire pour constater l’effet complet de l’interaction.

**Sources :** `function/forge/equipment/to_diamond.mcfunction`, lignes 1–7 ; `to_diamond_e2.mcfunction`, lignes 1–5 ; `perform_to_diamond_keep_evolution.mcfunction` ; `overlay_88/data/attuned/function/forge/open.mcfunction`, lignes 66–68. Les chemins abrégés commencent à `data/attuned/`.

Voir [Forge](Forge.md) et [Armures et boucliers](Armures-et-boucliers.md).

<a name="page-audit-technique-8-lancien-traitement-denclume-na-plus-de-session-ouverte-normalement"></a>

### 8. L’ancien traitement d’enclume n’a plus de session ouverte normalement

**État : absence de voie normale d’ouverture constatée statiquement.**

`anvil/process.mcfunction` exige un score positif `attw_anvil_t`. Dans la base et ses variantes, aucune commande ne démarre positivement cette session ; `anvil/open.mcfunction` appelle la nouvelle détection de station. Les anciennes fonctions de réparation manuelle, de consultation d’histoire et de reforge d’armure restent présentes, mais ne constituent pas des options normalement accessibles dans cette interface.

L’icône d’histoire de la nouvelle station utilise `action:0`, alors que le traitement des boutons ne lui associe pas de rapport détaillé. Elle doit être présentée comme descriptive.

**Sources :** `data/attuned/function/anvil/open.mcfunction`, lignes 1–4 ; `anvil/process.mcfunction`, lignes 1–6 et 66–68 ; `player_init.mcfunction` ; `station/render_controls.mcfunction`, lignes 43–44 ; `station/request.mcfunction`, lignes 4–7.

Les dix fonctions historiques `history/catchup/level_1..5` et `history/ranged/level_1..5` ne reçoivent aucun appel littéral dans les sept vues base + overlay. Ce contrôle d’appels n’interdit pas une invocation directe par un administrateur ; il décrit leur intégration au parcours normal.

<a name="page-audit-technique-9-une-interaction-avec-un-tome-peut-acheter-plusieurs-rangs"></a>

### 9. Une interaction avec un tome peut acheter plusieurs rangs

**État : conséquence directe de l’ordre des commandes, à confirmer en jeu.**

Chaque fonction `tomes/<type>/try` teste les rangs l’un après l’autre. Un achat réussi modifie immédiatement le rang, qui peut satisfaire le test suivant. Les fonctions de rang vérifient le lapis et l’XP, mais ne revérifient pas la présence du tome et ne conditionnent pas la progression au succès de sa consommation.

Le chemin de Vitalité peut ainsi parcourir I à V avec **32 blocs de lapis et 61 niveaux d’XP** disponibles, même si seul le premier tome a été consommé avec succès. Il faut contrôler le résultat dans Minecraft avant de publier un correctif. Le changement approprié serait de sélectionner un seul rang par interaction et de vérifier tous les ingrédients avant paiement.

**Sources :** `data/attuned/function/tomes/vitality/try.mcfunction`, lignes 2–8 ; `tomes/vitality/level_1.mcfunction` et `level_2.mcfunction`, lignes 1–13 ; `tomes/vigor/try.mcfunction` et `tomes/dexterity/try.mcfunction`, lignes 2–6.

Voir les coûts complets dans [Tomes et savoirs](Tomes-et-savoirs.md) et les autres observations dans [Audit des enchantements et du butin](Audit-enchantements-et-butin.md).

<a name="page-audit-technique-10-entretien-scripté--signe-de-durabilité-à-vérifier"></a>

### 10. Entretien scripté : signe de durabilité à vérifier

**État : suspicion qualifiée, sans affirmation de résultat en jeu.**

Les modificateurs de réparation scriptée des outils, armes à distance et boucliers emploient `minecraft:set_damage` avec `add:true` et des fractions négatives. Il faut vérifier précisément la signification du signe et les arrondis sur les versions Java ciblées, en mesurant la durabilité avant/après. Aucun document Bedrock n’est utilisé comme preuve du comportement Java dans cet audit.

Ce constat ne concerne pas indistinctement tous les entretiens. En particulier, l’overlay 94 des enchantements de familiarité d’épée et d’armure utilise `minecraft:change_item_damage`, une opération différente.

**Sources :** `data/attuned/item_modifier/history/familiarity/repair/**` ; `data/attuned/function/history/familiarity/repair/**` ; `overlay_94/data/attuned/enchantment/weapon_familiarity.json` et `armor_familiarity.json`.

<a name="page-audit-technique-11-autres-différences-entre-les-anciens-chemins-et-la-station"></a>

### 11. Autres différences entre les anciens chemins et la station

| Observation | Niveau de preuve | Source principale |
| --- | --- | --- |
| Volée à la forge attend `applied.longshot`, alors que le nouveau bonus écrit `applied.bow_long` | Incohérence statique de marqueur ; un objet neuf suivant ce seul parcours n’obtient pas l’ancien marqueur | `function/forge/capstone_volley.mcfunction`, lignes 9–10 ; `item_modifier/anvil/history/bow_long.json` |
| La recette netherite du bouclier accepte tout objet `minecraft:shield` | Filtre JSON certain ; les exigences de lignée du palier IV restent contrôlées ailleurs | `recipe/shield/netherite_upgrade.json` ; `function/station/check_shield.mcfunction`, ligne 16 |
| Les golems du Bastion sont créés dans la dimension du joueur, mais l’entretien ne parcourt pas explicitement les dimensions | Durée de vie hors Overworld à vérifier | `function/shield/summon_bastion.mcfunction` ; `function/maintenance/slow_20t.mcfunction`, lignes 5–7 |
| La Maîtrise annonce « deux enchantements au total », sans limiter tous ceux déjà présents | Écart entre le texte et les opérations | [Audit des enchantements et du butin](Audit-enchantements-et-butin.md) |
| Les récompenses prévues pour les coffres-forts des épreuves reposent sur un événement dont le déclenchement n’a pas été démontré ici | Disponibilité à tester | `advancement/loot/trial_reward.json` et `trial_ominous.json` |

Les valeurs et références détaillées du gameplay sont conservées dans [findings-gameplay.json](../reference/findings-gameplay.json) ; le volet livres, enchantements et butin figure dans [findings-enchantments.json](../reference/findings-enchantments.json).

<a name="page-audit-technique-limites-de-laudit"></a>

## Limites de l’audit

La syntaxe JSON et les chemins locaux peuvent être valides malgré une propriété inadaptée à une version du jeu. Cet audit ne charge pas les registres via les codecs Minecraft et n’exécute pas les fonctions, les macros ni les séquences d’interaction.

Il ne mesure pas non plus les performances à plusieurs joueurs, les interactions avec des mods ou plugins serveur, la conservation des données pendant toutes les migrations, ni les résultats graphiques à toutes les perspectives. Les 43 textures sont montrées par assemblage des pixels originaux, sans génération d’illustration et sans simulation d’une capture de jeu.

Les tests historiques annoncés dans `VALIDATION.md` sont une information du paquet fourni. Ils n’ont pas été reproduits ici et leur attribution v0.16.1 doit rester visible.

<a name="page-audit-technique-vérifications-en-jeu-utiles-avant-une-publication-de-compatibilité"></a>

## Vérifications en jeu utiles avant une publication de compatibilité

1. Charger cette archive précise dans un monde de test pour chaque version revendiquée, puis conserver les journaux de chargement et de `/reload`.
2. Vérifier la forge et la table d’enchantement dans les deux interfaces : chat sur 1.21–1.21.5, dialogues sur 1.21.6–1.21.11.
3. Contrôler les modèles d’arc et d’arbalète pendant toute la tension et après chargement, puis les boucliers dans les deux mains et en blocage.
4. Tester la conservation du nom personnel, de la durabilité, des enchantements et de l’histoire lors des évolutions et de la migration des textes.
5. Contrôler la génération des reliques dans de nouveaux coffres, ainsi que les bonus reposant sur des progrès de génération de butin, avec une attention particulière aux coffres-forts des chambres d’épreuves.
6. Vérifier les cas de station partagée, de confirmation répétée, d’inventaire plein et d’association avec un autre pack utilisant les mêmes tables vanilla.

Les essais doivent produire un rapport propre à v0.17.1. Une déclaration de support dans `pack.mcmeta` et une inspection statique constituent des éléments utiles, mais ne suffisent pas à certifier ces scénarios.
