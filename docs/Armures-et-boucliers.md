[Accueil du wiki](Home.md) · [Sommaire du dépôt](../README.md) · [Annexes](../ANNEXES.md)

<a name="page-armures-et-boucliers"></a>

# Armures et boucliers

Les protections possèdent une histoire indépendante de celle de l'arme du joueur. Une armure progresse grâce aux événements de combat et à certains déplacements ; le bouclier progresse grâce aux blocages comptabilisés.

Cette documentation repose sur le code de la **v0.17.1**. Les seuils et les appels sont vérifiés dans les fichiers, sans essai de combat en jeu.

<a name="page-armures-et-boucliers-armures--commencer-le-suivi"></a>

## Armures : commencer le suivi

Portez les pièces à suivre dans leurs emplacements normaux. Une routine exécutée toutes les cinq ticks initialise casque, plastron, jambières et bottes reconnus, puis leur affecte leur matériau et leur potentiel. Un objet en armure qui reste seulement dans l'inventaire n'est pas initialisé par cette routine.

Les matériaux pris en charge sont cuir, mailles, fer, or, diamant et netherite, ainsi que la carapace de tortue pour le casque. Le cuivre est ajouté pour les versions Minecraft concernées.

**Sources du ZIP :** `data/attuned/function/maintenance/armor_5t.mcfunction`, lignes 1–2 ; `function/armor/scan.mcfunction`, lignes 1–14 ; `function/armor/material/{head,chest,legs,feet}.mcfunction` ; `data/attuned/tags/item/{helmets,chestplates,leggings,boots}.json`.

<a name="page-armures-et-boucliers-gagner-de-lexpérience-darmure"></a>

## Gagner de l'expérience d'armure

| Action traitée | Pièces recevant l'expérience | Gain |
| --- | --- | ---: |
| Événement de joueur blessé | Toutes les pièces suivies portées | 5 XP d'armure par pièce |
| Marcher 25 blocs | Jambières et bottes | 1 XP par pièce |
| Sprinter 25 blocs | Jambières et bottes | 1 XP par pièce |
| Avancer accroupi sur 25 blocs | Jambières | 1 XP |
| Nager sur 25 blocs | Casque et plastron | 1 XP par pièce |

Les distances reposent sur les statistiques de déplacement Minecraft et sont accumulées en segments de **2 500 centimètres**. Il s'agit d'expérience d'objet, indépendante de la barre d'XP du joueur.

L'événement général incrémente aussi le nombre de coups subis. S'il a lieu dans le Nether, un compteur spécialisé augmente. Les coups « en danger » d'armure sont comptés lorsque la santé, lue à l'échelle entière, est au plus 8 ; ce test n'est pas celui des armes et boucliers à 10 points.

**Sources du ZIP :** `data/attuned/function/armor/event/hurt.mcfunction`, lignes 1–23 ; `function/armor/movement.mcfunction`, lignes 1–20 ; `function/armor/movement/{walk,sprint,crouch,swim}.mcfunction` ; `function/load.mcfunction`, ligne 292.

<a name="page-armures-et-boucliers-activités-spécialisées-de-larmure"></a>

## Activités spécialisées de l'armure

| Événement | Compteur spécialisé enregistré |
| --- | --- |
| Projectile reçu | Projectiles du casque |
| Dégât de feu | Feu du plastron et des bottes |
| Explosion | Explosions du plastron |
| Chute | Chutes des bottes |

Ces compteurs influencent la sélection du bonus d'histoire à l'enclume. Par exemple, la nage favorise Souffle profond et Vision abyssale sur un casque ; les chutes favorisent Pas léger et Pied sûr sur les bottes. Le code peut aussi sélectionner un bonus de repli si aucun comportement prioritaire n'est rempli. Voir [Bonus adaptatifs](Bonus-adaptatifs.md).

**Sources du ZIP :** `data/attuned/function/armor/event/{projectile,fire,explosion,fall}.mcfunction` ; `function/station/select/{helmet,chestplate,leggings,boots}.mcfunction`.

<a name="page-armures-et-boucliers-paliers-et-limites-des-armures"></a>

## Paliers et limites des armures

Les paliers I à V demandent **25, 100, 250, 500 et 1 000 XP d'armure**. Chaque palier est payé à l'enclume : **3 lapis-lazuli**, plus **3 niveaux du joueur** aux paliers I et II, puis **4 niveaux** aux paliers III à V.

