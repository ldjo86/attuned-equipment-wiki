[Accueil du wiki](Home.md) · [Sommaire du dépôt](../README.md) · [Annexes](../ANNEXES.md)

<a name="page-faq"></a>

# Questions fréquentes

<a name="page-faq-dois-je-installer-un-mod-"></a>

## Dois-je installer un mod ?

Le pack fourni utilise les systèmes de datapacks et de resource packs de Minecraft Java. Son installation décrite n’exige pas de mod. La compatibilité avec un serveur modifié n’a cependant pas été testée dans cette analyse. Voir [Installation](Installation.md) et [Compatibilité](Compatibilite.md).

<a name="page-faq-pourquoi-les-textures-ou-les-traductions-napparaissent-elles-pas-"></a>

## Pourquoi les textures ou les traductions n’apparaissent-elles pas ?

Le `resources.zip` contenu dans le datapack ne s’active pas à cet emplacement. Il faut l’extraire, le placer dans les packs de ressources du client et l’activer. Sur un serveur, chaque joueur doit disposer de ce pack. Vérifier aussi la priorité des autres resource packs. Voir [Resource pack](Resource-pack.md).

<a name="page-faq-le-cuivre-ressemble-à-du-fer-sur-ma-version--est-ce-prévu-"></a>

## Le cuivre ressemble à du fer sur ma version : est-ce prévu ?

Avant Java 1.21.9, le palier cuivre des épées et outils utilise un objet de base en fer avec des données Attuned cuivre. Son histoire et sa prochaine reforge suivent le cuivre ; ses propriétés vanilla de base restent celles du fer. Ce comportement est décrit dans [Compatibilité](Compatibilite.md).

<a name="page-faq-jai-atteint-le-nombre-dutilisations-pourquoi-mon-objet-névolue-t-il-pas-"></a>

## J’ai atteint le nombre d’utilisations, pourquoi mon objet n’évolue-t-il pas ?

L’histoire rend un palier accessible. La station d’enclume doit encore le valider, avec les conditions de matériau et de potentiel, le lapis demandé et les niveaux d’XP du joueur. Les paliers sont successifs. Consulter [Progression et histoire](Progression-et-histoire.md), puis [Enclume](Enclume.md).

<a name="page-faq-pourquoi-mon-objet-en-netherite-a-t-il-moins-de-potentiel-"></a>

## Pourquoi mon objet en netherite a-t-il moins de potentiel ?

Le matériau final et le potentiel d’origine sont différents. Un objet nouvellement initialisé en netherite commence généralement avec un potentiel II ; un objet ayant conservé une lignée commencée dans un matériau donnant le potentiel V peut garder ce plafond supérieur. Une fabrication neuve ne reprend pas l’histoire d’un exemplaire précédent. Les exceptions et familles sont détaillées dans [Équipements](Equipements.md).

<a name="page-faq-une-relique-commence-t-elle-déjà-avec-deux-évolutions-"></a>

## Une relique commence-t-elle déjà avec deux évolutions ?

Les neuf reliques compatibles portent 100 utilisations ou points d’expérience d’armure hérités, mais leur évolution commence à zéro. L’histoire facilite l’accès aux premiers seuils ; les évolutions et récompenses restent à obtenir selon leurs conditions. La hache en or est l’exception narrative. Voir [Reliques et butin](Reliques-et-butin.md).

<a name="page-faq-puis-je-renommer-et-réparer-normalement-à-lenclume-"></a>

## Puis-je renommer et réparer normalement à l’enclume ?

La station Attuned utilise son propre inventaire et ses propres transactions. Elle ne reproduit pas l’ensemble des opérations de l’enclume vanilla. Certaines anciennes fonctions de réparation et de consultation existent encore dans les fichiers, mais leur présence ne signifie pas qu’un bouton actuel les ouvre. Voir [Enclume](Enclume.md) et [Audit technique](Audit-technique.md).

<a name="page-faq-puis-je-reforger-une-armure-par-le-menu-générique-de-la-forge-"></a>

## Puis-je reforger une armure par le menu générique de la forge ?

Un problème de routage a été repéré dans v0.17.1 : une armure peut atteindre un menu prévu pour des armes et outils. Sous certaines conditions, ce chemin peut prélever les matériaux sans appliquer une conversion d’armure. Cette possibilité est déduite du code et doit être reproduite en monde de test. Consulter [Forge](Forge.md) avant cette opération ; les transformations effectivement disponibles y sont distinguées des anciennes fonctions.

