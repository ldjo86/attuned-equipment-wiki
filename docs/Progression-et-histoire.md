[Accueil du wiki](Home.md) · [Sommaire du dépôt](../README.md) · [Annexes](../ANNEXES.md)

<a name="page-progression-et-histoire"></a>

# Progression et histoire

Attuned conserve plusieurs progressions sur **chaque objet**. Les confondre peut faire croire qu'un palier est obtenu alors qu'il est seulement devenu disponible.

| Notion | Ce qu'elle représente | Comment elle change |
| --- | --- | --- |
| Matériau | Bois, pierre, cuivre, fer, diamant, netherite… | Fabrication ou reforge |
| Histoire | Utilisations, tirs, blocages, combats, déplacements… | Actions enregistrées pendant le jeu |
| Évolution | Palier effectivement forgé I à V, ou I à IV pour le bouclier | Validation payante à la station |
| Potentiel | Plafond de lignée inscrit sur l'objet | Initialisation et certaines migrations ; il suit généralement la reforge |
| Bonus d'histoire | Enchantement choisi à partir des activités de l'objet | Un bonus lors de la validation d'un palier |
| Familiarité | Quatre rangs d'expérience à long terme | Déblocage automatique aux seuils dédiés |
| Hauts faits | Métiers pratiqués longtemps, ennemis maîtrisés et boss vaincus | Récompenses séparées des paliers |

**Portée :** lecture statique de la v0.17.1, sans serveur Minecraft lancé pour validation.

<a name="page-progression-et-histoire-seuils-des-évolutions-ordinaires"></a>

## Seuils des évolutions ordinaires

Cette table concerne les épées, les quatre outils, les arcs, les arbalètes et les quatre pièces d'armure. Les boucliers suivent une table particulière.

| Évolution | Histoire totale requise | Niveaux d'XP du joueur consommés | Restriction de matériau pour épée/outils/arc/arbalète |
| --- | ---: | ---: | --- |
| I | 25 | 3 | Aucun filtre supplémentaire dans le contrôleur de station |
| II | 100 | 3 | Bois refusé |
| III | 250 | 4 | Bois, pierre et or refusés |
| IV | 500 | 4 | Bois, pierre, cuivre et or refusés |
| V | 1 000 | 4 | Netherite obligatoire |

L'unité est l'utilisation pour les épées et outils, le tir/utilisation pour les arcs et arbalètes, et le point d'expérience d'armure pour les protections. Les seuils sont **cumulatifs** : le palier III demande un total de 250, pas 250 actions supplémentaires après le palier II.

Pour les armures, le contrôleur n'applique pas les filtres de bois/pierre/cuivre de ce tableau ; le potentiel d'origine et la condition netherite du palier V restent déterminants. Pour tous les types, le palier doit être inférieur ou égal au potentiel de l'objet, ne pas avoir déjà été réclamé, et ne pas dépasser l'évolution actuelle + 1. Un objet portant une ancienne évolution peut récupérer des paliers d'histoire antérieurs encore non marqués comme réclamés.

Le lapis est une dépense supplémentaire qui dépend du **bonus proposé**, et non seulement du numéro du palier. Voir [Enclume](Enclume.md) et [Bonus adaptatifs](Bonus-adaptatifs.md).

**Sources du ZIP :** `data/attuned/function/station/evaluate.mcfunction`, lignes 25–75 ; `function/station/check_standard.mcfunction`, lignes 1–65 ; `function/station/claim.mcfunction`, lignes 4–12.

<a name="page-progression-et-histoire-ce-qui-se-passe-au-passage-dun-seuil"></a>

## Ce qui se passe au passage d'un seuil

Le seuil ouvre l'accès au palier. Il ne remplace pas la transaction de la station. Dans cette archive, les anciennes fonctions de rattrapage automatique contiennent surtout des commentaires ou une lecture d'évolution ; elles n'appellent plus leurs anciens fichiers `level_1` à `level_5`.

La station effectue successivement l'évolution, l'application du bonus, l'attribution du titre, le marquage du palier comme réclamé, puis le prélèvement du lapis. Elle remet ensuite l'objet au joueur et prélève les niveaux d'XP. L'histoire accumulée n'est pas consommée.

Chaque nouveau palier ajoute aussi la maîtrise de sa famille : maîtrise d'arme pour l'épée, maîtrise d'outil pour les outils, Tir forgé pour l'arc, maîtrise d'arbalète, maîtrise d'armure, ou maîtrise de bouclier. Le détail des effets se trouve dans [Enchantements](Enchantements.md).

**Sources du ZIP :** `data/attuned/function/history/catchup/apply.mcfunction`, lignes 7–27 ; `function/history/ranged/catchup.mcfunction`, lignes 21–39 ; `function/station/commit_item.mcfunction`, lignes 1–11 ; `item_modifier/station/evolve/*.json`.

<a name="page-progression-et-histoire-comment-lhistoire-est-attribuée"></a>

## Comment l'histoire est attribuée

Les compteurs principaux des armes et outils reposent sur les statistiques Minecraft d'utilisation. Le datapack détecte une hausse depuis le tick précédent et ajoute une unité à l'objet suivi présent en main principale. Le nombre peut donc différer du nombre de clics, du nombre de blocs obtenus ou du nombre total de projectiles créés par un enchantement.

