# BitVault Staking Protocol

**BitVault** is a decentralized staking and governance protocol purpose-built for the Bitcoin Layer 2 ecosystem. Designed with security, scalability, and user empowerment at its core, BitVault enables STX token holders to stake assets, earn tiered rewards, and actively participate in protocol governance — all while preserving system integrity through robust safeguards and emergency controls.

## Key Features

* **STX Staking with Lock Incentives**
  Users can stake STX tokens with optional time-lock periods to boost rewards. The longer you lock, the higher your multiplier — up to 2x in rewards.

* **Tiered Reward System**
  Tier levels based on stake amount unlock additional multipliers and protocol features. Current tiers:

  * **Tier 1**: 1M STX – 1x Rewards
  * **Tier 2**: 5M STX – 1.5x Rewards
  * **Tier 3**: 10M STX – 2x Rewards

* **Decentralized Governance**
  Stakeholders with sufficient voting power can create and vote on governance proposals, helping shape the protocol’s evolution.

* **Emergency Controls**
  Includes safety mechanisms like contract pausing and cooldown-based unstaking to protect the protocol and its users from malicious or unintended actions.

* **Transparent Analytics Token**
  A placeholder for future integration of an `ANALYTICS-TOKEN` that may represent governance weight, reward eligibility, or analytical insights.

## Contract Overview

| Component            | Description                                       |
| -------------------- | ------------------------------------------------- |
| **Token**            | Defines a fungible `ANALYTICS-TOKEN`              |
| **UserPositions**    | Tracks staking, voting power, and tier data       |
| **StakingPositions** | Records stake details including lock and cooldown |
| **TierLevels**       | Defines reward tiers and feature access           |
| **Proposals**        | Governance structure for community decisions      |

## Core Functions

### Initialization

```clarity
(initialize-contract)
```

Sets up the contract's tier structure and initial protocol state. Only callable by the contract owner.

### Staking

```clarity
(stake-stx (amount uint) (lock-period uint))
```

Stake STX with optional lock periods (0, 1 month, or 2 months). Rewards are tiered by stake size and lock time.

### Unstaking Flow

1. Initiate unstaking:

   ```clarity
   (initiate-unstake (amount uint))
   ```
2. Complete unstaking after cooldown (\~24h default):

   ```clarity
   (complete-unstake)
   ```

### Governance

* **Create Proposal**

  ```clarity
  (create-proposal (description string) (voting-period uint))
  ```
* **Vote on Proposal**

  ```clarity
  (vote-on-proposal (proposal-id uint) (vote-for bool))
  ```

## Emergency & Admin Functions

* **Pause Contract**
  Temporarily disables core functions.

  ```clarity
  (pause-contract)
  ```

* **Resume Contract**
  Reactivates the protocol.

  ```clarity
  (resume-contract)
  ```

## Read-Only Queries

* `get-contract-owner` – Returns contract owner address
* `get-stx-pool` – Total STX currently staked
* `get-proposal-count` – Number of proposals created

## Reward Calculation

Rewards are calculated per block using:

```
rewards = (stake-amount × base-rate × reward-multiplier × blocks) / 14400000
```

Where:

* `base-rate` = 5% (default)
* `reward-multiplier` = Tier × Lock period
* 1 block ≈ 30 seconds

## Security and Compliance

* **Cooldown Periods**: Prevent instant withdrawals and front-running.
* **Emergency Mode**: Ensures controlled halts during critical protocol risks.
* **Tier-based Access**: Enables progressive unlocking of features based on user commitment.

## Prerequisites

* Clarity SDK / Stacks blockchain environment
* STX tokens for staking
* Access to a Clarity-compatible wallet or deployment environment (e.g., Clarinet)

## Example Usage

```lisp
;; Initialize contract
(initialize-contract)

;; Stake 2M STX with 1-month lock
(stake-stx u2000000 u4320)

;; Propose a new governance change
(create-proposal "Enable new feature X" u200)

;; Vote in favor of proposal 1
(vote-on-proposal u1 true)
```

## Contributions

Want to contribute? Feel free to fork, improve, or extend the BitVault protocol. Ideas for reward mechanisms, tier structures, or analytics integration are welcome!

## 🧭 Roadmap Highlights

* ✅ Tiered staking system
* ✅ Governance proposals
* 🚧 Reward claiming + compounding
* 🚧 `ANALYTICS-TOKEN` utility
* 🚧 UI dashboard integration

---

**Built with love for the Bitcoin Layer 2 community.**
*Secure. Scalable. Stakeworthy.*
