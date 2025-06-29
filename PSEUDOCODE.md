# FairShareCoin – Pseudocode

This document outlines the core logic behind the FairShareCoin (FSC) system.

Each real human can mint exactly one FSC after a one-time identity verification.  
There is no mining, no inflation, and no transaction fees.

---

## 1. Minting FSC (Identity-Based Issuance)
```pseudo
function registerUser(passportData, userEmail):
    if not isValid(passportData):
        return "Invalid identity"

    coinMintId = hash(passportData)

    if coinExists(coinMintId):
        return "Coin already issued"

    wallet = createWallet(coinMintId)
    issueCoin(wallet, 1 FSC)
    storeEmail(wallet, userEmail)

    return wallet.address
```

## 2. Sending FSC or Fractions
```pseudo
function sendFSC(fromWallet, toWallet, amount):
    if fromWallet.balance < amount:
        return "Insufficient balance"

    fromWallet.balance -= amount
    toWallet.balance += amount

    recordTransaction(fromWallet, toWallet, amount)
    return "Success"
```

## 3. Wallet Recovery (Lost Passport, Renewed ID, etc.)
```pseudo
function recoverWallet(passportData, optionalNewEmail):
    coinMintId = hash(passportData)

    if coinExists(coinMintId):
        wallet = getWalletByCoin(coinMintId)
        if optionalNewEmail:
            updateEmail(wallet, optionalNewEmail)
        return wallet

    return "No wallet found for this identity"
```

## 4. Inactivity and Death
```pseudo
function checkDormancy(wallet):
    if wallet.lastActive > 20 years:
        markAsDormant(wallet)
```
