[Accueil du wiki](Home.md) · [Sommaire du dépôt](../README.md) · [Annexes](../ANNEXES.md)

<a name="page-enchantements"></a>

# Enchantements

Attuned Equipment v0.17.1 contient **73 définitions d’enchantement personnalisées**. Ce total réunit les savoirs de bibliothèque, les traits acquis par l’histoire, les maîtrises, l’entretien, les exploits et quelques marqueurs techniques. Il ne correspond donc pas à 73 livres que l’on peut acheter ou sélectionner à la table.

La table propose **20 savoirs Attuned**. Leurs niveaux accessibles par le menu standard et par la Maîtrise figurent dans [Tomes et savoirs](Tomes-et-savoirs.md). Les autres entrées accompagnent les systèmes de progression documentés dans les pages du wiki consacrées à l’histoire et à la forge.

<a name="page-enchantements-lire-les-valeurs"></a>

## Lire les valeurs

`L` désigne le niveau de l’enchantement. Le « maximum défini » est la limite inscrite dans son fichier JSON ; un menu peut appliquer un plafond plus bas. Une valeur d’attribut comme `+0,2` reste une valeur d’attribut : elle ne signifie pas automatiquement « 20 % de dégâts en moins ». Les protections, multiplicateurs et limites du moteur peuvent modifier le résultat final. Les valeurs ci-dessous décrivent le code fourni, sans simuler un combat en jeu.

Les deux colonnes « équipement » et « emplacement actif » sont distinctes : un bonus peut accepter un bouclier, mais ne fonctionner que lorsque celui-ci est tenu. Les correspondances exactes de tags et les variantes par version sont conservées dans le catalogue JSON.

<a name="page-enchantements-savoirs-de-la-bibliothèque"></a>

## Savoirs de la bibliothèque

| Enchantement | Maximum défini | Équipement | Emplacement actif | Effet |
| --- | --- | --- | --- | --- |
| Excavation (`excavation`) | V | Outils de minage | Main principale | Efficacité de minage : +2 × L à l’attribut. |
| Allonge (`reach`) | V | Outils de minage | Main principale | Portée d’interaction avec les blocs : +0,5 × L bloc. |
| Endurance (`endurance`) | V | Objets à durabilité | Tous emplacements | Chaque point de dégât de durabilité a 10 % × L de chance d’être supprimé. |
| Bûcheron (`lumberjack`) | V | Haches | Main principale | Efficacité de minage : +2,5 × L à l’attribut. |
| Moisson (`harvest`) | V | Houes | Main principale | Efficacité de minage : +2 × L ; portée d’interaction avec les blocs : +0,5 × L bloc. |
| Exécution (`execution`) | V | Armes tranchantes | Main principale | Dégâts : +0,75 × L. |
| Impact (`impact`) | V | Armes tranchantes | Main principale | Recul infligé : +0,5 × L. |
| Lame infernale (`infernal_edge`) | V | Armes tranchantes | Main principale | Coup direct : met la victime en feu pendant 2 × L secondes. |
| Siphon (`siphon`) | V | Armes tranchantes | Main principale | Coup direct : 8 / 12 / 16 / 20 / 24 % de chance de recevoir Guérison instantanée I. |
| Entrave (`bind`) | V | Armes tranchantes | Main principale | Coup direct : Lenteur I, pendant 2 à (L + 1) secondes. |
| Longue portée (`longshot`) | V | Arcs | Main principale | Dégâts de flèches : +0,5 × L ; accélération du projectile (voir note de version). |
| Volée (`volley`) | V | Arcs | Main principale | Ajoute L + 1 projectiles ; ajoute 9 − L à la dispersion. |
| Siège (`siege`) | V | Arbalètes | Main principale | Dégâts de flèches : +0,75 × L. |
| Mécanisme rapide (`rapid_mechanism`) | V | Arbalètes | Main principale / Main secondaire | Temps de chargement de l’arbalète : −0,12 × L seconde. |
| Perforation renforcée (`reinforced_piercing`) | V | Arbalètes | Main principale | Perforation des projectiles : +L. |
| Bastion (`bastion`) | V | Boucliers | Une des mains | Résistance au recul : +0,08 × L, en tenant le bouclier. |
| Riposte (`riposte`) | V | Boucliers | Une des mains | En subissant une attaque : 12 / 19 / 26 / 33 / 40 % de chance d’infliger 1 à 4 dégâts d’Épines à l’attaquant. |
| Pas léger (`feather_step`) | V | Bottes | Pieds | Protection contre les chutes : +2 × L points de protection d’enchantement, hors dégâts contournant l’invulnérabilité. |
| Garde abyssale (`abyssal_guard`) | V | Plastrons | Torse | Efficacité de déplacement dans l’eau : +0,2 × L. |
| Second souffle (`second_wind`) | V | Plastrons | Torse | En subissant une attaque : 10 / 15 / 20 / 25 / 30 % de chance de recevoir Régénération I pendant 2 à (2 + 1,5 × (L − 1)) secondes. |

