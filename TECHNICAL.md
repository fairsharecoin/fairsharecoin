# FairShareCoin – Technical Notes and Design Philosophy

This document outlines the core logic and functional design of FairShareCoin (FSC).  
FSC is engineered to be minimal, fair, and durable.

---

## 1. Identity-Based Minting

Each person may mint one FSC by verifying identity via an ICAO-compliant passport.

- The passport is hashed to create a unique identifier: `COINMINT_ID = hash(passportData)`
- Raw passport data is never stored
- One FSC is issued to one wallet — no repeats, no mining
- Prevents duplicate claims while preserving user privacy

---

## 2. No Mining / Controlled Growth

FSC cannot be mined.  
Coins are only issued to verified, living humans — once per person.

- No rewards are given for computation, staking, or early participation
- The total supply grows slowly over time, reflecting real human participation
- Supply is strictly limited by the number of unique verified individuals
- FSC is inherently deflationary long-term, as coins become inactive after death or prolonged inactivity

---

## 3. Transactions and Fees

- Transactions are always free
- Any wallet may send fractions of FSC to any valid address
- There are no miners, validators, or third parties involved
- All transactions are peer-to-peer and final

---

## 4. No Anonymous Minting

Wallets must be created through verified identity to receive FSC.  
Anonymous use is permitted **after** minting — but cannot initiate it.

This ensures:
- One-person-one-coin remains enforceable
- There is no “free ride” or black market wallet generation

---

## 5. Wallet Recovery

If a user loses access to their FSC wallet:

- They may re-verify with a valid passport
- The system hashes the new document and matches the COINMINT_ID
- The original wallet and coin are re-linked
- No new coin is created

---

## 6. Death and Inactivity

- Coins are never reclaimed or reassigned
- After 20+ years of inactivity, a wallet may be marked dormant
- This serves as a soft deflation mechanism
- Inheritance and donation are up to the user while alive

---

## 7. Fractional Units

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

## 8. No Governance Layer

FSC has no built-in voting, policy, or economic governance.

- There is no foundation, council, or DAO
- The design is final by intent: 1 coin, 1 person, no reissuance
- Philosophical, social, or legal adaptations must occur outside the system

---

## 9. Future Extensions (Optional)

While FSC is minimal by design, the protocol may be extended by others via Layer 2 or Layer 3 systems.

Examples may include:
- Microtransactions in games (pico-scale scoring)
- Voluntary trust ratings or contribution badges
- Anonymous group wallets with multisig constraints
- Encrypted peer-to-peer services tied to FSC wallets

None of these are required for FSC to function.

---

## 10. Design Priorities

- Enforced scarcity through human uniqueness, not computational cost  
- Free global access — no energy burn, no startup capital  
- Durable logic with minimal surface area for attack or abuse  
- Fairness by protocol, not politics  
- Optional anonymity without undermining issuance rules

---

## Status

This document is a living draft.  
As implementation evolves, details may be refined — but the foundational rules will not.
