[Accueil du wiki](Home.md) · [Sommaire du dépôt](../README.md) · [Annexes](../ANNEXES.md)

<a name="page-audit-enchantements-et-butin"></a>

# Audit — enchantements, savoirs et butin

<a name="page-audit-enchantements-et-butin-périmètre-et-niveau-de-preuve"></a>

## Périmètre et niveau de preuve

Cette analyse lit les fichiers de l’archive Attuned Equipment v0.17.1 comme des données. Elle ne constitue pas un test en jeu. Les faits chiffrés sont extraits de la base et recoupés avec les overlays ; les conséquences probables de commandes sont signalées comme des déductions. Les tableaux du wiki distinguent les ressources actives, les branches à vérifier et les contenus préparés pour un registre plus récent.

Les 73 enchantements incluent 20 savoirs Attuned, 19 traits d’armure, 7 maîtrises/spécialisations, 5 entretiens, 4 marqueurs d’évolution du bouclier, 16 exploits/vétérans et 2 marqueurs généraux. L’archive comporte aussi 27 livres/tomes, 10 reliques, 24 chemins de bonus de butin, 15 recettes et 36 définitions d’échange. Les 100 loot tables Attuned comprennent les 63 catalyseurs traités dans le volet forge, les 27 livres/tomes et les 10 reliques.

<a name="page-audit-enchantements-et-butin-points-nécessitant-une-vérification-ou-une-correction-future"></a>

## Points nécessitant une vérification ou une correction future

<a name="page-audit-enchantements-et-butin-un-clic-peut-acheter-plusieurs-rangs-de-tome-successifs"></a>

### Un clic peut acheter plusieurs rangs de tome successifs

**Statut :** Conséquence statique directe, à confirmer en jeu.

Les conditions de try consultent successivement le rang courant. Une fonction level\_N réussie modifie immédiatement ce rang avant le test suivant ; elle ne retourne pas depuis la fonction appelante. Les fonctions level\_N ne vérifient pas la présence du tome, et ne conditionnent pas la suite au succès du clear du tome.

Avec rang Vitalité 0, un seul tome, 32 blocs de lapis et au moins 61 niveaux disponibles, le chemin commande peut aller jusqu’à Vitalité V en un clic. Chaque coût de lapis et de niveaux est vérifié et prélevé ; les clear de tomes des rangs ultérieurs peuvent échouer sans empêcher les rangs.

**Conséquence pour le wiki :** Lors d’une future correction autorisée, choisir le rang une seule fois (ou return run function au bon rang) et revérifier la quantité de tome avant le prélèvement.

Sources : `data/attuned/function/tomes/vitality/try.mcfunction`, lignes 2–8 ; `data/attuned/function/tomes/vitality/level_1.mcfunction`, lignes 1–13 ; `data/attuned/function/tomes/vitality/level_2.mcfunction`, lignes 1–13 ; `data/attuned/function/tomes/vigor/try.mcfunction`, lignes 2–6 ; `data/attuned/function/tomes/dexterity/try.mcfunction`, lignes 2–6.

<a name="page-audit-enchantements-et-butin-les-36-échanges-sont-dormants-sur-la-cible-java-121x"></a>

### Les 36 échanges sont dormants sur la cible Java 1.21.x

**Statut :** Confirmé par annonce officielle de registre.

Le pack contient uniquement les définitions villager\_trade et leurs tags. Ce registre a été introduit dans Java 26.1, après la plage 1.21.x annoncée. Aucune fonction locale d’injection Offers n’a été identifiée.

**Conséquence pour le wiki :** Conserver la liste comme catalogue de préparation ; ne pas annoncer ces échanges comme accessibles en survie 1.21.x et ne pas déduire une compatibilité 26.1 du seul registre.

Sources : `data/attuned/villager_trade/cleric/vitality.json`, lignes 1–31 ; `data/minecraft/tags/villager_trade/cleric/level_5.json`, lignes 1–8.