<a name="page-enchantements-traits-darmure"></a>

## Traits d’armure

| Enchantement | Maximum défini | Équipement | Emplacement actif | Effet |
| --- | --- | --- | --- | --- |
| Concentration (`focus`) | V | Casques | Tête | Efficacité de minage : +0,35 × L à l’attribut. |
| Souffle profond (`deep_breath`) | V | Casques | Tête | Bonus d’oxygène : +0,5 × L à l’attribut. |
| Esprit d’acier (`iron_mind`) | V | Casques | Tête | Résistance au recul : +0,035 × L. |
| Vision abyssale (`abyssal_sight`) | V | Casques | Tête | Vitesse de minage sous l’eau : +0,15 × L à l’attribut. |
| Vigilance (`vigilance`) | V | Casques | Tête | Protection contre les projectiles : +1,5 × L points de protection d’enchantement, hors dégâts contournant l’invulnérabilité. |
| Carapace (`carapace`) | V | Plastrons | Torse | Armure : +0,5 × L. |
| Garde ardente (`emberguard`) | V | Plastrons | Torse | Durée de combustion : −8 % × L, multiplicateur de la valeur totale. |
| Ancrage explosif (`blast_anchor`) | V | Plastrons | Torse | Résistance au recul des explosions : +0,08 × L. |
| Cœur gardé (`vital_guard`) | V | Plastrons | Torse | Vie maximale : +0,5 × L point de vie (soit +0,25 × L cœur). |
| Agilité (`agility`) | V | Jambières | Jambes | Force du saut : +2 % × L, multiplicateur de la valeur totale. |
| Élan (`momentum`) | V | Jambières | Jambes | Vitesse de déplacement : +1,2 % × L, multiplicateur de la valeur totale. |
| Pas d’ombre (`shadow_step`) | V | Jambières | Jambes | Vitesse en position accroupie : +0,06 × L à l’attribut. |
| Stabilité (`stability`) | V | Jambières | Jambes | Résistance au recul : +0,03 × L. |
| Pionnier (`trailblazer`) | V | Jambières | Jambes | Efficacité de déplacement : +0,08 × L à l’attribut. |
| Pas de braise (`cinder_step`) | V | Bottes | Pieds | Durée de combustion : −6 % × L, multiplicateur de la valeur totale. |
| Coureur (`runner`) | V | Bottes | Pieds | Vitesse de déplacement : +1,5 % × L, multiplicateur de la valeur totale. |
| Grande foulée (`stride`) | V | Bottes | Pieds | Hauteur de franchissement : +0,1 × L bloc. |
| Pied sûr (`sure_foot`) | V | Bottes | Pieds | Distance de chute sans dégâts : +0,5 × L bloc. |
| Marcheur (`wanderer`) | V | Bottes | Pieds | Efficacité de déplacement : +0,1 × L à l’attribut. |

