# Netlithic Tokenomics

> Status: experimental devnet. NLT is a devnet test token with no market and no price.
> Nothing in this document is an offer or a promise of any return.

## What the devnet does today

These are the rules the current node software actually enforces:

- **Consensus:** proof-of-work. Difficulty starts at 3 and adjusts every 10 blocks.
- **Issuance:** each mined block pays the miner a fixed **10 NLT** reward.
- **No supply cap:** issuance continues for as long as blocks are mined.
  There is no maximum supply and no halving yet.
- **No pre-mine:** the genesis block contains no transactions. Every NLT on
  the devnet was created by mining.
- **No allocations:** there is no community pool, validator pool, treasury
  or reserve in the code today.
- **Transfers:** Ed25519-signed transactions with nonces, on chain id
  `netlithic-dev-1`.
- **Contribution points:** each node keeps a local counter in
  `state_contributions.json` (10 points per mined block, 1 per sent
  transaction). These points are not on-chain, are not agreed between
  nodes, and cannot be exchanged for NLT.

Devnet NLT is for testing only and may be reset at any time
(see `new_genesis.py`).

## Proposed future design (not implemented)

The following is a design proposal for discussion. None of it exists in
the code yet, and any of it may change.

- A fixed total supply of 1,000,000,000 NLT.
- A proposed split of that supply:

| Category | Share | Tokens |
|--------|--------|--------|
| Community contribution pool | 60% | 600,000,000 |
| Validator rewards | 20% | 200,000,000 |
| Protocol treasury | 15% | 150,000,000 |
| Protocol reserve | 5% | 50,000,000 |

- **Community pool:** intended to reward measurable contributions such as
  running nodes, writing code, reporting security issues and documentation.
- **Validator rewards:** intended for a future validator system. Today the
  devnet has miners, not validators, and there is no staking.
- **Treasury and reserve:** intended for development, grants and security
  audits, with spending decided through a future governance process that
  has not been designed yet.

Moving from the devnet rules to this design would require a new chain or a
documented change to issuance. That decision has not been made.