Source officielle : [Minecraft Java 26.1](https://www.minecraft.net/en-us/article/minecraft-java-edition-26-1).

<a name="page-audit-enchantements-et-butin-bonus-de-livres-des-coffres-forts-des-épreuves-à-tester"></a>

### Bonus de livres des coffres-forts des épreuves à tester

**Statut :** Branche présente, déclenchement réel non établi.

Deux advancements écoutent player\_generates\_container\_loot pour reward/reward\_ominous. La présence de la bonne table ne prouve pas que le Vault émet cet événement. Aucun essai de Vault ni preuve primaire de ce point ne fait partie de cette analyse.

**Conséquence pour le wiki :** Tester un coffre-fort neuf normal et menaçant avant de transformer les chances prévues en promesse de disponibilité.

Sources : `data/attuned/advancement/loot/trial_reward.json`, lignes 1–13 ; `data/attuned/advancement/loot/trial_ominous.json`, lignes 1–13 ; `data/attuned/function/loot/structure/trial_reward.mcfunction`, lignes 1–10 ; `data/attuned/function/loot/structure/trial_ominous.mcfunction`, lignes 1–10.

<a name="page-audit-enchantements-et-butin-le-texte--deux-enchantements-au-total--décrit-mal-les-objets-déjà-enchantés"></a>

### Le texte « deux enchantements au total » décrit mal les objets déjà enchantés

**Statut :** Écart entre formulation UI et opérations.

Le menu annonce deux enchantements au total, mais l’application choisit un enchantement et au plus un bonus sans compter les enchantements déjà présents. Les modificateurs set\_enchantments ne vident pas explicitement les autres entrées.

**Conséquence pour le wiki :** Dans le wiki, écrire « un enchantement choisi et au plus un bonus supplémentaire ».

Sources : `data/attuned/function/compat/menu/enchanting/main.mcfunction`, lignes 1–2 ; `data/attuned/function/enchanting/mastery/apply/attuned_excavation.mcfunction`, lignes 13–24 ; `data/attuned/item_modifier/enchanting/mastery/attuned_excavation.json`, lignes 1–7.

<a name="page-audit-enchantements-et-butin-le-menu-standard-lunge-ne-sélectionne-jamais-le-rang-i"></a>

### Le menu standard Lunge ne sélectionne jamais le rang I

**Statut :** Déduction statique des seuils.

Le dispatcher exige une puissance d’au moins 12 puis sélectionne déjà le niveau II dès 8 ; le niveau III est sélectionné à 15. Ainsi le niveauI existe en fonction mais n’est pas atteint par ce menu. Les fonctions réelles sont activées par overlay94 ; la base renvoie un message nécessitant 1.21.11.

**Conséquence pour le wiki :** Conserver les plages exactes dans le catalogue ; demander une décision de conception avant de changer le seuil.

Sources : `data/attuned/function/enchanting/vanilla_apply/lunge.mcfunction`, lignes 1–10 ; `data/attuned/function/enchanting/vanilla_apply/lunge_1.mcfunction`, lignes 1–2.

<a name="page-audit-enchantements-et-butin-points-confirmés-à-conserver-dans-la-publication"></a>

## Points confirmés à conserver dans la publication

- Les reliques remplacent quatre tables de coffres : ancienne cité (25 %), trésor de bastion (25 %), pyramide (15 %) et cité de l’End (35 %). Les choix au sein d’un pool ont des poids égaux.
- Neuf reliques ont bien une initialisation complète et 100 unités d’histoire ; le Serment des Cendres est la dixième, explicitement narrative. Il ne faut pas généraliser son absence de suivi aux neuf autres.
- Les coûts classiques sont 1/2/3 lapis et 1/2/3 niveaux XP. Leurs tirages internes sont aux niveaux 5/15/30 ; la puissance exigée est 1/8/15.
- La Maîtrise coûte 1 lapis et 5 niveaux, exige 15 puissance et un savoir, puis effectue 40 essais pour au plus 1 bonus appris.
- Les 20 savoirs Attuned sont achetés par niveau avec des blocs de lapis. Leurs plafonds standard et de Maîtrise sont distincts des max\_level de leurs définitions.
- L’overlay94 change réellement les cinq effets weapon\_familiarity, armor\_familiarity, forged\_shot, crossbow\_mastery et longshot ; les descriptions de la page Enchantements distinguent ces variantes.
- La recette netherite du bouclier accepte tout minecraft:shield au niveau de son filtre JSON. Les conditions de lignée et d’évolution sont traitées par d’autres fonctions et ne doivent pas être inventées dans la recette.

Les fichiers `findings.json` et les neuf couples de catalogues CSV/JSON conservent les extractions, les variantes et les références de lignes. Les scripts de génération sont des outils de documentation écrits pour cette analyse ; ils ne lancent aucune fonction Minecraft.
