# PF2e Rule Element Forge

Builds a proper form for every pf2e rule element, right on the item sheet's
Rules tab — no more hand-writing raw JSON to make a rule work.

## Install

**The easy way (Windows):** download the [SpazzMods Installer](https://github.com/Spazzletopia-Studios/spazzmods-installer/releases/latest),
run it, and click Install on PF2e Rule Element Forge. No account needed.

**Without the installer:** paste this into Foundry's **Install Module →
Manifest URL** box:
`https://github.com/Spazzletopia-Studios/pf2e-rule-element-forge/releases/latest/download/module.json`

## Using it

- Open any item's **Rules** tab. Next to every existing rule, and next to
  the **New** button, there is a wand icon — click it.
- The window builds a real form for whatever rule element you picked, with
  every field it actually takes, instead of a raw JSON box.
- Predicates (the conditions that gate a rule) get their own builder with
  rows you fill in, instead of hand-written logic.
- The draft is checked as you edit, and the **Apply** button stays disabled
  until the rule is valid — so you cannot save something broken.
- Stuck on what values to use? Search the compendiums for a real item using
  the same rule element and load it as a starting point.

---

A form editor for every pf2e rule element, on the item sheet's Rules tab.

Replaces the **PF2e Rule Element Generator** by Bolt, which stopped being
maintained in September 2022 and no longer works: it was written for Foundry v10
and hooks DOM elements (`a.edit-rule-element`, `a.add-rule-element`) that pf2e
removed several majors ago, so on a current install it shows no buttons at all.

## What it does

Open any item's **Rules** tab. Next to every existing rule, and next to the
**New** button, there is a wand. It opens a window with:

- **A form built from the live schema.** Every pf2e rule element is a Foundry
  DataModel with a declared schema, and this reads that schema at runtime. All
  40 rule elements (the same 40 in pf2e 7.12.2 and 8.x) get a form, including the 26 that pf2e itself
  only offers as a raw JSON box. Nothing is hardcoded, so a pf2e update that
  adds a rule element or changes a field needs no update here.
- **A predicate builder.** Rows for roll options, `not`, groups (`and`, `or`,
  `nand`, `nor`, `xor`, `iff`), numeric comparisons (`eq`, `gt`, `gte`, `lt`,
  `lte`) and `if`/`then`, nested to any depth. The roll-option boxes autocomplete
  from the item's and the actor's real roll options — the same list pf2e's own
  "View Roll Options" button shows.
- **Live validation.** The draft is run through the actual pf2e rule element
  class on every edit and any validation failure is shown before you save. Apply
  stays disabled until the rule is valid.
- **Examples from the compendiums.** Search real pf2e items that use the rule
  element you are editing and load one as a starting point.

## Requirements

- Foundry VTT 13 with the pf2e system 7.12.2 (the 7.x version this release was
  tested with), or Foundry VTT 14 with pf2e 8.x (tested with 8.5.0). Both lines
  register the same 40 rule elements; the fields of each form are the ones your
  installed pf2e declares.
- The Rules tab must be visible to you — pf2e gates it behind the
  **Minimum Role for Rules UI** system setting.

## Settings

| Setting | Scope | Default |
| --- | --- | --- |
| Block Apply while a rule is invalid | world | on |
| Expand advanced fields by default | client | off |
| Compendiums searched for examples | world | six pf2e SRD packs |

## API

```js
game.pf2eRuleElementForge.open(item, { index: null, key: "FlatModifier" });
game.pf2eRuleElementForge.keys();
```

`item` may be a document or a UUID. `index` selects an existing rule to edit;
omit it to build a new one.

## Checking it works

With a world loaded, paste this into the browser console (F12):

```js
(await import("/modules/pf2e-rule-element-forge/scripts/smoke.js")).run()
```

It walks every rule element the installed pf2e has, builds and renders each
form (a field that fell back to a JSON box is reported), checks the validator
rejects a bad `priority` for every one of them, and checks it accepts a
known-good rule and rejects broken ones. It reads only — nothing is written to
the world.

## Notes

- Rules are read from and written to the item **source** (`item.toObject()`),
  never the prepared `item.system.rules`, so applying a rule cannot corrupt the
  item with system-built objects.
- Opening an existing rule and pressing Apply writes back exactly that rule.
  A schema default shown in a control you did not touch is not written, an
  object or list in a value box is kept as written, and a key your PF2e version
  has no field for is kept as written too (since 1.1.0).
- Predicates are written in the modern array form. The module this replaces
  emitted the pre-4.x `{ all, any, not }` object, which today fails validation
  on every rule it writes.

## License

MIT.

## Get help

[Get Help](https://github.com/Spazzletopia-Studios/spazzmods-support) — report a bug, get install help, ask a question, or suggest an idea.