<a name="page-enchantements-maîtrises-et-spécialisations"></a>

## Maîtrises et spécialisations

| Enchantement | Maximum défini | Équipement | Emplacement actif | Effet |
| --- | --- | --- | --- | --- |
| Maîtrise martiale (`weapon_mastery`) | V | Épées | Main principale | Dégâts : +0,4 × L. |
| Maîtrise de l’outil (`tool_mastery`) | V | Objets explicitement listés (voir catalogue) | Main principale | Vitesse de casse : +10 % × L de la valeur de base ; portée des blocs : +L bloc. |
| Maîtrise d’armure (`armor_mastery`) | V | Armures | Armure | Robustesse d’armure : +0,25 × L. |
| Maîtrise du bouclier (`shield_mastery`) | IV | Boucliers | Une des mains | Résistance au recul : +0,05 × L, en tenant le bouclier. |
| Maîtrise d’arbalète (`crossbow_mastery`) | V | Arbalètes | Main principale | Dégâts de flèches : +0,2 × L ; accélération du projectile (voir note de version). |
| Tir forgé (`forged_shot`) | V | Arcs | Main principale | Dégâts de flèches : +0,25 × L ; accélération du projectile (voir note de version). |
| Main sûre (`steady_hand`) | V | Arcs | Main principale | Dégâts de flèches : +0,25 × L. |

<a name="page-enchantements-entretien"></a>

## Entretien

| Enchantement | Maximum défini | Équipement | Emplacement actif | Effet |
| --- | --- | --- | --- | --- |
| Entretien (`weapon_familiarity`) | IV | Épées | Main principale | Avant 1.21.11 : dégâts de durabilité ×0,9 / 0,8 / 0,7 / 0,6. En 1.21.11 : coup direct, 6 / 9 / 12 / 15 % de chance de réparer 3 / 4 / 5 / 6 points (I à IV). |
| Entretien (`tool_familiarity`) | IV | Outils d’entretien | Main principale | Marqueur Entretien : réparation pilotée par les fonctions de familiarité ; JSON sans effet natif. |
| Entretien (`ranged_familiarity`) | IV | Objets explicitement listés (voir catalogue) | Main principale | Marqueur Entretien : réparation pilotée par les fonctions de familiarité ; JSON sans effet natif. |
| Entretien (`shield_familiarity`) | IV | Boucliers | Une des mains | Marqueur Entretien : réparation pilotée par les fonctions de familiarité ; JSON sans effet natif. |
| Entretien (`armor_familiarity`) | IV | Armures | Armure | Avant 1.21.11 : dégâts de durabilité ×0,9 / 0,8 / 0,7 / 0,6. En 1.21.11 : après une attaque reçue, 4 / 6 / 8 / 10 % de chance de réparer 2 / 3 / 4 / 5 points (I à IV). |

<a name="page-enchantements-évolutions-du-bouclier"></a>

## Évolutions du bouclier

| Enchantement | Maximum défini | Équipement | Emplacement actif | Effet |
| --- | --- | --- | --- | --- |
| Garde vive (`shield_quick_guard`) | I | Boucliers | Une des mains | Marqueur : un blocage compté accorde Vitesse I pendant 2 s. |
| Trempe défensive (`shield_tempered`) | I | Boucliers | Une des mains | Chaque point de dégât de durabilité a 25 % de chance d’être supprimé. |
| Rempart vivant (`shield_living_bulwark`) | I | Boucliers | Une des mains | Marqueur : un blocage compté accorde Résistance I pendant 2 s. |
| Appel du Bastion (`shield_bastion_call`) | I | Boucliers | Une des mains | Marqueur : après un blocage, au palier IV en netherite, invoque deux golems si le délai de 20 s est terminé ; durée prévue des golems 30 s. |

