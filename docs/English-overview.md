[Accueil du wiki](Home.md) · [Sommaire du dépôt](../README.md) · [Annexes](../ANNEXES.md)

<a name="page-english-overview"></a>

# English overview

**Attuned Equipment v0.17.1 — Minecraft Java 1.21.x**

Attuned Equipment keeps equipment history on supported weapons, tools, armor and shields. Actions such as uses, shots, blocks and armor activity contribute to that history. Evolution tiers are then claimed at the Attuned anvil station, subject to the item’s potential, material, tier conditions and payment.

This repository contains a detailed French wiki and this English introduction. The datapack’s own resource pack supports French and English, with regional aliases.

<a name="page-english-overview-installation"></a>

## Installation

1. Put `Attuned_Equipment_DP_1.21.x_v0.17.1.zip` in the world’s `datapacks` folder.
2. Remove the previous Attuned datapack version from that folder.
3. Extract the embedded `resources.zip`, then put it in each client’s `resourcepacks` folder and enable it.
4. Reload or restart the world/server.

The resource pack is **not enabled automatically from inside the datapack ZIP**. On a server, every player needs it for the intended appearance and translations.

<a name="page-english-overview-four-different-ideas"></a>

## Four different ideas

| System | Meaning |
| --- | --- |
| Material | The equipment’s current material |
| History | Actions and experience stored on that particular item |
| Potential | The item’s lineage ceiling |
| Evolution | Tiers actually claimed at the anvil station |

A newly created netherite item does not automatically inherit a full history or maximum potential. Existing equipment reforged through its lineage can differ from a newly crafted high-material item.

<a name="page-english-overview-relics"></a>

## Relics

The pack adds ten named relics with short stories and vanilla enchantments. End City treasure chests have a 35% chance of one relic, Ancient Cities 25%, Bastion treasure chests 25% and Desert Pyramids 15%. These are additional rolls when the chest loot is first generated.

Nine compatible relics receive 100 inherited uses or armor experience. The golden axe is a narrative exception. The inherited history does not award paid evolution tiers automatically.

<a name="page-english-overview-compatibility"></a>

## Compatibility

The declared target is stable **Java 1.21–1.21.11**. Version overlays adapt data formats. Smithing and enchanting actions use clickable chat through 1.21.5 and native dialogs from 1.21.6. Earlier copper tool and sword stages use iron base items with Attuned copper identity.

The pack replaces four vanilla chest loot tables. Combining it with another datapack that replaces the same tables requires a merge.

<a name="page-english-overview-known-issues-and-evidence"></a>

## Known issues and evidence

The supplied files contain legacy anvil paths, an armor smithing routing issue, possible chained tome purchases, and scripted durability maintenance that needs a focused in-game check. The bundled villager trade definitions use a registry introduced in Java 26.1 and are not working 1.21.x trade sources merely because their files exist.

The included `VALIDATION.md` still refers to **v0.16.1**. This wiki’s v0.17.1 audit checks the supplied files statically; it does not claim that Minecraft was run or that the previous test suite was repeated.

<a name="page-english-overview-detailed-guides"></a>

## Detailed guides

See [Installation](Installation.md), [Equipment](Equipements.md), [History and progression](Progression-et-histoire.md), [Anvil](Enclume.md), [Smithing](Forge.md), [Enchantments](Enchantements.md), [Relics](Reliques-et-butin.md), [Recipes](Recettes.md), [Resource pack](Resource-pack.md) and [Technical audit](Audit-technique.md).

[Wiki home](Home.md)
