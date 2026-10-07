[Accueil du wiki](Home.md) · [Sommaire du dépôt](../README.md) · [Annexes](../ANNEXES.md)

<a name="page-sources-et-methode"></a>

# Sources et méthode

<a name="page-sources-et-methode-archive-examinée"></a>

## Archive examinée

| Élément | Identification |
| --- | --- |
| Datapack | `Attuned_Equipment_DP_1.21.x_v0.17.1.zip` |
| Taille du ZIP fourni | 4 033 711 octets |
| SHA-256 du datapack | `37f220d2955f305821cfd2c7379be91674f996507b1afa62a86567b359c189ef` |
| Resource pack | Fichier `resources.zip` inclus dans le datapack |
| Taille du ZIP du RP | 289 554 octets |
| SHA-256 du RP | `666fbf47d2eaa7325ddcb191ae44c650f080ecc2c4e6a366b85fb530054a6620` |
| Date de l’analyse | 6 octobre 2026 |

La référence d’identité des fichiers est leur contenu dans cette archive. Les noms de fonction et de ressource `attuned:*` sont conservés pour permettre de retrouver précisément les mécanismes documentés.

<a name="page-sources-et-methode-inventaire"></a>

## Inventaire

Le datapack contient **6 627 fichiers**, dont 4 255 fonctions `.mcfunction` et 2 367 JSON. Ces nombres comprennent la base et les variantes d’overlays. Le resource pack imbriqué contient **145 fichiers**, dont 101 JSON, 43 PNG et un `pack.mcmeta`.

La base `data/attuned/` contient 1 561 fonctions, 788 modificateurs d’objets, 100 tables de butin, 73 définitions d’enchantement, 58 dialogues, 45 avancées techniques, 36 définitions d’échanges, 23 tags, 15 recettes et 7 prédicats. Le namespace `minecraft` fournit les points d’entrée, des tags et quatre remplacements de tables de coffres. Les variantes de compatibilité remplacent une partie de ces fichiers.

Les 45 fichiers d’avancement servent notamment à détecter des événements et à déclencher des fonctions. Il ne faut pas les présenter automatiquement comme 45 succès visibles dans un onglet de progression.

L’[inventaire CSV exhaustif](../reference/file-inventory.csv) indique le chemin, la couche, la taille et le SHA-256 de chaque fichier des deux archives. Le [manifeste des archives](../reference/archive-manifest.json) conserve leurs totaux et empreintes.

<a name="page-sources-et-methode-travail-effectué"></a>

## Travail effectué

1. Extraction des deux archives et inventaire des fichiers.
2. Lecture des métadonnées et des notices, puis distinction entre v0.17.1 et les anciennes notes.
3. Composition de la base avec chaque overlay applicable et contrôle des références locales reconnues.
4. Lecture des points d’entrée `load`, `tick`, des événements et des transactions pour déterminer les fonctions normalement accessibles.
5. Analyse des matériaux, plafonds, coûts, effets, recettes et sources de butin.
6. Décodage des 43 textures, inspection des modèles et vérification des clés de traduction.
7. Rédaction des guides, catalogues et observations, avec contrôle contradictoire des principaux résultats.

Les [résultats de validation statique](../reference/verification-statique.json) détaillent le périmètre des contrôles. Les preuves volumineuses de résolution de références sont regroupées dans [l’archive des références détaillées](../reference/detailed-reference-checks.zip). Les résultats des contrôles et les preuves de résolution des références sont fournis dans les annexes de référence.

<a name="page-sources-et-methode-lire-les-conclusions-correctement"></a>

## Lire les conclusions correctement

| Formulation | Ce qu’elle signifie |
| --- | --- |
| Présent dans les fichiers | La définition existe, sans garantir qu’un chemin de jeu l’utilise |
| Accessible dans le parcours actuel | Un chemin depuis les entrées normales du pack a été identifié |
| Risque déduit du code | Une séquence problématique est identifiable ; son effet reste à reproduire dans Minecraft |
| Contrôle statique réussi | Les fichiers examinés satisfont le contrôle décrit |
| Test en jeu | Requiert une exécution du client ou du serveur ; aucun n’a été effectué dans cette analyse |

