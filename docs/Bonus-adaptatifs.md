[Accueil du wiki](Home.md) · [Sommaire du dépôt](../README.md) · [Annexes](../ANNEXES.md)

<a name="page-bonus-adaptatifs"></a>

# Bonus d'histoire adaptatifs

À l'enclume, le bonus n'est pas tiré au hasard. Le datapack examine l'histoire de l'objet, applique des priorités dans un ordre précis, puis choisit un bonus encore non marqué comme appliqué. Si aucune priorité d'activité ne convient, il utilise un ordre de repli.

Les seuils de cette page servent donc à **influencer le choix**, et ne sont pas tous des conditions obligatoires d'acquisition. Le palier d'évolution, le potentiel, le matériau, l'histoire globale et le paiement restent contrôlés séparément. Voir [Progression et histoire](Progression-et-histoire.md) et [Enclume](Enclume.md).

Cette page reproduit les règles de sélection des fonctions `data/attuned/function/station/select/*.mcfunction` de la **v0.17.1**, sans simulation en jeu.

<a name="page-bonus-adaptatifs-règles-communes"></a>

## Règles communes

Dans chaque liste, la première règle satisfaite dont le bonus est encore disponible gagne. Les tests suivants ne sont plus utilisés après le choix. Un bonus déjà marqué comme appliqué est ignoré.

Les bonus nommés I ou II ajoutent généralement **un niveau** via `minecraft:set_enchantments` avec `add:true`. « Seconde Endurance », par exemple, est la seconde attribution de ce bonus ; elle produit normalement Endurance II après Endurance I. Sur un objet déjà enchanté autrement, le niveau final peut différer de l'intitulé descriptif. Les marqueurs d'histoire, et non seulement les niveaux d'enchantement présents, déterminent si le bonus a déjà été réclamé.

**Sources :** `data/attuned/function/station/select/*.mcfunction` ; `function/station/apply_bonus.mcfunction` ; `item_modifier/anvil/history/*.json`.

<a name="page-bonus-adaptatifs-épée"></a>

## Épée

| Priorité | Comportement enregistré | Bonus choisi |
| ---: | --- | --- |
| 1 | Au moins 3 éliminations dans le Nether | Lame infernale |
| 2 | Au moins 5 coups infligés à faible santé | Siphon |
| 3 | Au moins 8 coups en sprint | Impact |
| 4 | Au moins 5 éliminations | Exécution |
| 5 | Au moins 20 coups infligés | Entrave |

**Repli :** Impact → Exécution → Siphon → Lame infernale → Entrave.

**Source :** `data/attuned/function/station/select/sword.mcfunction`, lignes 2–21.

<a name="page-bonus-adaptatifs-arc"></a>

## Arc

| Priorité | Comportement enregistré | Bonus choisi |
| ---: | --- | --- |
| 1 | Au moins 2 éliminations lointaines | Longue portée |
| 2 | Au moins 3 éliminations dans le Nether | Flamme |
| 3 | Au moins 8 éliminations | Puissance |
| 4 | Au moins 2 éliminations à faible santé | Frappe |

**Repli :** Main sûre → Puissance → Frappe → Longue portée → Flamme.

Une élimination lointaine correspond à au moins **24 blocs de distance** dans l'avancement associé. Le code attribue l'élimination à l'arme suivie en main principale au moment où l'événement est traité.

**Sources :** `data/attuned/function/station/select/bow.mcfunction`, lignes 2–20 ; `advancement/history/long_kill.json`, lignes 4–19 ; `function/history/event/long_kill.mcfunction`, lignes 2–4.

<a name="page-bonus-adaptatifs-arbalète"></a>

## Arbalète

| Priorité | Comportement enregistré | Bonus choisi |
| ---: | --- | --- |
| 1 | Au moins 2 éliminations lointaines | Perforation renforcée |
| 2 | Au moins 6 éliminations | Siège |
| 3 | Au moins 20 éliminations et premier Siège déjà appliqué | Second Siège |

**Repli :** Mécanisme rapide → second Mécanisme rapide si le premier est déjà appliqué → Perforation renforcée → Siège → second Siège → second Mécanisme rapide.

**Source :** `data/attuned/function/station/select/crossbow.mcfunction`, lignes 2–16.

<a name="page-bonus-adaptatifs-pioche"></a>

## Pioche

On note `M` le nombre de minerais et `R` le nombre de roches enregistrés.

| Priorité | Comportement enregistré | Bonus choisi |
| ---: | --- | --- |
| 1 | `M ≥ 5` et `8 × M ≥ R` | Allonge |
| 2 | `R ≥ 20` et `R > 8 × M` | Excavation |
| 3 | `R ≥ 80` et première Excavation déjà appliquée | Seconde Excavation |

**Repli :** Endurance → seconde Endurance si la première est appliquée → Excavation → Allonge → seconde Excavation → seconde Endurance.

**Source :** `data/attuned/function/station/select/pickaxe.mcfunction`, lignes 2–17.

<a name="page-bonus-adaptatifs-hache"></a>

## Hache

On note `B` le nombre de bûches et `C` le nombre de coups infligés.

| Priorité | Comportement enregistré | Bonus choisi |
| ---: | --- | --- |
| 1 | `B ≥ 10` et `B ≥ 2 × C` | Bûcheron |
| 2 | `B ≥ 50` et premier Bûcheron déjà appliqué | Second Bûcheron |
| 3 | `C ≥ 8` et `C ≥ B` | Impact |
| 4 | `C ≥ 30` et premier Impact déjà appliqué | Second Impact |

**Repli :** Endurance → Bûcheron → Impact → second Bûcheron → second Impact.

**Source :** `data/attuned/function/station/select/axe.mcfunction`, lignes 2–17.

