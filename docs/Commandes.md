[Accueil du wiki](Home.md) · [Sommaire du dépôt](../README.md) · [Annexes](../ANNEXES.md)

<a name="page-commandes"></a>

# Commandes d’administration et de démonstration

Les interactions normales passent par les objets et stations décrits dans les guides. Les commandes ci-dessous sont destinées à un joueur disposant des permissions nécessaires, dans un monde de test ou pour un diagnostic.

<a name="page-commandes-inspecter"></a>

## Inspecter

| Commande | Effet |
| --- | --- |
| `/datapack list enabled` | Affiche les datapacks activés |
| `/reload` | Recharge les données du monde |
| `/function attuned:info` | Affiche les données Attuned de l’objet tenu et des indications de progression |

`attuned:info` affiche les données internes de l’objet ; ce n’est pas un menu d’évolution. S’il indique que l’objet n’est pas suivi, consulter les conditions d’initialisation de sa famille.

<a name="page-commandes-donner-des-objets-de-test"></a>

## Donner des objets de test

| Commande | Contenu principal |
| --- | --- |
| `/function attuned:give/visual_test` | Variantes d’arcs et d’arbalètes pour vérifier l’affichage |
| `/function attuned:give/all_bows` | Famille d’arcs |
| `/function attuned:give/all_crossbows` | Famille d’arbalètes |
| `/function attuned:give/armor_test_kit` | Quatre pièces d’armure en fer et 64 lapis |
| `/function attuned:give/knowledge_books` | Livres de savoir déclarés dans la fonction de test |
| `/function attuned:give/tomes` | Un tome de vitalité, un de vigueur et un de dextérité |
| `/function attuned:give/test_kit` | Ensemble étendu : objets, matériaux, lapis, livres et **60 niveaux d’XP** |

Le kit complet ajoute directement des ressources et de l’expérience. Prévoir de la place dans l’inventaire ; les fonctions de démonstration ne sont pas une étape nécessaire de progression en survie.

Le message du kit d’armure cite encore `v0.14.0` dans cette archive. Ce texte ancien ne change pas la version déclarée du pack.

<a name="page-commandes-utilisation-depuis-la-console-dun-serveur"></a>

## Utilisation depuis la console d’un serveur

Les fonctions de distribution utilisent `@s`. Elles doivent donc s’exécuter **en tant que joueur**. Depuis une console, remplacer `PseudoDuJoueur` par le pseudo exact :

```mcfunction
execute as PseudoDuJoueur at PseudoDuJoueur run function attuned:give/visual_test
```

Le slash initial peut être nécessaire dans le chat, alors que les consoles de serveur attendent généralement la commande sans slash.

<a name="page-commandes-boutons-et-anciens-déclencheurs"></a>

## Boutons et anciens déclencheurs

Le code contient des objectifs `trigger`, mais plusieurs opérations exigent une session ouverte par l’interaction correspondante. Les appeler à la main n’est pas une procédure générale de déblocage. Les anciennes routes d’enclume sont détaillées dans l’[audit technique](Audit-technique.md).

<a name="page-commandes-signaler-un-problème-utilement"></a>

## Signaler un problème utilement

Joindre la version exacte de Minecraft, la version des deux packs, la liste des autres datapacks, le type et le matériau de l’objet, ses paliers et l’action effectuée. Pour un problème de chargement, copier l’erreur pertinente de `latest.log`. Pour un problème visuel, préciser si le resource pack est activé et quels autres packs ont priorité.

<a name="page-commandes-sources"></a>

## Sources

`data/attuned/function/info.mcfunction` ; `data/attuned/function/give/test_kit.mcfunction` ; `data/attuned/function/give/visual_test.mcfunction` ; `data/attuned/function/give/all_bows.mcfunction` ; `data/attuned/function/give/all_crossbows.mcfunction` ; `data/attuned/function/give/armor_test_kit.mcfunction` ; `data/attuned/function/give/knowledge_books.mcfunction` ; `data/attuned/function/give/tomes.mcfunction` ; `data/attuned/function/anvil/process.mcfunction`.

[Retour à l’accueil](Home.md)
