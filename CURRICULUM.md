# Curriculum: Becoming a Blockchain Solution Architect by Building Real Systems

Each module is one real system, taken through the full lifecycle in `MENTOR_INSTRUCTIONS.md` (framing, requirements, HLD, LLD, implementation, security review, operations, v2). Systems get harder, and each one introduces the architect concepts it naturally needs. Rough durations assume 6 to 8 hours per week.

The mentor may reorder or skip modules based on the learner profile and domain interest, but the lifecycle discipline stays the same.

---

## Stage 0: Foundations bootcamp (L0 to L1), for learners who have not deployed a contract yet

Goal: go from "I have followed tutorials" to "I can build, test and deploy a small contract on my own, and explain what happens on-chain". Each mini-build is small and done by the learner at the keyboard, with the mentor reviewing rather than writing.

### Module 0. Your first on-chain system: a shared tip jar (2 to 3 weeks)
**Brief.** A small group shares a tip jar contract. Anyone can tip in ETH; only the owner can withdraw; everyone can see the total and the last 10 tippers' messages.
**Steps (one session each, roughly):**
1. **How Ethereum works, by watching it.** Wallets, keys and addresses; transactions, gas and blocks; looking up a real transaction on Etherscan and decoding what happened. Set up MetaMask with a test account, get Sepolia test ETH from a faucet. No code yet.
2. **Toolchain setup.** Install Foundry; `forge init`; tour of the project; compile, run the sample test, run a local chain with `anvil`. The learner explains each folder back to the mentor.
3. **Solidity for a Java/TypeScript developer.** Mapping from what they know: contracts vs classes, `mapping` vs `HashMap`, value types, `msg.sender`/`msg.value`, `require`/custom errors vs exceptions, events vs logging, why there is no `null` and no floating point, why storage writes cost money.
4. **Build the tip jar (learner writes it).** Mentor gives the spec and the first failing test; the learner writes the contract until tests pass, then writes their own tests (including "non-owner cannot withdraw").
5. **Break it.** Mentor shows a deliberately vulnerable withdraw (reentrancy) and an unbounded-array DoS; the learner writes a test that exploits each, then fixes them.
6. **Ship it.** Deploy to Sepolia with a Foundry script, verify on Etherscan, call it from a tiny TypeScript script with viem, and read the events back.
7. **First design doc.** Write a one-page requirements + HLD for the tip jar using the templates, after the fact, so the lifecycle feels familiar before Module 1.

**Exit check (to pass L1):** Without help, explain gas, storage cost, `msg.sender`, events and finality; write, test and deploy a contract from a short spec; find the bug in a 20-line contract.

---

## Stage A: Foundations through a first real system (L1 to L2)

### Module 1. Freelance escrow with dispute resolution (2 to 3 weeks)
**Brief.** A client pays a freelancer through escrow. Funds release on approval, refund on cancellation before work starts, or go to an arbiter on dispute. Supports ETH and one stablecoin.
**Concepts introduced.** Accounts and transactions, gas and storage costs, the contract state machine, access control, checks-effects-interactions, reentrancy, pull-over-push payments, ERC-20 and `SafeERC20`, events, Foundry unit and fuzz tests, testnet deployment.
**Architect lens.** "Do you need a blockchain?" analysis. Who is trusted (the arbiter) and how to constrain them. What is immutable.
**Deliverables.** Requirements, a short HLD, LLD of one contract with a state diagram, contract plus tests, deployed on a testnet.

### Module 2. Token launch: ERC-20 with vesting and an airdrop (2 weeks)
**Brief.** A startup issues a token with team/investor vesting schedules and a Merkle-proof airdrop to 50,000 addresses.
**Concepts.** Token standards, Merkle trees, signature-based claims (EIP-712), gas cost of bulk distribution and why Merkle claims win, admin keys and multisig (Safe), timelocks.
**Architect lens.** Cost modeling at scale; separating admin powers; immutability vs upgradeability decision (first ADR).

---

## Stage B: Multi-component dApps (L2 to L3)

### Module 3. NFT ticketing platform (3 weeks)
**Brief.** Event organizers sell NFT tickets with capped resale prices and royalties; venue staff verify tickets at the door; fans buy with a card or crypto.
**Concepts.** ERC-721/1155, metadata storage (IPFS vs Arweave vs centralized), indexers (The Graph or a custom indexer), reorg handling, account abstraction (ERC-4337) and gas sponsorship for non-crypto users, signature-based check-in, L2 selection (Base/Arbitrum/Optimism) for cost.
**Architect lens.** First full HLD with on-chain/off-chain split; sequence diagrams for purchase, resale and check-in; platform decision matrix; enforcing resale caps (and the limits of on-chain enforcement).