<a name="page-enchantements-exploits-et-vétérans"></a>

## Exploits et vétérans

| Enchantement | Maximum défini | Équipement | Emplacement actif | Effet |
| --- | --- | --- | --- | --- |
| Vétéran (`battle_hardened`) | I | Armes suivies par l’histoire | Main principale | Dégâts : +0,5. |
| Fléau des infectés (`zombie_slayer`) | I | Armes suivies par l’histoire | Main principale | Dégâts contre #attuned:zombie\_family : +2. |
| Briseur d’os (`skeleton_slayer`) | I | Armes suivies par l’histoire | Main principale | Dégâts contre #attuned:skeleton\_family : +2. |
| Sang-froid (`creeper_slayer`) | I | Armes suivies par l’histoire | Main principale | Dégâts contre les creepers : +2,5. |
| Brise-flamme (`blaze_slayer`) | I | Armes suivies par l’histoire | Main principale | Dégâts contre les blazes : +2,5. |
| Traqueur du Vide (`enderman_slayer`) | I | Armes suivies par l’histoire | Main principale | Dégâts contre les endermen : +2,5. |
| Héritage draconique (`dragon_legacy`) | I | Armes suivies par l’histoire | Main principale | Dégâts contre #attuned:end\_family : +1,5. |
| Héritage nécrotique (`wither_legacy`) | I | Armes suivies par l’histoire | Main principale | Dégâts contre #attuned:wither\_family : +1,5. |
| Héritage abyssal (`guardian_legacy`) | I | Armes suivies par l’histoire | Main principale | Dégâts contre #attuned:guardian\_family : +1,5. |
| Écho brisé (`warden_legacy`) | I | Armes suivies par l’histoire | Main principale | Dégâts : +0,75. |
| Mineur éprouvé (`miner_veteran`) | I | Pioches | Main principale | Vitesse de casse : +5 % de la valeur de base. |
| Bûcheron éprouvé (`lumber_veteran`) | I | Haches | Main principale | Vitesse de casse : +5 % de la valeur de base. |
| Terrassier éprouvé (`digger_veteran`) | I | Pelles | Main principale | Vitesse de casse : +5 % de la valeur de base. |
| Cultivateur éprouvé (`harvest_veteran`) | I | Houes | Main principale | Vitesse de casse : +5 % de la valeur de base. |
| Armure endurcie (`armor_veteran`) | I | Armures | Armure | Robustesse d’armure : +0,25. |
| Gardien éprouvé (`shield_veteran`) | I | Boucliers | Une des mains | Résistance au recul : +0,05, en tenant le bouclier. |

<a name="page-enchantements-marqueurs"></a>

## Marqueurs

| Enchantement | Maximum défini | Équipement | Emplacement actif | Effet |
| --- | --- | --- | --- | --- |
| Expérience naturelle (`experienced`) | I | Objets explicitement listés (voir catalogue) | Une des mains | Marqueur d’expérience naturelle ; aucun effet natif dans son JSON. |
| Empreinte d’histoire (`history_imprint`) | I | Équipement compatible avec l’histoire | Tous emplacements | Marqueur d’histoire ; aucun effet natif dans son JSON. |

<a name="page-enchantements-incompatibilités-de-la-table"></a>

## Incompatibilités de la table

Trois paires sont exclusives dans les définitions et contrôlées par les menus d’apprentissage :

| Famille | Première option | Seconde option |
| --- | --- | --- |
| Combat | Exécution | Siphon |
| Arc | Longue portée | Volée |
| Bouclier | Bastion | Riposte |

Les fonctions d’histoire peuvent attribuer des enchantements directement. Les messages du menu indiquent d’ailleurs qu’une évolution ultérieure peut dépasser certaines de ces limites ; les paires ci-dessus décrivent la table, sans interdire les récompenses que l’histoire applique séparément.

