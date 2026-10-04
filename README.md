# PF2e Rule Element Forge

## Purpose and features

Rule Element Forge gives item authors a form editor for PF2e rule elements. It reads the rule element schemas from the installed PF2e system, builds a predicate editor, validates drafts, and can load working examples from compendiums.

## Setup

Foundry VTT 13 with PF2e 7.12.2 or newer 7.x, or Foundry VTT 14 with PF2e 8.x. The manifest sets Foundry minimum 13 and maximum 14; it was verified with PF2e 8.5.0.

This is a free module. Install it with the [SpazzMods Installer](https://github.com/Spazzletopia-Studios/spazzmods-installer/releases/latest), or use the [public GitHub release](https://github.com/Spazzletopia-Studios/pf2e-rule-element-forge/releases/latest). Enable **PF2e Rule Element Forge** in Manage Modules.

You need permission to edit the item, and the PF2e **Rules** tab must be visible to your role. PF2e controls the minimum role for that tab.

## Quick start

1. Open an editable item sheet and select **Rules**.
2. Click the wand next to **New** to make a rule, or the wand on an existing rule to edit it.
3. Choose the rule element type. Add values with the form and build any predicate rows.
4. Check the live validation messages and use **Examples** to find a real compendium item if needed.
5. Click **Apply** when the rule is valid.

## Detailed use

The editor reads each field from the live PF2e rule-element schema. It includes a predicate builder for roll options, negation, groups, comparisons, and if/then conditions. Roll-option suggestions come from the actor and item. The draft is checked by the installed PF2e rule class; **Apply** stays unavailable while it is invalid.

The example search looks for compendium items that use the selected rule. Examples are starting points, not a guarantee that the rule will work on every actor or item. PF2e still evaluates the saved rule.

When you edit a rule, Forge works with the item's source data, not PF2e's prepared rule objects. It preserves untouched defaults, structured values, and keys unknown to the installed schema. Predicates are saved in the modern array format. The editor does not grant permission to edit the item or bypass PF2e's Rules-tab role limit.

## Settings

- **Block Apply while a rule is invalid** — world, on by default.
- **Expand advanced fields by default** — client, off by default.
- **Compendiums searched for examples** — world, six PF2e SRD packs by default.

## Limits and recovery

A valid form only proves the draft passes the installed rule-element validator. Review the item's behavior in PF2e and test it on the intended actor. If the Rules tab or wand controls are absent, check item ownership/edit permission and the PF2e minimum role setting. Some keys are not declared by the installed schema; Forge preserves them when editing the existing rule but does not show an editable field for them.

## API and development

`game.pf2eRuleElementForge.open(item, { index: null, key: "FlatModifier" })` opens a new rule editor. `game.pf2eRuleElementForge.keys()` lists supported rule keys. Pass a document or UUID; use `index` to edit an existing rule.

A read-only in-world smoke is available at `/modules/pf2e-rule-element-forge/scripts/smoke.js`. The harness gate can be run with `node run-all.mjs` from the module's `harness/` directory.

## Credits and license

MIT License. Author: Spazz. This module replaces the obsolete PF2E Rule Element Generator.

## Get help

[SpazzMods Support](https://github.com/Spazzletopia-Studios/spazzmods-support).