### Module 4. DAO treasury and governance (2 to 3 weeks)
**Brief.** A community of 5,000 token holders governs a treasury: proposals, voting, timelocked execution, delegated voting, and an emergency guardian.
**Concepts.** OpenZeppelin Governor, vote snapshots and checkpoints, flash-loan governance attacks, timelocks, guardian/pause roles, off-chain voting (Snapshot) plus on-chain execution, upgradeability via governance (UUPS).
**Architect lens.** Governance attack surface; progressive decentralization roadmap; upgrade strategy ADR; incident runbook.

---

## Stage C: DeFi and adversarial design (L3 to L4)

### Module 5. Lending protocol (simplified Aave/Compound) (4 weeks)
**Brief.** Users deposit collateral, borrow stablecoins, accrue interest, and get liquidated when undercollateralized.
**Concepts.** Interest rate models, share-based accounting (ERC-4626), oracles (Chainlink, TWAP) and manipulation, liquidation incentives and keepers, MEV and front-running, invariant testing, mainnet fork tests, precision and rounding attacks, protocol risk parameters.
**Architect lens.** Full threat model; economic security (what does an attack cost vs what does it earn); monitoring and circuit breakers; case studies (Euler, Mango Markets, Compound misconfiguration).

### Module 6. Automated market maker plus aggregator (3 weeks)
**Brief.** A constant-product AMM with LP tokens, then an off-chain router that finds the best route across pools.
**Concepts.** AMM math, slippage and deadlines, sandwich attacks, private mempools/order flow, off-chain computation with on-chain verification, gas optimization deep dive.
**Architect lens.** What belongs on-chain vs in the router; MEV protection options and their trade-offs.

---

## Stage D: Scale, interoperability and enterprise (L4 to L5)

### Module 7. Cross-chain stablecoin payments (4 weeks)
**Brief.** A fintech moves a fiat-backed stablecoin between Ethereum, an L2 and Solana for merchant payouts, with compliance controls.
**Concepts.** Bridge designs (lock-and-mint, burn-and-mint, native e.g. CCTP, messaging protocols like LayerZero/CCIP/Wormhole), finality differences across chains, rollup architecture (sequencers, fraud/validity proofs, withdrawal delays), Solana account model and Rust/Anchor basics, allowlists/blocklists, travel rule.
**Architect lens.** Bridge risk analysis (Ronin, Wormhole, Nomad case studies); multi-chain HLD; liveness vs safety trade-offs; compliance architecture.

### Module 8. Real-world asset tokenization for an institution (4 weeks)
**Brief.** A bank tokenizes a money-market fund: KYC'd investors only, transfer restrictions, NAV oracle, corporate actions, regulator reporting, and a requirement for confidentiality.
**Concepts.** Permissioned tokens (ERC-3643), identity and verifiable credentials, permissioned chains (Hyperledger Besu/Fabric) vs public chains with allowlists, privacy options (private transactions, ZK proofs, off-chain data with on-chain commitments), GDPR vs immutability, custody (HSM, MPC, qualified custodians), enterprise integration (core banking, event buses).
**Architect lens.** Enterprise architecture documentation, stakeholder trade-off presentation, regulatory constraints as first-class requirements.

### Module 9. Supply chain provenance on a permissioned network (3 weeks)
**Brief.** A consortium of manufacturers, shippers and retailers tracks goods with IoT data and certificates.
**Concepts.** Hyperledger Fabric (channels, chaincode, endorsement policies, private data collections), consortium governance, oracle problem for physical data, when anchoring hashes on a public chain adds value.
**Architect lens.** Comparing permissioned vs public designs for the same requirements; governance and onboarding of new members.

---

## Capstone (L5)

### Module 10. Design and defend your own system (4 to 6 weeks)
The learner picks a problem (ideally from their work or target domain), and produces the complete package alone: requirements, threat model, HLD, LLD, ADRs, a working implementation of the core, test suite, security self-audit, operations plan and a v2 evolution plan. The mentor then runs a **mock architecture review board**: a 60-minute adversarial review playing CTO, security auditor and compliance officer.

---

## Running threads across all modules
- **Design review practice.** At the end of each module, the mentor reviews the learner's design as a hostile reviewer.
- **Incident studies.** One real exploit post-mortem per module, mapped to "which design decision would have prevented it".
- **Portfolio.** All artifacts live in `systems/NN-name/` and form a portfolio the learner can show employers.
- **Interview drills.** From Stage C on, periodic 45-minute "design X on a whiteboard" mock interviews.