<a name="page-faq-pourquoi-aucun-menu-moderne-ne-souvre-t-il-"></a>

## Pourquoi aucun menu moderne ne s’ouvre-t-il ?

Jusqu’à Java 1.21.5, les actions personnalisées de forge et d’enchantement utilisent des liens dans le chat. Fermer l’écran vanilla si nécessaire, ouvrir le chat avec **T** et cliquer avant l’expiration de la session. À partir de Java 1.21.6, le pack utilise les dialogues natifs. Voir [Compatibilité](Compatibilite.md).

<a name="page-faq-pourquoi-bûcheron-ne-coupe-t-il-pas-larbre-entier-"></a>

## Pourquoi Bûcheron ne coupe-t-il pas l’arbre entier ?

Le nom d’un enchantement ne suffit pas à définir son comportement. Dans ce pack, Bûcheron améliore un attribut de minage. Moisson modifie le minage et la portée ; sa définition ne replante pas automatiquement les cultures. Les effets réellement déclarés sont détaillés dans [Enchantements](Enchantements.md).

<a name="page-faq-pourquoi-les-villageois-ne-vendent-ils-pas-les-livres-préparés-"></a>

## Pourquoi les villageois ne vendent-ils pas les livres préparés ?

Le ZIP contient des définitions de commerce utilisant `villager_trade`, un registre introduit avec Java 26.1. Ces fichiers ne fournissent donc pas leurs offres en Java 1.21.x. Ils sont conservés dans l’analyse comme contenu préparé, avec cette limite explicite. Voir [Échanges préparés](Echanges-prepares.md).

<a name="page-faq-les-nouveaux-trésors-apparaissent-ils-dans-mes-anciens-coffres-"></a>

## Les nouveaux trésors apparaissent-ils dans mes anciens coffres ?

Les reliques sont ajoutées lors de la première génération du contenu des coffres concernés. Un coffre déjà ouvert ne reçoit pas rétroactivement une nouvelle relique. Les coffres compatibles, les chances et les conflits de tables figurent dans [Reliques et butin](Reliques-et-butin.md).

<a name="page-faq-peut-on-cumuler-tous-les-datapacks-de-butin-"></a>

## Peut-on cumuler tous les datapacks de butin ?

Deux fichiers portant le même identifiant de table de butin ne fusionnent pas automatiquement leurs ajouts. Attuned remplace quatre tables vanilla. Si un autre datapack remplace l’une d’elles, il faut fusionner leurs pools pour conserver les deux contributions. Voir [Compatibilité](Compatibilite.md).

<a name="page-faq-les-tomes-fonctionnent-ils-comme-un-achat-unique-garanti-"></a>

## Les tomes fonctionnent-ils comme un achat unique garanti ?

Un risque d’achats successifs au cours d’une seule interaction a été repéré dans les fonctions des tomes. Le code du rang suivant peut être évalué après l’achat du précédent, et le contrôle de présence du tome n’est pas répété à chaque rang. Lire [Tomes et savoirs](Tomes-et-savoirs.md) et l’[audit](Audit-technique.md) avant d’utiliser ce système avec beaucoup de lapis et d’XP.

<a name="page-faq-les-1-860-tests-annoncés-garantissent-ils-v0171-"></a>

## Les 1 860 tests annoncés garantissent-ils v0.17.1 ?

Le `VALIDATION.md` fourni porte le titre v0.16.1. L’analyse actuelle vérifie les fichiers de v0.17.1 de manière statique et ne lance pas Minecraft. Un résultat de parsing JSON ou une référence de modèle résolue ne garantit pas à lui seul un comportement en jeu. Voir [Sources et méthode](Sources-et-methode.md).

<a name="page-faq-ce-pack-fonctionne-t-il-sur-bedrock-ou-en-java-26x-"></a>

## Ce pack fonctionne-t-il sur Bedrock ou en Java 26.x ?

Cette archive vise Java 1.21.x. La présence de fichiers provenant de formats ultérieurs ne constitue pas un portage complet. Utiliser une édition appropriée à la version ciblée et ne pas rétrograder un monde pour l’installer.

[Retour à l’accueil](Home.md)
