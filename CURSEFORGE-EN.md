<a name="page-curseforge-en"></a>

# Attuned Equipment

**Turn your equipment into companions that grow with your adventures.**

Attuned Equipment is a datapack for **Minecraft Java 1.21.x**. Weapons, tools, armor and shields keep their own history, while special anvils, smithing interactions and enchantment menus offer further progression.

<a name="page-curseforge-en-features"></a>

## Features

- **Equipment history:** track uses, shots, blocks and armor experience on supported items.
- **Forged evolution:** unlock and pay for successive tiers through the Attuned anvil station.
- **Material progression:** reforge supported weapons and tools while carrying their history forward.
- **Custom bows and crossbows:** stone, copper, iron, gold, diamond and netherite variants.
- **Enchantments and knowledge:** discover additional equipment effects and use the custom enchanting interface.
- **Relic treasures:** ten named relics with short stories and vanilla enchantments, found as bonus loot in selected structures.
- **French and English text:** the resource pack follows the client language.

<a name="page-curseforge-en-relic-treasure-locations"></a>

## Relic treasure locations

| Structure chest | Chance of one bonus relic |
| --- | ---: |
| End City | 35% |
| Ancient City | 25% |
| Bastion treasure chest | 25% |
| Desert Pyramid | 15% |

These rolls are made when the chest loot is first generated. Previously opened chests are not repopulated. Nine compatible relics start with 100 inherited uses or armor experience. The golden axe has narrative lore without artificial Attuned progression.

<a name="page-curseforge-en-installation"></a>

## Installation

1. Place the datapack ZIP in your world’s `datapacks` folder.
2. Remove older Attuned editions from that folder.
3. Extract the embedded `resources.zip`, then install and enable it in each player’s `resourcepacks` folder.
4. Reload or restart the world/server.

**The embedded resource pack is not enabled automatically. Every client needs to activate it.**

<a name="page-curseforge-en-compatibility-and-release-notes"></a>

## Compatibility and release notes

This release targets the stable Java versions from **1.21 through 1.21.11**, using version-specific overlays. It does not target Bedrock or Java 26.x.

Before 1.21.6, custom smithing and enchanting actions use clickable chat menus. From 1.21.6 onward, they use native dialogs. Before native copper equipment is available, the copper stage of tools and swords uses an iron base item with Attuned copper identity.

This release overrides four vanilla chest loot tables to add relic pools. Other datapacks overriding the same tables require a merge.

The wiki documents known implementation issues, including armor smithing routes, tome purchase handling and scripted durability maintenance. The bundled villager trade definitions use a registry introduced after 1.21.x and are not advertised as working 1.21.x features. The old v0.16.1 validation notes are not a new in-game validation of v0.17.1.

<a name="page-curseforge-en-documentation"></a>

## Documentation

The project Wiki covers installation, equipment, progression, anvils, smithing, enchantments, recipes, relics, resource-pack behavior and troubleshooting. Consult its known-issues page before updating an established world.

## Useful links

- [Wiki](https://github.com/ldjo86/attuned-equipment-wiki/blob/main/docs/Home.md)
- [Textures and resource pack](https://github.com/ldjo86/attuned-equipment-wiki/blob/main/docs/Resource-pack.md)
- [Known issues](https://github.com/ldjo86/attuned-equipment-wiki/blob/main/docs/Audit-technique.md)
