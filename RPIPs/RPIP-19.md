---
rpip: 19
title: oDAO Health Clarity
description: Short and long term improvements for oDAO health clarity
author: Valdorff (@Valdorff)
discussions-to: https://dao.rocketpool.net/t/make-odao-health-clearer/1658/6
status: Final
type: Protocol
category: Core
created: 2023-04-17
---


## Abstract
Clearer oDAO performance metrics will help oDAO members better take action to improve when
warranted, and also allow for monitoring and accountability (from both other oDAO members and the
community at large).

## Motivation
The current voting method for automated duties, where oDAO members stop voting once consensus is
reached, makes it difficult or impossible to tell if oDAO nodes are working properly based on
performance data. This is true for the greater community and even true for the oDAO members
themselves.

## Specification
- In the short term, the watchtower SHALL implement a voting scheme that will show each oDAO member
  can submit balances at least once a week
- In the short term, the watchtower SHALL implement a voting scheme that will show each oDAO member
  can submit prices at least once a week
- In the medium term, the watchtower SHOULD implement a voting scheme that will show each oDAO
  member can generate a correct merkle tree; this MAY have a moderate timeout to avoid degrading NO
  experience much
- The next significant smart contract release SHALL allow for voting past consensus

## Reference Implementation
### Subcommittees for balance and price duties
This change can be implemented now in the watchtower.

Each oDAO node figures out its index (similar code already exists). On an even update
`((current_update_block - first_update_block) / blocks_between updates) % 2 == 0`, nodes with even
indices submitBalances right away but only submitPrices after waiting X minutes. On an odd update,
nodes with odd indices submitBalances right away but only submitPrices after waiting 10 minutes.
Nodes should do the work immediately and hold off on voting, to avoid unnecessary delay when
submitting after their 10-minute wait. Note: consensus currently requires more than half of votes,
so this approach will often mean we must hit the 10-minute wait before consensus is possible.

### Subcommittee for reward snapshot duty
This change can be implemented now; however, trees currently take a long time and the subcommittee
approach works using generous buffers. As a result, it's recommended that this change be implemented
after trees are reliably fast enough in the watchtower such that this approach doesn't degrade NO
experience significantly.

Each oDAO node figures out its own index (similar code already exists). On an even rewards period,
nodes with even indices submitRewardSnapshot right away, and nodes with odd indices should only
submitRewardSnapshot after waiting 30 minutes. On an odd rewards period, nodes with odd indices
submitRewardSnapshot right away, and nodes with even indices should only submitRewardSnapshot after
waiting 30 minutes. Nodes should do the work immediately and hold off on voting to avoid
unnecessary delay when submitting after their 30-minute wait. Note: consensus currently requires
more than half of votes, so this approach will often mean we need to hit the 30-minute wait before
consensus is possible.

It should be explicitly noted that isolated failures are not cause for alarm, and there are simply
not many data points. The oDAO may wish to conduct an internal test with a member who didn't submit
in the active subcommittee.

### Voting past consensus
This change requires a smart contract release.

#### submitPrices()
- Change > to >= in `require(_block > getPricesBlock(), "Network prices for an equal or higher block are set");`
  - Update message to say "for a higher block"
- After emitting `PricesSubmitted`, return early if this is a vote on something already executed
  - `if (_block == getPricesBlock()) { return; }`

#### submitBalances()
- Change > to >= in `require(_block > getBalancesBlock(), "Network balances for an equal or higher block are set");`
  - Update message to say "for a higher block"
- After emitting `BalancesSubmitted`, return early if this is a vote on something already executed
  - `if (_block == getBalancesBlock()) { return; }`

### submitRewardSnapshot()
- Change == to <= in `require(_submission.rewardIndex == getRewardIndex(), "Can only submit snapshot for next period");`
  - fix message to "Can only submit snapshot for periods up to next"
- Change >= to == in `if (calcBase.mul(submissionCount).div(rocketDAONodeTrusted.getMemberCount()) >= rocketDAOProtocolSettingsNetwork.getNodeConsensusThreshold())`
- After emitting `RewardSnapshotSubmitted`, return early if this is a vote on something already executed
  - `if (_submission.rewardIndex != getRewardIndex()) { return; }`

## Security Considerations
For the watchtower-side interventions, security is not being changed.

For the smart contract interventions, care must be taken to avoid introducing bugs, such as multiple
execution possibilities.

## Copyright
Copyright and related rights waived via [CC0](https://creativecommons.org/publicdomain/zero/1.0/).
