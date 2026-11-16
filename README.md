# Michigan rate model

What would the federal permitting bill (BAAJA, S. 5653) mean for electric bills in Michigan, and could data centers be made to pay for the state's new transmission lines?

This is a bill-impact model for DTE Electric, built from figures already filed in Michigan Public Service Commission dockets and published by MISO. It compares three worlds:

- **A.** No federal bill.
- **B.** The bill passes and Michigan does nothing more.
- **C.** The bill passes and Michigan enacts a statute that charges data centers an adder above the standard rate and credits it to other customers.

Author: Collin Parks, University of Michigan Law School.

## What I found

BAAJA's ratepayer provisions are usually read as a shield: data centers may not push their costs onto everyone else. Read with section 229(b)(2), they are also a lever. A State may charge a data center more than it costs to serve and credit the difference to other customers, and in Michigan the numbers are not small.

Some of this happens already. A data center on DTE's standard rate pays more than it costs to serve, and because the Commission sets rates to cover DTE's total costs, the difference lowers everyone else's bills at the next rate case. On the figures in the record, the two contracts already approved, Saline and Van Buren, are worth roughly $78 to $92 a year to a DTE household.

New load adds to that. Take 2 GW more, a $10 per MWh charge credited back per kWh, and the lowest estimate in the record of what standard rates contribute (MPSC Staff's). A household comes out about $16 a year ahead with no federal bill, $24 under the federal bill alone, and $58 under the federal bill plus a Michigan statute, after allowing for data centers that build their own gas plants instead. That $58 is close to the $61 a year each household will owe for MISO's new regional lines.

That the charge works does not mean it can go anywhere. It works only if the load stays, and a statute can make one exit harder (building gas plants on site) but cannot close the other (building in Ohio). The explorer lets the charge run to $70 per MWh; the defaults are the version I would defend.

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

The explorer is live at https://parksgc.github.io/michigan-rate-model/ and the figures at https://parksgc.github.io/michigan-rate-model/figures/.

## Results at the default settings

Defaults: 2 GW of new data center load on DTE's system, a $10 per MWh adder credited per kWh to all other customers, and MPSC Staff's Van Buren figure for what standard rates already contribute.

| | World A | World B | World C |
|---|---|---|---|
| Credit to a DTE household, dollars a year | $20 | $30 | $61 |
| Share of other customers' line bill covered | 28% | 46% | 97% |

- The line bill is DTE's other customers' share of MISO's Tranche 1 and 2.1 lines: about $305 million a year, or $61 a household, at the central cost.
- The household credit in world C is 3.9% of the average residential bill.
- The explorer opens with exit to on-site gas counted, so its starting numbers are a little lower: $58 a household and about 91% of the line bill in world C.
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
- 463 workbook cells were recomputed independently in Python: 0 mismatches.
- 37 tests change one dial at a time and check a property the logic requires (for example, with the adder at zero, world C equals world B).
- The explorer's arithmetic was compared with the workbook at thirteen dial settings: 252 comparisons, 0 mismatches.
- What the explorer prints (the four numbers, the sentence, the buttons) was checked against the workbook: 94 checks, 0 mismatches.
- A separate pass re-derived headline figures from the sources without seeing the workbook. It reproduced MPSC Staff's $5.46 per MWh and the central line cost ($7.48 against the model's $7.49). It could not reach DTE's rate case exhibits, the Saline order or the Grid Strategies paper, so those inputs rest on a second, non-blind reading.
- Eight of ten published figures the model should reproduce fall within 15%. The two that do not are DTE's separate claims for Saline and Van Buren; the model reproduces their sum.

## Limits

- **DTE Electric only.** Consumers Energy is not modeled.
- **A snapshot, not a forecast.** Results are for full load on DTE's 2029 study year, not a path by year.
- **The step from world A to world B is mostly the federal transmission charge.** Michigan's own orders already forbid a subsidy, so the bill's retail floor adds little here. What world B adds is section 2107(a)'s charge for new transmission, estimated from Grid Strategies' MISO-wide figure. FERC has not written that rule, and part of it may overlap with upgrade costs Michigan already assigns to data centers directly.
- **The central contribution figure is a deliberate low.** MPSC Staff's Van Buren figure ($5.46 per MWh) is the lowest positive number in the record, and the Commission did not adopt it or any other figure. DTE's own studies put the contribution at $21.58. Staff's figure is a 20-year total divided evenly by year, not a present value, and if Staff assumed Google pays only its minimum bill, the per-MWh figure would be about $6.14. The residential share applied to it comes from DTE's cost studies, a different source.
- **The line cost mixes dollar years.** Tranche 1's cost is in 2022 dollars and Tranche 2.1's in 2024 dollars. Restating Tranche 1 would raise the line bill by about 3%, so the coverage figures run slightly high.
- **The exit module is assumed.** Nothing anchors the share of data centers that build their own gas plants. The assumed curve treats speed as the main reason to leave the grid, so the adder moves it little: with on-site gas left open, 20% leave at no adder and about 30% at $40.
- **Load that goes to another state is a dial, set to zero.** Nothing in the record measures it, and the model legislation cannot close that exit. With it at zero, a large adder looks better than it should; turn it up in the explorer or on the workbook's Scenarios tab.
- **None of the money is earmarked for the lines.** The line bill is a yardstick for scale. Contribution and the federal charge lower other customers' bills generally.
- **Per-household figures mix years** (2029 energy over a 2025 customer count) and run 1 to 2% high.
- **Some inputs come from summaries or secondary sources**, including the residential customer count, the carbon capture cost and the social cost of carbon. The Inputs tab marks each.
- The Union of Concerned Scientists' Michigan emissions figure could not be reconciled with the model's rates.
