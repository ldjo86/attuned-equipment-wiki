[Accueil du wiki](Home.md) · [Sommaire du dépôt](../README.md) · [Annexes](../ANNEXES.md)

<a name="page-compatibilite"></a>

# Compatibilité

**Attuned Equipment v0.17.1 cible Minecraft Java 1.21 à 1.21.11.** Une seule archive contient les adaptations nécessaires aux différents formats de la série. Le pack de ressources doit également être activé chez chaque joueur.

La compatibilité indiquée ici distingue la cible annoncée par les fichiers, les adaptations effectivement présentes et les vérifications réalisées pour ce wiki. L’analyse de v0.17.1 est statique : aucun démarrage de serveur ou de client Minecraft n’a été effectué pendant cet audit.

<a name="page-compatibilite-versions-et-overlays"></a>

## Versions et overlays

Un overlay est un dossier de remplacement que Minecraft choisit selon son format de pack. Pour cette archive, le jeu combine la base avec **l’overlay correspondant à sa version**, sans additionner les six overlays successifs.

| Minecraft Java | Format du datapack | Fichiers du datapack utilisés | Format du RP | Modèles d’objets du RP |
| --- | ---: | --- | ---: | --- |
| 1.21, 1.21.1 | 48 | Base | 34 | `overlay_legacy` |
| 1.21.2, 1.21.3 | 57 | Base + `overlay_57` | 42 | `overlay_legacy` |
| 1.21.4 | 61 | Base + `overlay_61` | 46 | Définitions modernes |
| 1.21.5 | 71 | Base + `overlay_71` | 55 | Définitions modernes |
| 1.21.6 | 80 | Base + `overlay_80` | 63 | Définitions modernes |
| 1.21.7, 1.21.8 | 81 | Base + `overlay_80` | 64 | Définitions modernes |
| 1.21.9, 1.21.10 | 88.0 | Base + `overlay_88` | 69.0 | Définitions modernes |
| 1.21.11 | 94.1 | Base + `overlay_94` | 75.0 | Définitions modernes |

