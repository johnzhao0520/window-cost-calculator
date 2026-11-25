# Data model

The calculator is deliberately simple: a cost per window built from material and labor components, then scaled by count, stories and state.

```text
material_per_window = sqft × material_$/sqft × complexity + sqft × glass_$/sqft
labor_per_window    = (base_labor + sqft × labor_$/sqft) × complexity + removal_fee
total               = (material_per_window + labor_per_window × story_multiplier) × qty × state_multiplier
range               = total ± 18%
```

## Coefficient sources

| Group | How it was set |
| --- | --- |
| Window type base sq ft and complexity | Typical unit sizes and installation difficulty for each type, from public product and installation price listings |
| Material $/sq ft | Mid-range published prices for standard vinyl, foam-filled, woodgrain vinyl and fiberglass units |
| Glass adders | Published upgrade prices for Low-E and triple-pane assemblies |
| Base labor, per-sq-ft labor, removal fee | Public installer price ranges, mid-point values |
| Story multiplier | 1.00 / 1.12 / 1.28 for 1 / 2 / 3+ stories |
| State multiplier | 0.90–1.28, from regional labor cost differences; 1.00 default |
| Range spread | ±18%, the observed spread of bids around a median for the same job |

The JSON block at the top of `index.html` (`const M = {...}`) is the single source of truth; the page has no other data input.

## Known limits

- One square-footage figure per window type, not per real opening size.
- No frame material for the opening, no trim, no permit, no disposal beyond the removal fee.
- States are multipliers, not county or ZIP data — local bids in a metro can sit well outside the output.
- Data version is frozen at `2026-11` in the model metadata.

For ZIP-level pricing and per-page anchors, use the live site.
