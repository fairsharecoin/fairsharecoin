# FairShareCoin – Technical Notes and Design Philosophy

> **Status note (2026-04-03):** This is a living concept draft and contains forward-looking and historical design language. Current implemented behavior (alpha runtime, security controls, and operational constraints) is maintained in `fairsharecoin/foundation`. Treat this document as non-authoritative when it conflicts with implementation docs.

This document outlines the core logic and functional design of FairShareCoin (FSC).  
FSC is engineered to be minimal, fair, and durable.

## Implementation Delta (concept vs current alpha runtime)

To reduce confusion for readers:

- This file describes **target/proposed** behavior in multiple sections.
- The active alpha runtime today is centralized-operational and iterated in `fairsharecoin/foundation`.
- Specific values/rules in this file (for example: dormancy windows, governance claims, fully fee-free final-state assumptions, and recovery/freeze flow details) should be treated as **draft policy language**, not guaranteed current production behavior.
- For integration, testing, and operator expectations, prioritize the implementation repo docs and runbooks.

---

## 1. Identity-Based Minting

Each person may mint one FSC by verifying identity via an ICAO-compliant passport.

- The passport is hashed to create a unique identifier: `COINMINT_ID = hash(passportData)`
- Raw passport data is never stored
- One FSC is issued to one wallet — no repeats, no mining
- Prevents duplicate claims while preserving user privacy

---

## 2. Email / GPG Identity Anchor

Every wallet is created with a secure email address or GPG public key.

This identity anchor is:

- Provided during the initial registration process
- Stored off-chain, never placed on the public ledger
- Used for wallet continuity, recovery, and optional interaction
- Replaceable upon verified recovery (e.g. new passport)

Even if email is lost, recovery via passport-based verification remains possible.  
However, linking a new email may be required to reestablish continuity.

This dual-anchor system (passport hash + email/GPG key) supports both uniqueness and usability.

---

## 3. No Mining / Controlled Growth

FSC cannot be mined.  
Coins are only issued to verified, living humans — once per person.

- No rewards are given for computation, staking, or early participation
- The total supply grows slowly over time, reflecting real human participation
- Supply is strictly limited by the number of unique verified individuals
- FSC is inherently deflationary long-term, as coins become inactive after death or prolonged inactivity

---

## 4. Transactions and Fees

- The target model aims for fee-minimal or fee-free user transfers where operationally feasible
- Any wallet may send fractions of FSC to valid destinations defined by the active implementation
- Validator/settlement architecture is implementation-dependent during alpha phases
- Finality and settlement guarantees should be read from the active runtime documentation

---

## 5. No Anonymous Minting

Wallets must be created through verified identity to receive FSC.  
Anonymous use is permitted **after** minting — but cannot initiate it.

This ensures:
- One-person-one-coin remains enforceable
- There is no “free ride” or black market wallet generation

---

## 6. Wallet Recovery

If a user loses access to their FSC wallet:

- They may re-verify with a valid passport
- The system hashes the new document and matches the COINMINT_ID
- The original wallet and coin are re-linked
- No new coin is created

---

## 7. Death and Inactivity

- Long-term policy intent is to avoid arbitrary reassignment of value
- Dormancy windows (including any 20+ year concept) are draft policy values and may change before stable protocolization
- Inactivity handling is intended as a fairness-preserving supply behavior, but implementation details remain under active design
- Inheritance/donation behavior depends on future policy and implementation decisions

---

## 8. Fractional Units

FSC supports full divisibility into fractional units:
- nanos (0.000000001 FSC)
- picos (0.000000000001 FSC)
- or other standards in future applications

Fractional units enable:
- Tipping
- Game scoring
- Microsharing
- Long-term scaling of value

---

## 9. Governance Scope (Draft Position)

Current concept direction minimizes on-chain governance complexity.

- The design intent remains: 1 coin, 1 person, no arbitrary reissuance
- Governance/process structures may evolve off-chain as the project matures
- Legal, social, and operational adaptations are expected to develop alongside implementation phases

---

## 10. Future Extensions (Optional)

While FSC is minimal by design, the protocol may be extended by others via Layer 2 or Layer 3 systems.

Examples may include:
- Microtransactions in games (pico-scale scoring)
- Voluntary trust ratings or contribution badges
- Anonymous group wallets with multisig constraints
- Encrypted peer-to-peer services tied to FSC wallets

None of these are required for FSC to function.

---

## 11. Design Priorities

- Enforced scarcity through human uniqueness, not computational cost  
- Free global access — no energy burn, no startup capital  
- Durable logic with minimal surface area for attack or abuse  
- Fairness by protocol, not politics  
- Optional anonymity without undermining issuance rules

---

## 12. Wallet Freeze & Recovery Logic

To protect user funds and maintain one-human-one-coin integrity, FairShareCoin wallets support a dual-freeze and single-reactivation system:

### Freeze Triggers

A wallet can be frozen by either of the following:

1. **Registered Email or GPG Key**
   - A signed request to freeze the wallet can be sent using the registered email or GPG key.
   - Useful if the user's ePassport is lost or suspected stolen.

2. **Verified ePassport Scan**
   - A live scan using the original passport (matching the COINMINT_ID) can be used to freeze the wallet.
   - Useful if the email account has been compromised.

Frozen wallets cannot send or receive until reactivated.

---

### Reactivation

To reactivate a frozen wallet, the user must:

- Present a valid ePassport matching their original COINMINT_ID, and
- Register a new email address or GPG key

Only a valid ePassport (preferably a digitally signed one via NFC) can reactivate a frozen wallet. This ensures that control can only be restored by the original identity.

---

### Additional Safeguards

- Freeze/recovery events are logged on the public ledger for transparency (no private data exposed).
- Only the original identity can reclaim the wallet — there is no reset or re-mint.
- This system protects against physical passport theft, email compromise, or malicious recovery attempts.



## Current implementation references

- Active implementation baseline: https://github.com/fairsharecoin/foundation
- Alpha runbooks and release/readiness docs: `foundation/docs/`

## Status

This document is a living draft.  
As implementation evolves, details may be refined.