<a name="page-bonus-adaptatifs-pelle"></a>

## Pelle

| Priorité | Comportement enregistré | Bonus choisi |
| ---: | --- | --- |
| 1 | Au moins 10 blocs de sable enregistrés | Excavation |
| 2 | Au moins 60 blocs de sable et première Excavation appliquée | Seconde Excavation |
| 3 | Au moins 8 blocs de neige enregistrés | Allonge |

**Repli :** Endurance → seconde Endurance si la première est appliquée → Excavation → Allonge → seconde Excavation → seconde Endurance.

Le terrain général est lu par la fonction mais n'ajoute pas de règle de priorité distincte dans ce sélecteur.

**Source :** `data/attuned/function/station/select/shovel.mcfunction`, lignes 2–16.

<a name="page-bonus-adaptatifs-houe"></a>

## Houe

On note `C` le nombre de cultures et `U` le nombre d'utilisations enregistrées.

| Priorité | Comportement enregistré | Bonus choisi |
| ---: | --- | --- |
| 1 | `C ≥ 10` | Moisson |
| 2 | `C ≥ 60` et première Moisson déjà appliquée | Seconde Moisson |
| 3 | `U ≥ 25` et `U > 2 × C` | Allonge |

**Repli :** Endurance → seconde Endurance si la première est appliquée → Moisson → Allonge → seconde Moisson → seconde Endurance.

**Source :** `data/attuned/function/station/select/hoe.mcfunction`, lignes 2–17.

<a name="page-bonus-adaptatifs-casque"></a>

## Casque

Un segment de déplacement représente 25 blocs comptés par la statistique correspondante.

| Priorité | Comportement enregistré | Bonus choisi |
| ---: | --- | --- |
| 1 | Au moins 2 segments de nage | Souffle profond |
| 2 | Au moins 3 projectiles subis | Vigilance |
| 3 | Au moins 1 segment de nage | Vision abyssale |
| 4 | Au moins 3 coups subis en danger | Esprit d'acier |
| 5 | Au moins 12 coups subis | Concentration |
| 6 | Au moins 5 coups subis dans le Nether | Seconde Vigilance |

**Repli :** Souffle profond → Vigilance → Vision abyssale → Esprit d'acier → Concentration → seconde Vigilance.

**Source :** `data/attuned/function/station/select/helmet.mcfunction`, lignes 2–23.

<a name="page-bonus-adaptatifs-plastron"></a>

## Plastron

| Priorité | Comportement enregistré | Bonus choisi |
| ---: | --- | --- |
| 1 | Au moins 3 coups subis en danger | Second souffle |
| 2 | Au moins 2 segments de nage | Garde abyssale |
| 3 | Au moins 12 coups subis | Carapace |
| 4 | Au moins 3 événements de feu | Garde ardente |
| 5 | Au moins 2 explosions | Ancrage explosif |
| 6 | Au moins 5 coups subis dans le Nether | Cœur gardé |

**Repli :** Second souffle → Garde abyssale → Carapace → Garde ardente → Ancrage explosif → Cœur gardé.

**Source :** `data/attuned/function/station/select/chestplate.mcfunction`, lignes 2–25.

<a name="page-bonus-adaptatifs-jambières"></a>

## Jambières

| Priorité | Comportement enregistré | Bonus choisi |
| ---: | --- | --- |
| 1 | Au moins 2 segments de déplacement accroupi | Pas d'ombre |
| 2 | Au moins 3 segments de sprint | Élan |
| 3 | Au moins 10 coups subis | Stabilité |
| 4 | Au moins 5 segments de marche | Pionnier |
| 5 | Au moins 8 segments de sprint | Agilité |
| 6 | Au moins 4 coups subis en danger | Second Pas d'ombre |

**Repli :** Pas d'ombre → Élan → Stabilité → Pionnier → Agilité → second Pas d'ombre.

**Source :** `data/attuned/function/station/select/leggings.mcfunction`, lignes 2–23.

<a name="page-bonus-adaptatifs-bottes"></a>

## Bottes

| Priorité | Comportement enregistré | Bonus choisi |
| ---: | --- | --- |
| 1 | Au moins 2 événements de chute | Pas léger |
| 2 | Au moins 4 événements de chute | Pied sûr |
| 3 | Au moins 4 segments de marche | Grande foulée |
| 4 | Au moins 8 segments de marche | Marcheur |
| 5 | Au moins 4 segments de sprint | Coureur |
| 6 | Au moins 3 événements de feu | Pas de braise |

**Repli :** Pas léger → Pied sûr → Grande foulée → Marcheur → Coureur → Pas de braise.

Les quatre types d'armure ont chacun **six possibilités de bonus**, mais au plus **cinq paliers d'histoire**, et parfois moins selon leur potentiel. Une seule lignée neuve ne reçoit donc pas nécessairement les six possibilités par sa seule progression à la station. L'ordre de ses activités peut changer laquelle reste absente.

**Source :** `data/attuned/function/station/select/boots.mcfunction`, lignes 2–21 ; `function/station/evaluate.mcfunction`, lignes 25–42.

<a name="page-bonus-adaptatifs-bouclier--ordre-fixe"></a>

## Bouclier : ordre fixe

Le bouclier constitue l'exception : son bonus dépend directement du palier choisi.

| Palier | Bonus |
| --- | --- |
| I | Trempe défensive |
| II | Garde vive |
| III | Rempart vivant |
| IV | Appel du Bastion |

Les exigences de blocage, de faible santé, de matériau et de lignée se trouvent dans [Armures et boucliers](Armures-et-boucliers.md).

**Source :** `data/attuned/function/station/select/shield.mcfunction`, lignes 1–6.
