---
rpip: 
title: Rebalance RPL Inflation for Protocol Funding
description: Increase the pDAO and GMC share of RPL inflation to support protocol funding.
author: Dr Doofus (@DrDoofus-MD-PhD-DDS)
discussions-to:
status: Draft
type: Protocol
category: Core
created: 2026-05-21
requires: RPIP-10, RPIP-25, RPIP-33, RPIP-46, RPIP-68, RPIP-69
vote-to:
vote-date:
vote-result:
tags: [rpl-inflation, saturn-2, node-operator-percent, pdao-percent]
---

## Abstract

This RPIP proposes rebalancing RPL inflation allocation to increase protocol funding during and after the Saturn 2 transition.

Before Saturn 2, the current RPL inflation allocation sends 70% of RPL issuance to Node Operators, 27.5% to the pDAO, and 2.5% to the oDAO. This RPIP would reduce the Node Operator share to 50%, increase the pDAO share to 47.5%, and leave the oDAO share unchanged at 2.5%. This RPIP also updates the internal pDAO allocation policy to 30% IMC, 30% GMC, and 40% Reserve Treasury.

When Saturn 2 takes effect, Node Operator share of RPL inflation is already set to go to zero ([RPIP-46](./RPIP-46.md)). Under the existing Saturn 2 plan, annual RPL inflation would thus fall from 5% to 1.5%. Under this RPIP, elimination of Node Operator RPL rewards will reduce inflation from 5% to 2.5%.

## Motivation

Rocket Pool currently faces a protocol funding shortfall.

The decline in RPL price has greatly reduced the GMC’s funding capabilities. The GMC has already made multiple rounds of cuts to support, administration, business development/STAR, marketing and other recurring expenses. However, current funding is now not enough for basic operating costs and does not provide adequate room for upcoming protocol needs.

The GMC is increasingly asked to fund or help fund items such as support, rescue node costs, business development, Chainlink costs, Saturn 2 related work, Snapshot, and other worthy initiatives. Meanwhile, pDAO funding from megapools is not yet available at meaningful scale and it might be a long time before it becomes helpful at a meaningful level.

Before Saturn 2, 70% of RPL inflation is directed to Node Operator RPL rewards. When Saturn 2 takes effect, those Node Operator RPL rewards will go away entirely. This RPIP proposes a phase out of those rewards pre-Saturn 2 by redirecting part of the current Node Operator RPL issuance to pDAO protocol funding immediately, and to preserve that funding after Saturn 2.


## Specification

### Pre-Saturn 2 RPL Inflation Allocation

Before Saturn 2, this RPIP makes two related changes:

1. It changes the RPL inflation allocation from:

```
   Node Operators: 70%
   pDAO:           27.5%
   oDAO:            2.5%
```

   to:

```
   Node Operators: 50%
   pDAO:           47.5%
   oDAO:            2.5% (unchanged)
```

2. It changes the internal pDAO allocation policy from:

```
   IMC:              50%
   GMC:              25%
   Reserve Treasury: 25%
```

   to:

```
   IMC:              30%
   GMC:              30%
   Reserve Treasury: 40%
```

This approximately doubles the GMC RPL and bolsters the reserve treasury by about 10,000 RPL per cycle.

#### RPL Inflation Allocation Implementation

- These pre-Saturn 2 changes **SHALL** be implemented via the on-chain pDAO proposal system using the rewards-percentages as follows (values are given as a fraction between 0 and 1):

```
Node Operators (rocketClaimNode):        0.5
pDAO (rocketClaimDAO):                   0.475
oDAO (rocketClaimTrustedNode):           0.025
```

- This change **SHOULD** be submitted via the Smartnode CLI command: `rocketpool pdao propose rewards-percentages`

#### pDAO Allocation Implementation

After the above changes are active, the pDAO allocation policy ([RPIP-10](./RPIP-10.md)) **SHALL** be modified and implemented as follows:

```
IMC = 30%
GMC = 30%
Reserve Treasury = 40%
```

### Post-Saturn 2 RPL Inflation Allocation

When Saturn 2 takes effect, Node Operator RPL issuance will still be eliminated as planned in accordance with [RPIP-46](./RPIP-46.md) and the oDAO and pDAO issuance will remain the same as the above changes dictate. This means the post-Saturn 2 pDAO/oDAO allocation percentages remain consistent with the 95%/5% DAO split specified in [RPIP-46](./RPIP-46.md), while the absolute issuance reflects the pre-Saturn 2 oDAO share established by [RPIP-68](./RPIP-68.md):

```
Node Operators:       0%
pDAO:                 95%
oDAO:                 5%
```

However, instead of reducing annual RPL inflation from 5% to 1.5%, annual RPL inflation will be reduced from 5% to 2.5% (simply the effect of eliminating the 50% Node Operator share).

#### Post-Saturn 2 RPL Inflation Implementation

Post Saturn 2, annual RPL inflation will be changed as follows:

- [RPIP-46](./RPIP-46.md) **SHALL** be amended to change RPL inflation from 1.5% to 2.5%.
- `rpl.inflation.interval.rate` **SHALL** be set to the value corresponding to 2.5% annual inflation using the same annualization convention as [RPIP-46](./RPIP-46.md). The expected value is approximately `1000067606974065369`, subject to technical confirmation.