Le potentiel d'origine est II pour cuir, mailles, or, tortue et netherite neuve ; III pour diamant neuf ; V pour fer et cuivre. Le palier V exige néanmoins un matériau netherite. Porter une pièce diamant suivie transformée en netherite synchronise son matériau sans supprimer son histoire ou son potentiel.

La chaîne de reforge d'armure cuivre → fer → diamant existe dans les fichiers mais n'est plus raccordée à la nouvelle station. Pour une nouvelle lignée de fer à potentiel V, l'accès normal à la transformation diamant reste donc une limite de cette version. Le menu générique d'outils peut même être proposé à une armure et prélever des matériaux sans exécuter de transformation adaptée. Consultez [Forge](Forge.md) avant toute tentative.

**Sources du ZIP :** `data/attuned/function/station/check_standard.mcfunction`, lignes 2–9 ; `function/station/cost.mcfunction`, lignes 79–126 ; `item_modifier/init/armor/*.json` ; `function/armor/sync_netherite.mcfunction`, lignes 2–9 ; `item_modifier/evolution/armor/sync_netherite.json` ; `function/anvil/process.mcfunction`, lignes 1–2 et 66 ; `function/forge/open.mcfunction`, lignes 61–63.

<a name="page-armures-et-boucliers-boucliers-disponibles"></a>

## Boucliers disponibles

| Bouclier | Durabilité maximale enregistrée | Potentiel à la fabrication directe | Fabrication |
| --- | ---: | --- | --- |
| Fer | 600 | IV | 6 lingots de fer et 1 planche |
| Diamant | 850 | III | 6 diamants et 1 lingot de fer |
| Netherite | 1 150 | Hérite des données du bouclier utilisé | Amélioration à la table de forge |

Les recettes de fer et de diamant utilisent la même forme : trois objets sur la première ligne, trois sur la deuxième et le matériau principal au centre de la troisième. Le centre de la première ligne reçoit la planche pour le fer, ou le lingot de fer pour le diamant.

| Recette fer | Colonne 1 | Colonne 2 | Colonne 3 |
| --- | --- | --- | --- |
| Haut | Lingot de fer | Planche | Lingot de fer |
| Milieu | Lingot de fer | Lingot de fer | Lingot de fer |
| Bas | Vide | Lingot de fer | Vide |

| Recette diamant | Colonne 1 | Colonne 2 | Colonne 3 |
| --- | --- | --- | --- |
| Haut | Diamant | Lingot de fer | Diamant |
| Milieu | Diamant | Diamant | Diamant |
| Bas | Vide | Diamant | Vide |

Un bouclier vanilla peut être initialisé comme ancienne forme de bois. Les fonctions de migration appliquées lors d'un blocage transforment les formes bois/cuivre en fer et leur attribuent un potentiel IV. Les anciens fichiers de boucliers en cuivre ne doivent donc pas être présentés comme une filière de fabrication supplémentaire stable.

**Sources du ZIP :** `data/attuned/recipe/shield/{iron,diamond,netherite_upgrade}.json` ; `item_modifier/init/shield.json` ; `item_modifier/material/{shield_iron,shield_diamond,shield_netherite_sync}.json` ; `function/shield/migrate_legacy_{mainhand,offhand}.mcfunction`.

<a name="page-armures-et-boucliers-les-quatre-évolutions-de-garde"></a>

## Les quatre évolutions de garde

| Palier | Blocages totaux | Blocages à faible santé | Autres conditions | Bonus d'histoire | Coût |
| --- | ---: | ---: | --- | --- | --- |
| I | 100 | Aucun minimum | Potentiel et ordre des paliers respectés | Trempe défensive | 1 bloc de lapis + 3 niveaux |
| II | 250 | 20 | Potentiel et ordre des paliers respectés | Garde vive | 1 bloc de lapis + 3 niveaux |
| III | 500 | Aucun nouveau minimum explicite | Matériau diamant ou netherite | Rempart vivant | 1 bloc de lapis + 4 niveaux |
| IV | 1 000 | 75 | Netherite, potentiel IV et marqueur de reforge diamant | Appel du Bastion | 1 bloc de lapis + 4 niveaux |

Les totaux sont cumulatifs. Les blocages à faible santé sont enregistrés lorsque la santé du joueur est au plus **10 points** selon la lecture du code, soit 5 cœurs de base. Le potentiel III d'un bouclier de diamant neuf ne suffit pas au palier IV.

