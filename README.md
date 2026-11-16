# Michigan rate model

What would the federal permitting bill (BAAJA, S. 5653) mean for electric bills in Michigan, and could data centers be made to pay for the state's new transmission lines?

This is a bill-impact model for DTE Electric, built from figures already filed in Michigan Public Service Commission dockets and published by MISO. It compares three worlds:

- **A.** No federal bill.
- **B.** The bill passes and Michigan does nothing more.
- **C.** The bill passes and Michigan enacts a statute that charges data centers an adder above the standard rate and credits it to other customers.

Author: Collin Parks, University of Michigan Law School.

## What is here

| Path | What it is |
|---|---|
| `index.html` | The interactive explorer. Pick a world and move the dials |
| `figures/index.html` | Figures 1 to 10, with a black-and-white view |
| `figures/figures_print.pdf` | The ten figures in black and white, one per page |
| `figures/print_bare/` | Black-and-white PNGs, chart and legend only |
| `figures/print_full/` | Black-and-white PNGs with title, note and source line |
| `figures/color_full/` | Color PNGs with title, note and source line |
| `workbook/Michigan_rate_model_DTE.xlsx` | The model. Every result is a live formula; every input carries its source |

If GitHub Pages is turned on for this repository, the explorer is the home page and the figures are at `figures/`.

## Results at the default settings

Defaults: 2 GW of new data center load on DTE's system, a $10 per MWh adder credited per kWh to all other customers, and MPSC Staff's Van Buren figure for what standard rates already contribute.

| | World A | World B | World C |
|---|---|---|---|
| Credit to a DTE household, dollars a year | $20 | $30 | $61 |
| Share of other customers' line bill covered | 28% | 46% | 97% |

- The line bill is DTE's other customers' share of MISO's Tranche 1 and 2.1 lines: about $305 million a year, or $61 a household, at the central cost.
- The household credit in world C is 3.9% of the average residential bill.
- The result moves most with two things the statute does not control: how much load arrives, and what that load contributes at standard rates.

## How it works

The workbook has five modules.

1. **Surplus.** What a megawatt-hour sold to a data center pays above its cost, from DTE's cost-of-service studies in Case U-22046, and what reaches other customers in each world.
2. **Lines.** The cost of MISO's new regional lines to DTE's other customers, and how much of it new load covers.
3. **Exit.** How many data centers would leave for on-site gas as the adder rises, with and without limits on that exit. This module is assumed, not estimated.
4. **Gas.** Other groups' estimates of the bill's effect on gas prices, applied to a household that heats with gas.
5. **Emissions.** CO2 per gigawatt by who supplies the power.

Three kinds of money are kept apart throughout: the incremental cost of serving a data center (the federal floor), the contribution it makes above that cost at standard rates, and the adder a state statute would add on top.

## Sources

Each input row on the workbook's Inputs tab names its source and page. The main ones:

- DTE Electric, exhibits and application in MPSC Case U-22046 (cost-of-service studies, large-load billing figures, class revenues).
- MPSC orders in Case U-21990 (Saline) and Case U-22058 (Van Buren).
- MISO, MTEP24 and the LRTP Tranche 1 business case (line costs).
- Grid Strategies, "Grid Funding from Data Centers in BAAJA" (the federal transmission charge).
- ICF, Rhodium Group, the Department of Energy and Energy Innovation (gas price cases).
- EIA and EPA eGRID (heat rates and emission rates); Rabobank, Modo Energy and NETL (on-site gas and carbon capture costs).

## How it was checked

- The inputs behind Modules 1 and 2 were read a second time from the dockets and MISO documents and matched.
- 462 workbook cells were recomputed independently in Python: 0 mismatches.
- 33 tests change one dial at a time and check a property the logic requires (for example, with the adder at zero, world C equals world B).
- The explorer's arithmetic was compared with the workbook at eight dial settings: 152 comparisons, 0 mismatches.
- Eight of ten published figures the model should reproduce fall within 15%. The two that do not are DTE's separate claims for Saline and Van Buren; the model reproduces their sum.

## Limits

- **DTE Electric only.** Consumers Energy is not modeled.
- **A snapshot, not a forecast.** Results are for full load on DTE's 2029 study year, not a path by year.
- **The step from world A to world B is uncertain.** World A lets a shortfall from new load fall on other customers. Michigan's own orders already forbid a subsidy, so the federal floor may add less than shown.
- **The central contribution figure is a choice.** Staff's Van Buren figure ($5.46 per MWh) is the lowest positive number in the record. DTE's own studies put it near $22.
- **The exit module is assumed.** Nothing anchors the share of data centers that leave, and load that goes to another state is not modeled. A large adder will look better here than it should.
- **Per-household figures mix years** (2029 energy over a 2025 customer count) and run 1 to 2% high.
- **Some inputs come from summaries or secondary sources**, including the residential customer count, the carbon capture cost and the social cost of carbon. The Inputs tab marks each.
- The Union of Concerned Scientists' Michigan emissions figure could not be reconciled with the model's rates.
