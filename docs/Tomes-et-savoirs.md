[Accueil du wiki](Home.md) · [Sommaire du dépôt](../README.md) · [Annexes](../ANNEXES.md)

<a name="page-tomes-et-savoirs"></a>

# Tomes et savoirs

Cette page distingue deux systèmes : les **livres de savoir**, rangés dans les bibliothèques sculptées pour enseigner un enchantement à la table, et les **tomes de progression**, consommés pour augmenter les caractéristiques du joueur.

<a name="page-tomes-et-savoirs-préparer-la-table"></a>

## Préparer la table

1. Placez une table d’enchantement.
2. Entourez-la de bibliothèques selon l’anneau habituel à deux blocs de distance : le pack examine les 16 emplacements du pourtour, au niveau de la table et un bloc plus haut, soit 32 positions possibles.
3. Laissez entre la table et chaque bibliothèque un bloc qui transmet la puissance d’enchantement. Le code utilise le tag Minecraft `enchantment_power_transmitter` pour ce contrôle.
4. Placez les livres enchantés utiles dans des **bibliothèques sculptées** présentes dans cet anneau.
5. Tenez l’équipement à enchanter en main principale, puis interagissez avec la table. Le menu s’ouvre dans le chat pour les anciennes variantes et dans un dialogue pour les variantes qui les prennent en charge.

Une bibliothèque normale apporte **1 puissance**. Une bibliothèque sculptée non vide apporte également **1 puissance**, même avec plusieurs livres. Une bibliothèque sculptée vide n’apporte rien. Le total est limité à **15**. Chaque enchantement présent dans les `stored_enchantments` d’un livre enchanté est reconnu comme un savoir disponible ; il n’est pas nécessaire que ce livre ait un nom Attuned particulier. Plusieurs enchantements sur un seul livre peuvent donc enseigner plusieurs savoirs.

La détection conserve la **présence du savoir**, pas le niveau exact du livre. Les livres restent dans la bibliothèque ; les coûts sont prélevés dans les ressources du joueur. La session de menu expire après 200 ticks, soit environ 10 secondes au rythme normal du jeu. Si elle expire, ouvrez à nouveau la table.

Sources : `data/attuned/advancement/interaction/use_enchanting_table.json`, lignes 4–20 ; `data/attuned/function/enchanting/open.mcfunction`, lignes 1–14 ; `scan/providers.mcfunction`, lignes 1–2049 ; `scan_table.mcfunction`, lignes 138–141 ; `process.mcfunction`, lignes 1–3. Les overlays 80, 88 et 94 remplacent l’ouverture du menu par un dialogue.

<a name="page-tomes-et-savoirs-les-trois-enchantements-classiques"></a>

## Les trois enchantements classiques

| Option | Puissance minimale | Lapis consommé | Niveaux XP consommés | Niveau interne du tirage Minecraft | Essais de bonus appris |
| --- | --- | --- | --- | --- | --- |
| Enchantement I | 1 | 1 lapis-lazuli | 1 | 5 | 5 |
| Enchantement II | 8 | 2 lapis-lazuli | 2 | 15 | 10 |
| Enchantement III | 15 | 3 lapis-lazuli | 3 | 30 | 18 |

Le niveau interne du tirage n’est pas le coût en XP : le troisième choix coûte bien **3 niveaux** dans le code. Les enchantements de départ viennent du groupe Minecraft `in_enchanting_table`. Après ce tirage, le pack essaie d’ajouter **au plus un** enchantement appris compatible de niveau I.

Le tirage du bonus se fait parmi 25 candidats : les 20 savoirs Attuned, Raccommodage, Furtivité rapide, Agilité des âmes, Rafale et Semelles givrantes. Un candidat non connu, incompatible ou déjà présent n’est pas appliqué. Le nombre d’essais ci-dessus n’est donc pas une chance fixe de recevoir un bonus. Si `k` des 25 candidats sont réellement admissibles et restent inchangés, la chance d’obtenir un bonus en `n` essais est `1 − (1 − k/25)^n`.

L’objet ne doit pas déjà porter le marqueur `table_enchanted`. Un objet déjà enchanté est refusé, sauf s’il porte le marqueur d’enchantement d’histoire reconnu par le pack. L’exception est donc liée aux données de l’objet, pas seulement à son nom ou à sa provenance.

Sources : `data/attuned/function/enchanting/classic/tier1.mcfunction`, `tier2.mcfunction` et `tier3.mcfunction`, lignes 1–25 ; `data/attuned/item_modifier/enchanting/classic/tier*.json`, lignes 3–9 ; `data/attuned/function/enchanting/bonus/classic1.mcfunction`, `classic2.mcfunction`, `classic3.mcfunction` et `bonus/candidate/1.mcfunction`, lignes 1–8. La migration/restauration de l’histoire utilise `classic/migrate_history_marker.mcfunction` et `classic/restore_history.mcfunction`.

<a name="page-tomes-et-savoirs-apprendre-les-20-savoirs-attuned"></a>