Le parcours complet attendu est donc : **bouclier de fer à potentiel IV**, paliers I et II, reforge diamant pour 3 diamants, palier III, transformation netherite avec modèle et lingot, puis palier IV lorsque les compteurs sont atteints. La recette de netherite accepte techniquement tous les boucliers vanilla ; sauter la reforge diamant ne crée pas le marqueur de lignée exigé au palier IV.

**Sources du ZIP :** `data/attuned/function/station/check_shield.mcfunction`, lignes 1–17 ; `function/station/select/shield.mcfunction`, lignes 1–6 ; `function/station/cost.mcfunction`, lignes 71–78 ; `function/forge/shield_to_diamond.mcfunction`, lignes 1–10 ; `function/history/shield_mainhand.mcfunction`, lignes 8–10 ; `recipe/shield/netherite_upgrade.json`.

<a name="page-armures-et-boucliers-ce-que-compte-un-blocage"></a>

## Ce que compte un blocage

Le datapack surveille la hausse de la statistique `damage_blocked_by_shield`, puis ajoute **un blocage par traitement** à l'objet. Ce n'est donc pas une copie du nombre de points de dégâts absorbés. Si plusieurs augmentations arrivent avant le traitement, elles ne donnent pas nécessairement autant d'unités d'histoire.

Un bouclier suivi en main secondaire est prioritaire sur celui en main principale. Les compteurs distinguent la main utilisée, les blocages dans le Nether et ceux à faible santé. Les effets de garde sont ensuite appelés après ce traitement.

**Sources du ZIP :** `data/attuned/function/tick.mcfunction`, ligne 45 ; `function/history/increment_shield_blocks.mcfunction`, lignes 1–3 ; `function/history/shield_{mainhand,offhand}.mcfunction`, lignes 1–17.

<a name="page-armures-et-boucliers-garde-vive-rempart-vivant-et-appel-du-bastion"></a>

## Garde vive, Rempart vivant et Appel du Bastion

**Garde vive** donne Vitesse I pendant deux secondes après un blocage compté. **Rempart vivant** donne Résistance I pendant deux secondes après un blocage compté. Les appels existent pour les deux mains.

**Appel du Bastion**, sur un bouclier en netherite à l'évolution IV, invoque deux golems de fer lors d'un blocage si le délai de récupération est écoulé. Le délai est de **400 ticks**, soit 20 secondes à cadence normale. Les gardiens ont une table de butin vide et sont supprimés lorsque leur âge atteint **600 ticks**, soit environ 30 secondes, par la routine de maintenance.

Le code gère les golems temporaires dans son contexte de dimension courant. La durée effective et la suppression dans le Nether ou l'End doivent être vérifiées en jeu ; il ne faut pas annoncer une durée garantie dans toutes les dimensions uniquement à partir de la constante de 600 ticks.

Trempe défensive, les maîtrises de bouclier et les autres enchantements défensifs ont leurs propres effets : consulter [Enchantements](Enchantements.md).

**Sources du ZIP :** `data/attuned/function/shield/effects_{mainhand,offhand}.mcfunction`, lignes 1–3 ; `function/shield/summon_bastion.mcfunction`, lignes 1–7 ; `function/tick.mcfunction`, ligne 15 ; `function/maintenance/slow_20t.mcfunction`, lignes 5–7.

<a name="page-armures-et-boucliers-familiarité-et-hauts-faits"></a>

## Familiarité et hauts faits

Le bouclier gagne ses quatre rangs de familiarité à **250, 500, 750 et 1 000 blocages**. L'armure utilise les mêmes valeurs sur son expérience. Ces rangs sont distincts des paliers payants.

Les protections peuvent aussi obtenir des récompenses de longue durée : **Gardien éprouvé à 2 500 blocages** pour le bouclier et **Armure endurcie à 2 000 événements de coups subis** pour chaque pièce. Les exploits de boss sont également mémorisés sur les pièces suivies portées au moment du déclenchement.

Voir [Progression et histoire](Progression-et-histoire.md) pour les réserves sur la réparation scriptée et [Hauts faits](Hauts-faits.md) pour les récompenses.

**Sources du ZIP :** `data/attuned/function/history/familiarity/check_shield_{mainhand,offhand}.mcfunction` ; `check_armor_*.mcfunction` ; `function/history/shield_mainhand.mcfunction`, ligne 13 ; `function/armor/add/*_hits.mcfunction`, ligne 7 ; `function/history/feat/*.mcfunction`, lignes 2–7.