Les sous-compteurs de métier utilisent les variations des statistiques de blocs minés. La pioche distingue notamment les minerais et certaines roches ; la hache les bûches ; la pelle le terrain, le sable et la neige ; la houe les cultures. Ces statistiques alimentent le choix du prochain bonus. Les fonctions d'activité consultent les variations du joueur et les attribuent à l'objet au moment où leur traitement est déclenché : ce n'est pas un journal complet identifiant physiquement chaque bloc détruit par chaque exemplaire.

Les éliminations à distance sont attribuées à l'arc ou à l'arbalète **tenu en main principale quand l'élimination est traitée**. Ranger son arc avant l'impact peut donc changer ce qui est enregistré. Une élimination lointaine exige une distance absolue d'au moins **24 blocs** dans l'avancement correspondant. Le code des coups et éliminations « en danger » pour armes et boucliers utilise une santé d'au plus **10 points**, soit 5 cœurs de santé standard ; l'armure utilise un autre test, décrit dans son chapitre.

**Sources du ZIP :** `data/attuned/function/tick.mcfunction`, lignes 10–45 ; `function/history/increment_uses.mcfunction`, lignes 1–7 ; `function/history/increment_shots.mcfunction`, lignes 1–8 ; `function/history/activity/*.mcfunction` ; `function/history/event/kill_projectile.mcfunction`, lignes 2–9 ; `advancement/history/long_kill.json`, lignes 4–19 ; `function/history/event/hurt_entity.mcfunction`, lignes 7–10 ; `function/history/shield_mainhand.mcfunction`, lignes 8–10.

<a name="page-progression-et-histoire-familiarité-i-à-iv"></a>

## Familiarité I à IV

La familiarité ne demande ni lapis ni niveaux du joueur. Elle est enregistrée automatiquement lorsque le compteur de l'objet atteint les valeurs suivantes.

| Rang | Compteur cumulé requis |
| --- | ---: |
| I | 250 |
| II | 500 |
| III | 750 |
| IV | 1 000 |

Le compteur utilisé est celui de la famille : utilisations, tirs, blocages ou expérience d'armure. Le potentiel d'évolution de l'objet ne constitue pas un plafond de familiarité dans les fonctions de détection.

<a name="page-progression-et-histoire-effets-selon-la-famille-et-la-version"></a>

### Effets selon la famille et la version

Pour la familiarité d'arme et d'armure, les versions anciennes de l'enchantement réduisent l'usure à **90 %, 80 %, 70 % et 60 %** de sa valeur, selon le rang. L'overlay de la 1.21.11 remplace ces effets par des chances de restauration de durabilité lors d'événements de combat : pour l'arme, **6/9/12/15 %**, avec une variation de **3/4/5/6 points** ; pour l'armure, **4/6/8/10 %**, avec **2/3/4/5 points**. Les conditions exactes sont décrites au catalogue des enchantements.

Pour les outils, les arcs/arbalètes et les boucliers, le datapack utilise des fonctions dédiées après une action déjà comptée. Elles vérifient que l'objet est endommagé et possède un rang de familiarité, puis tirent une chance de **6/9/12/15 %**. Les fichiers visent une variation de **3/4/5/6 points** rapportée à la durabilité du matériau.

**Point à vérifier avant d'annoncer une réparation fonctionnelle :** ces fonctions scriptées emploient `minecraft:set_damage` avec `add:true` et une fraction négative. Le signe et l'arrondi doivent être validés sur les versions Java ciblées. Le wiki ne présente donc pas ce mécanisme comme une réparation constatée en jeu. Les fonctions de combat de la 1.21.11 utilisent une autre opération, `minecraft:change_item_damage`, et doivent être distinguées de ce chemin scripté.

**Sources du ZIP :** `data/attuned/function/history/familiarity/check_mainhand.mcfunction`, lignes 3–60 ; `check_ranged.mcfunction`, lignes 3–24 ; `check_shield_mainhand.mcfunction`, lignes 3–12 ; `check_armor_helmet.mcfunction`, lignes 3–12 ; `data/attuned/predicate/familiarity/repair_1.json` à `repair_4.json` ; `function/history/familiarity/repair/{tool,ranged,shield_mainhand,shield_offhand}.mcfunction` ; `item_modifier/history/familiarity/repair/**` ; `data/attuned/enchantment/{weapon_familiarity,armor_familiarity}.json` ; `overlay_94/data/attuned/enchantment/{weapon_familiarity,armor_familiarity}.json`.

<a name="page-progression-et-histoire-voir-les-données-dun-objet"></a>

## Voir les données d'un objet

Les lignes de description affichent une partie de sa progression. Pour un contrôle par un administrateur, les fonctions `attuned:info` et `attuned:history/view` existent et lisent l'objet en main principale.

L'ancienne interface d'enclume proposait une consultation d'histoire via un déclencheur. La nouvelle station possède une icône « Histoire de l'objet », mais cette icône est descriptive (`action:0`) : elle n'appelle pas la fonction de consultation détaillée. Les commandes administratives et la nouvelle interface doivent être documentées séparément.

**Sources du ZIP :** `data/attuned/function/info.mcfunction`, lignes 1–4 ; `function/history/view.mcfunction`, lignes 2–15 ; `function/station/render_controls.mcfunction`, lignes 43–44 ; `function/station/request.mcfunction`, lignes 4–7.