## Apprendre les 20 savoirs Attuned

Chaque achat du menu standard ajoute **un niveau**, jusqu’au plafond standard de la ligne. Le savoir doit être connu de la bibliothèque et l’objet doit être compatible. **Les quantités ci-dessous sont des blocs de lapis**, alors que les choix classiques et la Maîtrise utilisent des lapis-lazuli individuels.

| Savoir | Puissance minimale | Blocs de lapis par achat | Niveaux XP par achat | Plafond standard | Niveau donné par Maîtrise |
| --- | --- | --- | --- | --- | --- |
| Excavation | 8 | 1 | 4 | III | IV |
| Allonge | 10 | 2 | 5 | II | III |
| Endurance | 10 | 2 | 5 | III | IV |
| Bûcheron | 8 | 1 | 4 | III | IV |
| Moisson | 8 | 1 | 4 | II | III |
| Exécution | 12 | 2 | 6 | III | IV |
| Impact | 10 | 1 | 5 | II | III |
| Lame infernale | 12 | 2 | 6 | II | III |
| Siphon | 15 | 3 | 8 | II | III |
| Entrave | 12 | 2 | 6 | III | IV |
| Longue portée | 12 | 2 | 6 | I | I |
| Volée | 15 | 4 | 8 | I | I |
| Siège | 12 | 2 | 6 | III | IV |
| Mécanisme rapide | 12 | 2 | 6 | III | IV |
| Perforation renforcée | 10 | 1 | 5 | III | IV |
| Bastion | 10 | 1 | 5 | III | IV |
| Riposte | 15 | 3 | 8 | III | IV |
| Pas léger | 10 | 1 | 5 | III | IV |
| Garde abyssale | 10 | 1 | 5 | III | IV |
| Second souffle | 15 | 3 | 8 | II | III |

Sources : `data/attuned/function/enchanting/apply/<identifiant>.mcfunction` et `data/attuned/item_modifier/enchanting/<identifiant>.json`. Toutes les conditions et références sont regroupées dans [couts-savoirs-attuned.csv](../catalogues/couts-savoirs-attuned.csv).

<a name="page-tomes-et-savoirs-maîtrise--choisir-directement-lenchantement"></a>

## Maîtrise : choisir directement l’enchantement

La quatrième option exige **15 puissance**, le savoir correspondant, **1 lapis-lazuli et 5 niveaux XP**. Elle applique directement le niveau prévu par son modificateur ; il n’est pas nécessaire d’avoir acheté tous les niveaux standard. Elle refuse un enchantement déjà au niveau maîtrisé ou au-dessus. Lorsqu’il n’est pas encore présent, une tentative d’enchantement de niveau I vérifie d’abord que l’objet peut le recevoir.

La Maîtrise fait ensuite jusqu’à **40 essais** pour ajouter au plus **un** savoir rare compatible de niveau I. Elle ne garantit pas ce deuxième bonus. Le texte de menu parlant de « deux enchantements au total » doit se comprendre comme un choix et un bonus possibles : les autres enchantements déjà portés par l’objet ne sont pas explicitement effacés par les modificateurs de maîtrise.

Les cibles Attuned sont données dans le tableau précédent. Les cibles Minecraft sont les suivantes ; la valeur est celle que le code applique, et ne promet pas une amélioration supplémentaire lorsque le moteur plafonne déjà l’effet.

| Enchantement Minecraft (identifiant exact) | Niveau appliqué par Maîtrise |
| --- | --- |
| `minecraft:aqua_affinity` | I |
| `minecraft:bane_of_arthropods` | VI |
| `minecraft:binding_curse` | I |
| `minecraft:blast_protection` | V |
| `minecraft:breach` | V |
| `minecraft:channeling` | I |
| `minecraft:density` | VI |
| `minecraft:depth_strider` | V |
| `minecraft:efficiency` | VI |
| `minecraft:feather_falling` | V |
| `minecraft:fire_aspect` | III |
| `minecraft:fire_protection` | V |
| `minecraft:flame` | I |
| `minecraft:fortune` | V |
| `minecraft:frost_walker` | III |
| `minecraft:impaling` | VI |
| `minecraft:infinity` | I |
| `minecraft:knockback` | III |
| `minecraft:looting` | V |
| `minecraft:loyalty` | V |
| `minecraft:luck_of_the_sea` | V |
| `minecraft:lunge` — Java 1.21.11 | V |
| `minecraft:lure` | V |
| `minecraft:mending` | I |
| `minecraft:multishot` | I |
| `minecraft:piercing` | V |
| `minecraft:power` | VI |
| `minecraft:projectile_protection` | V |
| `minecraft:protection` | V |
| `minecraft:punch` | III |
| `minecraft:quick_charge` | V |
| `minecraft:respiration` | V |
| `minecraft:riptide` | V |
| `minecraft:sharpness` | VI |
| `minecraft:silk_touch` | I |
| `minecraft:smite` | VI |
| `minecraft:soul_speed` | V |
| `minecraft:sweeping_edge` | V |
| `minecraft:swift_sneak` | V |
| `minecraft:thorns` | V |
| `minecraft:unbreaking` | V |
| `minecraft:vanishing_curse` | I |
| `minecraft:wind_burst` | V |