Sources : `data/attuned/tags/enchantment/exclusive_set/*.json` ; `data/attuned/function/enchanting/apply/execution.mcfunction`, lignes 9–10, et les cinq autres fonctions de ces paires.

<a name="page-enchantements-détails-qui-évitent-les-malentendus"></a>

## Détails qui évitent les malentendus

**Bûcheron et Moisson** augmentent ici des attributs de minage et, pour Moisson, la portée des blocs. Leur définition n’abat pas un arbre entier et ne replante pas automatiquement les cultures. **Vision abyssale** modifie le minage sous l’eau ; son fichier ne donne pas Vision nocturne. **Longue portée** ajoute des dégâts à la flèche sans vérifier la distance de la cible dans son propre effet d’enchantement. Les critères d’histoire qui permettent de l’obtenir sont un système séparé.

**Tir forgé, Maîtrise d’arbalète et Longue portée** accélèrent aussi le projectile à sa création. Jusqu’aux variantes précédant `overlay_94`, `compat/projectile_boost` multiplie les trois composantes de mouvement par environ 1,1, avec conversion entière intermédiaire. En 1.21.11, l’overlay 94 remplace cette fonction par une impulsion locale avant : sa magnitude vaut `0.03 × L` pour Tir forgé, `0.02 × L` pour Maîtrise d’arbalète et `0.1` fixe pour Longue portée. Le bonus n’est donc pas identique dans sa formulation entre toutes les versions ; ne pas additionner les anciennes et nouvelles variantes.

**Entretien d’épée et d’armure** change également en 1.21.11 : la réduction multiplicative de l’usure est remplacée par une réparation probabiliste après une attaque. Les deux comportements sont indiqués dans leurs lignes respectives. Les variantes d’overlay remplacent la définition de base, elles ne s’ajoutent pas à elle.

**Volée** écrit un bonus de nombre de projectiles et de dispersion. Son maximum défini est V, mais les menus standard et Maîtrise de cette version donnent seulement I. La disponibilité des niveaux supérieurs doit être distinguée de leur simple existence dans le JSON.

Les entrées sans effet natif ne sont pas toutes inactives : les trois marqueurs de garde du bouclier et les marqueurs d’entretien sont lus par des fonctions. Garde vive et Rempart vivant déclenchent leurs effets après un blocage compté ; l’Appel du Bastion requiert également le palier IV et un bouclier en netherite.

<a name="page-enchantements-familles-de-cibles-des-exploits"></a>

## Familles de cibles des exploits

| Tag | Créatures listées dans le pack |
| --- | --- |
| `zombie_family` | Zombie, zombie villageois, zombie momifié, noyé, piglin zombifié |
| `skeleton_family` | Squelette, vagabond, embourbé, wither squelette |
| `end_family` | Ender Dragon, enderman, shulker |
| `guardian_family` | Gardien, grand gardien |
| `wither_family` | Wither, wither squelette |

Sources : `data/attuned/tags/entity_type/<famille>.json`.

<a name="page-enchantements-sources-et-données-complètes"></a>

## Sources et données complètes

Chaque identifiant du tableau correspond à `data/attuned/enchantment/<identifiant>.json` dans l’archive v0.17.1. Le [catalogue CSV](../catalogues/enchantements.csv) conserve les 73 lignes ; le [catalogue JSON](../catalogues/enchantements.json) ajoute la définition complète, les effets structurés et toutes les variantes d’overlay, avec les chemins et numéros de lignes.

Les comportements scriptés du bouclier sont définis dans `data/attuned/function/shield/effects_mainhand.mcfunction`, lignes 1–3, `effects_offhand.mcfunction`, lignes 1–3, `summon_bastion.mcfunction` et `data/attuned/function/maintenance/slow_20t.mcfunction`, lignes 6–7. L’accélération précédente à l’overlay 94 se trouve dans `data/attuned/function/compat/projectile_boost.mcfunction`, lignes 1–6.