Note that inflation can be further reduced in the future if circumstances dictate, but it might be a greater challenge to raise inflation after Saturn 2 from 1.5% if further funding is needed than to reduce it if it is not.


## Rationale

### Protocol funding need

The GMC’s current funding stream is insufficient at current RPL prices. The GMC has already reduced spending, but continued austerity has limits. Further cuts to support, administration, committee work, and contributor compensation risk weakening the protocol and losing contributors who are already working for modest compensation.

This RPIP is based on the view that Rocket Pool should not solve a structural protocol funding issue only by further reducing compensation to people actively maintaining and improving the protocol.

### Node Operator RPL issuance is already transitional

Node Operator RPL issuance rewards are already expected to end with Saturn 2. This RPIP does not create a new long-term direction for Node Operator RPL rewards. Rather, it starts the transition earlier by reducing the Node Operator RPL rewards before Saturn 2, while still preserving a meaningful share until Saturn 2 takes effect.

### Timing matters

This proposal is time-sensitive because the current Node Operator RPL share only exists before Saturn 2. If no change is made before Saturn 2, then the 70% Node Operator share remains in place until Saturn 2 and then disappears. At that point, the protocol would need a separate future vote to increase inflation again if pDAO funding from megapools is not sufficient.

### pDAO funding from megapools is not yet sufficient

A future pDAO share from megapools may become an important protocol funding source. However, that source is not yet available at meaningful scale. The protocol needs funding during the period before Saturn 2 and may continue to need this RPL funding after Saturn 2 if `pdao_share` is insufficient.

### Minipool operator expectations

A potential concern is that reducing Node Operator RPL rewards before Saturn 2 changes expectations for current minipool operators. This concern should be weighed seriously. However, the reduction affects RPL issuance rewards, not ETH rewards. It also occurs in the context of an already-planned transition away from Node Operator RPL issuance rewards in Saturn 2. The proposal preserves 50% of RPL issuance for Node Operators before Saturn 2 while redirecting the remaining portion towards the pDAO.

### RPL value and inflation tradeoff

This RPIP would result in higher post-Saturn 2 RPL inflation than currently specified in [RPIP-46](./RPIP-46.md). The existing Saturn 2 plan reduces annual RPL inflation to 1.5%; this RPIP would instead reduce it to 2.5%.

Higher inflation can be harmful to RPL value if the additional RPL is spent inefficiently or sold into shallow demand. This proposal accepts that risk because underfunding core protocol needs can also harm RPL value by weakening support, development, growth, and contributor retention.

The intended tradeoff is not "more inflation forever." It is to preserve protocol funding during a period where other funding sources, including `pdao_share`, may not yet be sufficient. If protocol revenue or treasury conditions improve, future governance can reduce inflation or revise the pDAO allocation policy.

## Security Considerations

This RPIP does not change ETH rewards, validator duties, minipool delegate behavior, megapool mechanics, or validator security assumptions.

The primary risks are economic, governance, and incentive risks:

1. **Node Operator expectations:** Reducing Node Operator RPL issuance before Saturn 2 may be perceived as changing the expected transition for current minipool operators.
2. **RPL value and sell pressure:** Increasing the pDAO share and preserving higher inflation than [RPIP-46](./RPIP-46.md) currently specifies, may increase sell pressure if the additional RPL is spent quickly or inefficiently.
3. **Treasury discipline:** Larger pDAO, GMC, and Reserve Treasury inflows do not by themselves guarantee better outcomes. Poor budgeting or weak grant oversight could waste the additional issuance.
4. **Underfunding risk:** If this RPIP does not pass and no alternative funding source is available, Rocket Pool may underfund support, operations, security related work, Saturn 2 work, contributor retention, and growth initiatives.

This RPIP attempts to balance those risks by:

- preserving 50% of RPL rewards for Node Operators before Saturn 2,
- eliminating Node Operator RPL rewards at Saturn 2 as already planned,
- keeping GMC, IMC, and Reserve Treasury spending subject to normal governance and budgeting processes, and
- leaving future governance able to reduce inflation or revise allocations if the additional funding is no longer needed.

## Governance Considerations

This RPIP modifies RPL inflation allocation and therefore requires a 75% "For" supermajority under [RPIP-25](./RPIP-25.md).

Passage of this RPIP should be treated as authorization for three related governance actions:

1. A pre-Saturn 2 onchain pDAO proposal to change RPL claim percentages to 50% Node Operators, 47.5% pDAO, and 2.5% oDAO.
2. An update to the pDAO allocation policy in [RPIP-10](./RPIP-10.md) to set IMC to 30%, GMC to 30%, and Reserve Treasury to 40%.
3. An amendment to [RPIP-46](./RPIP-46.md) so that the Saturn 2 `rpl.inflation.interval.rate` target is 2.5% annual inflation rather than 1.5%.

This RPIP changes funding allocation and inflation policy. It does not approve any specific GMC grant, IMC incentive program, Reserve Treasury spend, or other individual expenditure.


## Copyright

Copyright and related rights waived via [CC0](https://creativecommons.org/publicdomain/zero/1.0/).