Exemples : Tranchant (`sharpness`) et Puissance (`power`) passent à VI ; Fortune, Butin (`looting`), Solidité et Protection passent à V. Les enchantements à un seul niveau, comme Raccommodage, restent I. Les niveaux de Longue portée et Volée restent également I dans la Maîtrise de cette version.

Sources : `data/attuned/function/enchanting/mastery/apply/*.mcfunction` ; `data/attuned/item_modifier/enchanting/mastery/*.json` ; pour `lunge`, les remplacements correspondants d’`overlay_94`. Les cibles sont extraites des modificateurs, et non déduites d’une règle générale « maximum + 1 ».

<a name="page-tomes-et-savoirs-menu-des-enchantements-minecraft-appris"></a>

## Menu des enchantements Minecraft appris

Le menu « enchantements vanilla appris » choisit un niveau à partir de la puissance. Ses coûts diffèrent de ceux de la Maîtrise et varient selon l’enchantement. Le catalogue [couts-savoirs-vanilla.csv](../catalogues/couts-savoirs-vanilla.csv) liste chaque niveau sélectionnable, sa plage de puissance et les coûts exacts, avec les fonctions sources.

À titre d’exemple, Tranchant choisit I à puissance 1–4, II à 5–8, III à 9–11, IV à 12–14 et V à 15. Son niveau V coûte 6 blocs de lapis et 10 niveaux XP. L’application utilise la commande Minecraft d’enchantement et refuse les combinaisons ou niveaux que cette voie ne permet pas.

Sources : `data/attuned/function/enchanting/vanilla_apply/sharpness.mcfunction`, lignes 1–12 ; `sharpness_5.mcfunction`, lignes 1–13.

<a name="page-tomes-et-savoirs-tomes-de-progression-du-joueur"></a>

## Tomes de progression du joueur

Tenez le tome en **main principale** et utilisez une table d’enchantement. Les trois tomes possèdent des rangs indépendants, conservés dans les scores du joueur. Le chemin d’utilisation des tomes intervient avant le calcul de puissance de la table : il ne demande pas 15 bibliothèques.

| Tome | Bonus par rang | Rang maximal | Bonus total maximal |
| --- | --- | --- | --- |
| Vitalité | +2 points de vie, soit +1 cœur | V | +10 points de vie, soit +5 cœurs |
| Vigueur | +2 % de la vitesse de déplacement de base | III | +6 % de la base |
| Dextérité | +5 % de la vitesse de casse de base | III | +15 % de la base |

<a name="page-tomes-et-savoirs-coûts-des-rangs-de-vitalité"></a>

### Coûts des rangs de Vitalité

| Rang acheté | Tome demandé | Blocs de lapis | Niveaux XP |
| --- | --- | --- | --- |
| I | 1 | 2 | 5 |
| II | 1 | 4 | 8 |
| III | 1 | 6 | 12 |
| IV | 1 | 8 | 16 |
| V | 1 | 12 | 20 |

<a name="page-tomes-et-savoirs-coûts-des-rangs-de-vigueur-et-de-dextérité"></a>

### Coûts des rangs de Vigueur et de Dextérité

| Rang acheté | Tome demandé | Blocs de lapis | Niveaux XP |
| --- | --- | --- | --- |
| I | 1 | 2 | 5 |
| II | 1 | 4 | 10 |
| III | 1 | 6 | 15 |

**Particularité de v0.17.1 à connaître :** les fonctions testent les rangs à la suite. Avec assez de lapis et de niveaux, un seul clic peut donc lancer plusieurs achats successifs. La présence d’un tome supplémentaire n’est pas revérifiée avant chaque rang. C’est un comportement déduit directement des commandes, qui reste à confirmer en jeu ; les coûts ci-dessus sont ceux de chaque achat individuel. L’audit technique détaille ce point.

Les tomes peuvent provenir des bonus de butin listés dans [Reliques et butin](Reliques-et-butin.md). Les définitions de vente présentes dans l’archive utilisent un registre introduit après 1.21.x ; elles ne constituent pas une source de survie disponible sur les versions annoncées.

Sources : `data/attuned/function/tomes/use.mcfunction`, lignes 1–4 ; `tomes/vitality/try.mcfunction`, lignes 2–8 ; `tomes/vigor/try.mcfunction` et `tomes/dexterity/try.mcfunction`, lignes 2–6 ; toutes les fonctions `tomes/<type>/level_<rang>.mcfunction`, lignes 1–13 ; `tomes/reapply.mcfunction`, lignes 2–15. Les scores sont conservés lors de leur initialisation par `player_init.mcfunction`, lignes 44–47.
