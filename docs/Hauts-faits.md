[Accueil du wiki](Home.md) · [Sommaire du dépôt](../README.md) · [Annexes](../ANNEXES.md)

<a name="page-hauts-faits"></a>

# Hauts faits et récompenses d'expérience

Les hauts faits complètent la progression à l'enclume. Ils inscrivent sur l'équipement ses activités marquantes et peuvent lui appliquer un enchantement automatiquement. Leurs compteurs restent **propres à l'objet**, et les récompenses ne demandent pas de lapis ou de niveaux d'expérience dans les fonctions qui les accordent.

Cette page décrit les seuils du code de la **v0.17.1**. Aucun combat de validation n'a été exécuté pendant l'analyse.

<a name="page-hauts-faits-maîtrises-de-créatures"></a>

## Maîtrises de créatures

| Créature | Éliminations comptées sur l'objet | Récompense |
| --- | ---: | --- |
| Zombie | 1 000 | Fléau des infectés I |
| Squelette | 1 000 | Briseur d'os I |
| Creeper | 500 | Sang-froid I |
| Enderman | 250 | Traqueur du Vide I |
| Blaze | 250 | Brise-flamme I |

Ces événements peuvent faire progresser une **épée, une hache, un arc ou une arbalète suivis en main principale**. Le code vérifie le type de l'objet au moment de l'élimination. Il utilise des avancées dédiées aux types de créatures correspondants : ne pas élargir automatiquement « zombie » à toutes ses variantes ou « squelette » à toutes les créatures apparentées.

Chaque récompense pose un marqueur empêchant de la redonner à répétition sur le même objet. Les fonctions de récompense modifient l'objet directement ; elles ne remettent pas un livre à appliquer plus tard.

**Sources du ZIP :** `data/attuned/advancement/history/mastery/*.json` ; `function/history/mastery/{zombie,skeleton,creeper,enderman,blaze}_kill.mcfunction`, lignes 1–5 ; `function/history/mastery/inc_*.mcfunction`, ligne 6 ; `function/history/mastery/unlock_*.mcfunction` ; `item_modifier/history/mastery/unlock_{zombie,skeleton,creeper,enderman,blaze}.json`.

<a name="page-hauts-faits-métiers-et-pratique-prolongée"></a>

## Métiers et pratique prolongée

| Activité | Seuil | Récompense |
| --- | ---: | --- |
| Éliminations sur une arme suivie | 1 000 | Vétéran I |
| Roche comptée pour une pioche | 10 000 | Mineur éprouvé I |
| Bûches comptées pour une hache | 5 000 | Bûcheron éprouvé I |
| Terrain compté pour une pelle | 10 000 | Terrassier éprouvé I |
| Cultures comptées pour une houe | 5 000 | Cultivateur éprouvé I |
| Blocages du bouclier | 2 500 | Gardien éprouvé I |
| Coups subis par une pièce d'armure portée | 2 000 par pièce | Armure endurcie I |

La roche reconnue pour ce compteur de pioche comprend la pierre, l'ardoise des abîmes, la netherrack et le tuf. Les minerais sont suivis séparément et ne sont pas le compteur utilisé par cette récompense de 10 000 roches.

Les listes de blocs sont explicites dans les statistiques enregistrées. Pour la houe, le code suit blé, carottes, pommes de terre, betteraves, verrues du Nether, cacao, pastèques et citrouilles. Les tests ne vérifient pas un âge de culture dans cette fonction de statistiques : « récoltes mûres » serait une description plus restrictive que le code.

Les sous-compteurs de métier proviennent de variations de statistiques du joueur, traitées lors d'une utilisation de l'outil. Ils doivent être compris comme des événements comptabilisés par le datapack, pas comme une garantie de provenance exclusive de chaque bloc dans toutes les situations de changement d'outil.

**Sources du ZIP :** `data/attuned/function/history/event/inc_kills.mcfunction`, ligne 7 ; `function/history/activity/write_{stone,logs,terrain,crops}.mcfunction`, ligne 7 ; `function/history/shield_{mainhand,offhand}.mcfunction`, ligne 13 ; `function/armor/add/{helmet,chestplate,leggings,boots}_hits.mcfunction`, ligne 7 ; `function/load.mcfunction`, lignes 209–216 et 260–275 ; `function/history/activity/{pickaxe,axe,shovel,hoe}.mcfunction`.

<a name="page-hauts-faits-exploits-de-boss"></a>

## Exploits de boss

| Boss vaincu | Enchantement attribué à l'arme admissible |
| --- | --- |
| Ender Dragon | Héritage draconique I |
| Wither | Héritage nécrotique I |
| Grand gardien | Héritage abyssal I |
| Warden | Écho brisé I |

Quand l'événement de boss est attribué au joueur, son exploit est enregistré sur l'objet suivi en main principale, l'objet suivi en main secondaire et les quatre pièces suivies portées. L'enchantement de récompense du tableau est cependant attribué uniquement à une **épée, une hache, un arc ou une arbalète suivis en main principale**, et une seule fois par objet pour ce boss.

Un bouclier ou une armure peut donc garder la mémoire de la victoire sans recevoir automatiquement l'enchantement offensif correspondant. Changer d'arme avant le déclenchement peut également modifier l'objet recevant la mémoire et la récompense.

**Sources du ZIP :** `data/attuned/advancement/history/feat/{dragon,wither,elder_guardian,warden}.json` ; `function/history/feat/*.mcfunction`, lignes 2–12 ; `item_modifier/history/feat/*.json` ; `item_modifier/history/mastery/unlock_{dragon_legacy,wither_legacy,guardian_legacy,warden_legacy}.json`.

<a name="page-hauts-faits-différence-avec-les-récompenses-de-la-station"></a>

## Différence avec les récompenses de la station

Les hauts faits utilisent des marqueurs de récompenses dans l'histoire de l'objet. La station utilise des marqueurs de bonus appliqués et des paliers réclamés. Débloquer un haut fait ne paie pas un palier à votre place et ne retire pas son coût en lapis.

Les effets exacts des enchantements de récompense sont détaillés dans [Enchantements](Enchantements.md). Pour le déroulement des paliers, consulter [Progression et histoire](Progression-et-histoire.md).
