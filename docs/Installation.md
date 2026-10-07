[Accueil du wiki](Home.md) · [Sommaire du dépôt](../README.md) · [Annexes](../ANNEXES.md)

<a name="page-installation"></a>

# Installation

Cette page concerne **Attuned Equipment v0.17.1 pour Minecraft Java 1.21.x**. Les différences entre versions sont détaillées dans [Compatibilité](Compatibilite.md).

<a name="page-installation-les-deux-packs"></a>

## Les deux packs

| Élément | Rôle | Où l’installer |
| --- | --- | --- |
| `Attuned_Equipment_DP_1.21.x_v0.17.1.zip` | Progression, fonctions, recettes, enchantements et trésors | Dossier `datapacks` du monde |
| `resources.zip`, inclus dans le premier ZIP | Textures, modèles et traductions | Dossier `resourcepacks` de chaque client |

Le fichier `resources.zip` extrait peut être conservé sous ce nom ou renommé `Attuned_Equipment_RP_1.21.x_v0.17.1.zip`. Le renommage ne modifie pas son contenu. Il faut extraire **ce fichier ZIP imbriqué**, et non déplacer le datapack entier dans `resourcepacks`.

<a name="page-installation-monde-solo-existant"></a>

## Monde solo existant

1. Faire une sauvegarde du monde avant une mise à jour de datapack.
2. Ouvrir le dossier du monde. Depuis la liste des mondes, l’action d’ouverture du dossier se trouve dans les options de modification du monde.
3. Placer le ZIP du datapack dans `<dossier-du-monde>/datapacks/`.
4. Retirer l’ancienne édition Attuned de ce même dossier. Une seule édition doit rester active.
5. Extraire `resources.zip` de l’archive fournie et placer ce ZIP dans le dossier `resourcepacks` du client. Le menu des packs de ressources permet d’ouvrir ce dossier.
6. Activer ce resource pack dans les options du jeu.
7. Ouvrir le monde. Si le monde est déjà chargé et que vous avez les permissions nécessaires, exécuter `/reload` ; sinon le fermer puis le rouvrir.
8. Vérifier le chargement et suivre le [guide des équipements](Equipements.md).

Les noms exacts des boutons varient avec la langue du client. Sur une instance de lanceur séparée, utiliser les dossiers de cette instance.

<a name="page-installation-serveur"></a>

## Serveur

Le datapack s’installe dans `<dossier-du-monde>/datapacks/` **sur le serveur**. Le resource pack doit être distribué et activé sur les clients des joueurs. Un pack de ressources oublié chez un joueur peut affecter son affichage sans signifier que la logique serveur est absente.

Après remplacement du datapack, redémarrer le serveur ou utiliser `/reload` avec les droits nécessaires. Si un autre datapack remplace les mêmes tables de coffres, il faudra fusionner les ajouts : voir [Reliques et butin](Reliques-et-butin.md).

<a name="page-installation-vérification-rapide"></a>

## Vérification rapide

Un administrateur peut utiliser :

```mcfunction
/datapack list enabled
```

Le pack doit figurer parmi les packs actifs. Après chargement, le code prévoit un message Attuned contenant `v0.17.1`.

Pour inspecter un objet tenu, un administrateur peut ensuite utiliser :

```mcfunction
/function attuned:info
```

Un objet neuf peut ne pas encore avoir été initialisé : voir la famille correspondante dans [Équipements](Equipements.md). Les kits de test sont décrits dans [Commandes](Commandes.md).

<a name="page-installation-langue-et-mise-à-jour-des-anciens-objets"></a>

## Langue et mise à jour des anciens objets

Les textes suivent la langue du jeu, avec français et anglais. Le code utilise une traduction anglaise de secours lorsque le resource pack n’est pas disponible.

Une migration parcourt progressivement l’inventaire, la main secondaire et les emplacements d’armure. La note d’installation annonce environ huit secondes pour un passage complet à 20 ticks par seconde. Un objet stocké dans un coffre doit être sorti pour entrer dans ce parcours. La conversion cible les anciens textes Attuned reconnus ; les noms personnels non reconnus sont conservés.

Cette durée est une cadence nominale, pas une mesure effectuée dans cette analyse.

<a name="page-installation-précautions-de-version"></a>

## Précautions de version

Cette archive cible Java 1.21.x. Elle ne constitue pas une édition Bedrock, une édition 26.x ou une garantie pour les snapshots. Ne pas utiliser une rétrogradation de monde comme procédure d’installation.

Le vieux fichier `LISEZ-MOI_1.21.txt` mentionne encore v0.16.1. Pour les noms d’archives et les ajouts FR/EN et reliques, la note `INSTALLATION_v0.17.1.txt` et le code actuel sont prioritaires.

<a name="page-installation-sources"></a>

## Sources

`INSTALLATION_v0.17.1.txt` ; `pack.mcmeta` ; `resources.zip/pack.mcmeta` ; `data/minecraft/tags/function/load.json` ; `data/attuned/function/load.mcfunction` ; `data/attuned/function/info.mcfunction` ; `data/attuned/function/localization/tick.mcfunction` et `localization/scan.mcfunction`.

[Retour à l’accueil](Home.md)