**Sources du pack :** `pack.mcmeta`, lignes 3–13 et 18–86 ; `resources.zip/pack.mcmeta`, lignes 3–28. Les numéros de formats de référence viennent des notes officielles de [Java 1.21](https://www.minecraft.net/en-us/article/minecraft-java-edition-1-21), [1.21.2](https://www.minecraft.net/en-us/article/minecraft-java-edition-1-21-2), [1.21.4](https://www.minecraft.net/en-us/article/minecraft-java-edition-1-21-4), [1.21.5](https://www.minecraft.net/en-us/article/minecraft-java-edition-1-21-5), [1.21.6](https://www.minecraft.net/en-us/article/minecraft-java-edition-1-21-6), [1.21.7](https://www.minecraft.net/en-us/article/minecraft-java-edition-1-21-7), [1.21.9](https://www.minecraft.net/en-us/article/minecraft-java-edition-1-21-9) et [1.21.11](https://www.minecraft.net/en-us/article/minecraft-java-edition-1-21-11). Les versions correctives regroupées conservent les familles de formats précédentes.

Les numéros de formats sont différents pour un datapack et pour un RP : le format `48` du datapack et le format `34` du RP correspondent tous deux à Java 1.21. Cette différence est normale.

<a name="page-compatibilite-différences-de-fonctionnement-selon-la-version"></a>

## Différences de fonctionnement selon la version

| Fonction | Avant la version concernée | À partir de la version concernée |
| --- | --- | --- |
| Menus de forge et de table d’enchantement | Jusqu’à 1.21.5 : actions cliquables dans le chat | 1.21.6 : fenêtres de dialogue natives |
| Apparence des objets personnalisés | Jusqu’à 1.21.3 : nombres `custom_model_data` et modèles de l’overlay ancien | 1.21.4 : composant `minecraft:item_model` et définitions d’objets modernes |
| Palier cuivre des épées et outils | Jusqu’à 1.21.8 : objet vanilla en fer portant l’identité Attuned du cuivre | 1.21.9 : objets vanilla en cuivre |
| Enchantements `weapon_familiarity` et `armor_familiarity` | Jusqu’à 1.21.10 : réduction d’usure de 10 % par niveau dans ces définitions | 1.21.11 : réparation conditionnelle lors d’un combat dans ces définitions |
| Impulsion des enchantements de tir concernés | Jusqu’à 1.21.10 : fonction de compatibilité multipliant les composantes de vitesse par environ 1,1 par déclenchement | 1.21.11 : impulsion native `minecraft:apply_impulse`, avec une formule propre à chaque enchantement |
| Maîtrise de l’enchantement vanilla Lunge | Jusqu’à 1.21.10 : refus explicite, sans prélèvement de lapis ni d’XP | 1.21.11 : branche d’application disponible sous ses conditions |

Sur les anciennes versions, le palier cuivre reste identifié comme cuivre pour l’histoire et les reforges Attuned, mais les propriétés vanilla de l’épée ou de l’outil de base sont celles du fer. Il ne faut donc pas présenter ses statistiques comme celles du cuivre vanilla récent.

Les menus dans le chat ont une session temporaire. Jusqu’à 1.21.5, fermer si nécessaire l’écran vanilla, ouvrir le chat avec **T**, puis cliquer rapidement sur l’action proposée. Les dialogues introduits par Minecraft 1.21.6 permettent ensuite une interface native. La documentation officielle décrit cet ajout dans les [notes de Java 1.21.6](https://www.minecraft.net/en-us/article/minecraft-java-edition-1-21-6).

**Exemples vérifiables dans le DP :**

- `data/attuned/function/forge/open.mcfunction`, lignes 33–48, et sa version dans `overlay_80` : actions du chat remplacées par `dialog show`.
- `data/attuned/function/forge/equipment/sword_stone_to_copper.mcfunction`, ligne 2, et sa version dans `overlay_88` : `iron_sword` remplacé par `copper_sword`.
- `data/attuned/enchantment/weapon_familiarity.json`, lignes 23–31, et sa version dans `overlay_94`, lignes 23–55 : mécanismes d’entretien différents.
- `data/attuned/function/compat/projectile_boost.mcfunction`, lignes 1–6, et `overlay_94/data/attuned/enchantment/forged_shot.json`, à partir de la ligne 42 : adaptation de l’impulsion.
- `data/attuned/function/enchanting/mastery/apply/minecraft_lunge.mcfunction`, lignes 1–2 : message de version requise suivi d’un arrêt immédiat.

<a name="page-compatibilite-contenu-présent-mais-non-actif-en-121x"></a>

## Contenu présent mais non actif en 1.21.x

L’archive contient **36 définitions de commerce** dans `data/attuned/villager_trade/` et **7 tags** dans `data/minecraft/tags/villager_trade/`. Minecraft a introduit les commerces pilotés par le dossier `villager_trade` dans **Java 26.1**, après toute la série 1.21.x. Ces fichiers ne rendent donc pas les offres correspondantes disponibles dans la cible de ce pack. Les [notes officielles de Java 26.1](https://www.minecraft.net/en-us/article/minecraft-java-edition-26-1), section « Data-driven Villager Trades », décrivent cette introduction.

Cette présence ne signifie pas que l’archive v0.17.1 est compatible avec Java 26.1. Ses métadonnées et ses adaptations visent Java 1.21.x. Un portage vers 26.x doit être traité comme une autre édition.

De même, les **58 fichiers de dialogue** se trouvent dans la base de l’archive. Leur simple présence ne rend pas le registre des dialogues disponible avant Java 1.21.6 ; les fonctions de compatibilité utilisent alors le chat.

<a name="page-compatibilite-association-avec-dautres-datapacks"></a>

## Association avec d’autres datapacks

Attuned Equipment remplace quatre tables vanilla pour ajouter des reliques :

| Identifiant de table | Structure |
| --- | --- |
| `minecraft:chests/end_city_treasure` | Cité de l’End |
| `minecraft:chests/ancient_city` | Cité antique |
| `minecraft:chests/bastion_treasure` | Salle au trésor d’un bastion |
| `minecraft:chests/desert_pyramid` | Pyramide du désert |

Un autre datapack qui fournit une de ces mêmes tables peut remplacer son contenu selon l’ordre de chargement. Les deux changements doivent être fusionnés si l’on veut conserver leurs effets ensemble. Il ne faut pas supposer que les pools de deux fichiers portant le même identifiant sont automatiquement réunis.

**Sources :** les quatre fichiers de `data/minecraft/loot_table/chests/` et leurs adaptations dans les overlays ; `INSTALLATION_v0.17.1.txt`, lignes 15–16.

Les conflits visuels du RP concernent notamment l’enclume, la table d’enchantement et les modèles vanilla de l’overlay ancien. Ils sont détaillés dans [Pack de ressources](Resource-pack.md).

<a name="page-compatibilite-portée-des-vérifications"></a>

## Portée des vérifications

L’audit de cette archive confirme les points suivants :

- Les **2 367 JSON du datapack**, les **101 JSON du RP** et les deux `pack.mcmeta` peuvent être analysés comme JSON strict, sans clé dupliquée détectée.
- Les références locales reconnues dans les sept compositions base/overlay sont présentes ; cela couvre notamment les appels de fonctions, les modificateurs d’objets, les prédicats, les tables de butin et les tags.
- Les deux fonctions de chargement et les deux fonctions de tick visées par les tags Minecraft existent.
- Toutes les références locales de modèles et de textures du RP examinées aboutissent à des fichiers présents ; les 43 PNG peuvent être décodés.
- Les dictionnaires français et anglais couvrent les clés Attuned `translate` retrouvées dans le DP.

Un JSON valide peut cependant employer une propriété inconnue d’une version donnée. Un fichier présent peut appartenir à un registre que cette version ne charge pas. Ces contrôles ne certifient donc pas les codecs Minecraft, le gameplay, le rendu ou les performances en serveur.

<a name="page-compatibilite-ancien-rapport-de-tests-inclus"></a>

### Ancien rapport de tests inclus

`VALIDATION.md` porte encore le titre **« Vérification Attuned Equipment v0.16.1 »** et mentionne **1 860 assertions** sur douze versions. `LISEZ-MOI_1.21.txt` est également titré v0.16.1 et recommande l’ancien RP. En revanche, `INSTALLATION_v0.17.1.txt` et les deux `pack.mcmeta` indiquent v0.17.1.

Le rapport historique n’est pas une preuve de tests exécutés sur le ZIP v0.17.1 analysé ici. La présence du même nombre de références de modèles ne change pas ce constat. Pour publier une affirmation « testé sur douze versions », il faut un nouveau rapport associé à cette archive précise.

Les notes de l’archive visent Java et ne revendiquent pas Bedrock, les snapshots ni les préversions. Aucun essai sur Paper, Spigot, Fabric, NeoForge ou d’autres environnements modifiés n’a été effectué dans cet audit. Consulter [Audit technique](Audit-technique.md) pour les limites et contrôles de publication proposés.