Une égalité des clés de langues ne constitue pas une révision linguistique exhaustive. Une référence de texture résolue ne prouve pas un bon rendu dans toutes les perspectives. Une syntaxe JSON valide ne signifie pas qu’un schéma est reconnu par chaque version du jeu.

<a name="page-sources-et-methode-points-dentrée-du-datapack"></a>

## Points d’entrée du datapack

`data/minecraft/tags/function/load.json` déclare `attuned:load` et `attuned:station/load`. `data/minecraft/tags/function/tick.json` déclare `attuned:tick` et `attuned:station/tick`.

Le tick général traite notamment les statistiques d’utilisation, les sessions de menus, l’histoire et la localisation. Des cadences de cinq ticks et vingt ticks répartissent certains entretiens. Le tick de station gère le parcours des enclumes. Ces cadences décrivent l’implémentation ; elles ne constituent pas une mesure de performance réelle.

<a name="page-sources-et-methode-anciennes-validations"></a>

## Anciennes validations

`VALIDATION.md` et `LISEZ-MOI_1.21.txt` sont titrés v0.16.1. Le premier annonce 1 860 assertions pour cette ancienne version. `INSTALLATION_v0.17.1.txt`, les deux métadonnées de pack et le message de chargement décrivent v0.17.1. Le présent wiki conserve cette distinction et n’attribue pas les anciens essais à la nouvelle archive.

<a name="page-sources-et-methode-provenance-et-droits"></a>

## Provenance et droits

Les mécanismes, noms, valeurs et pixels présentés proviennent du pack fourni. La planche de textures assemble ces pixels pour les montrer ; elle ne constitue pas une capture dans Minecraft. La documentation ne réattribue pas la création du datapack ou de ses graphismes.

Aucun fichier de licence explicite n’a été repéré dans les deux archives. Une licence pour la diffusion du pack ou du dépôt doit donc venir de son auteur ; ce wiki n’en invente pas une.

<a name="page-sources-et-methode-documentation-officielle-externe"></a>

## Documentation officielle externe

Les notes officielles de Minecraft servent à situer les changements de format et l’introduction des registres. Les données propres à Attuned restent fondées sur l’archive fournie.

- [Minecraft Java 1.21](https://www.minecraft.net/en-us/article/minecraft-java-edition-1-21).
- [Minecraft Java 1.21.2](https://www.minecraft.net/en-us/article/minecraft-java-edition-1-21-2).
- [Minecraft Java 1.21.4](https://www.minecraft.net/en-us/article/minecraft-java-edition-1-21-4).
- [Minecraft Java 1.21.5](https://www.minecraft.net/en-us/article/minecraft-java-edition-1-21-5).
- [Minecraft Java 1.21.6](https://www.minecraft.net/en-us/article/minecraft-java-edition-1-21-6).
- [Minecraft Java 1.21.7](https://www.minecraft.net/en-us/article/minecraft-java-edition-1-21-7).
- [Minecraft Java 1.21.9](https://www.minecraft.net/en-us/article/minecraft-java-edition-1-21-9).
- [Minecraft Java 1.21.11](https://www.minecraft.net/en-us/article/minecraft-java-edition-1-21-11).
- [Minecraft Java 26.1 — introduction de `villager_trade`](https://www.minecraft.net/en-us/article/minecraft-java-edition-26-1).
- [GitHub — documentation par Wiki](https://docs.github.com/en/communities/documenting-your-project-with-wikis/about-wikis).
- [GitHub — création de pages et dépôt Git du Wiki](https://docs.github.com/en/communities/documenting-your-project-with-wikis/adding-or-editing-wiki-pages).
- [CurseForge — guide de présentation et lien de Wiki](https://support.curseforge.com/support/solutions/articles/9000199552-overview-of-the-project-submission-page).

[Retour à l’accueil](Home.md)
