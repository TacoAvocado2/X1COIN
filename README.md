# X1 Coin

Powered by the SHA256 algorithm, X1 sets new standards in transaction processing speed and integrity.  
X1 offers innovative approach to security, efficiency and reliability.

---

**Consensus mechanism:** Proof-Of-Work (POW)  
**Total supply:** 21,000,000  
**Pre Mined:** NO  
**Block Halving:** 210,000  
**Starting Reward:** 50  

---

**Website:**  
https://x1coin.net  

**GitHub:**  
https://github.com/TacoAvocado2/X1COIN  

**Wallet:**  
https://github.com/TacoAvocado2/X1COIN/tags  

**Block Explorer:**  
https://explorer.x1coin.net


# 🪙 X1Coin → AtomicDEX Integration & Listing Plan

## Overview
This document outlines the **end-to-end process** for integrating X1Coin into AtomicDEX (Komodo Platform) **without forking the DEX**.

AtomicDEX is decentralized:
- There is **no listing approval gate**
- A coin becomes usable when:
  1. It is properly configured
  2. Infrastructure is live
  3. Liquidity exists

---

# 🎯 Objectives

- Add X1Coin as a supported UTXO asset
- Enable wallet functionality (send/receive)
- Enable atomic swaps (X1 ↔ BTC/KMD/etc.)
- Avoid maintaining a fork
- Upstream integration via PR

---

# 🧱 Phase 1 — Chain Compatibility

## Requirements

X1Coin must behave like a standard Bitcoin fork:

- UTXO-based
- Supports:
  - P2PKH
  - P2SH
- Compatible with:
  - HTLC (Hashed Time-Locked Contracts)

## Developer Tasks

- Verify:
  - `pubkey address prefix (pubtype)`
  - `script hash prefix (p2shtype)`
  - `WIF prefix (wiftype)`
  - `tx version`
  - `decimals (typically 8)`
- Confirm:
  - No custom script behavior that breaks swaps

---

# 🌐 Phase 2 — Electrum Infrastructure (CRITICAL)

AtomicDEX depends on Electrum—not full nodes.

## Requirements

Deploy **minimum 2–3 public Electrum servers**

## Setup

- Use:
  - ElectrumX OR Electrs (adapted for X1Coin)
- Connect to:
  - Fully synced X1 full node
- Enable:
  - SSL (required)
- Recommended ports:
  - `50002` (SSL)

## Validation Checklist

- [ ] Server syncs fully
- [ ] Responds to:
  - balance queries
  - transaction history
  - broadcast requests
- [ ] Stable uptime

⚠️ If Electrum is unstable → AtomicDEX will fail regardless of config correctness

---

# ⚙️ Phase 3 — Coin Configuration

Add X1Coin to the Komodo coin registry.

## Example Config

```json
{
  "coin": "X1",
  "name": "X1Coin",
  "fname": "X1Coin",
  "rpcport": XXXX,
  "pubtype": XX,
  "p2shtype": XX,
  "wiftype": XX,
  "txfee": XXXX,
  "estimate_fee_mode": "ECONOMICAL",
  "mm2": 1,
  "required_confirmations": X,
  "avg_blocktime": XX,
  "protocol": {
    "type": "UTXO"
  },
  "electrum": [
    { "url": "electrum1.x1coin.org:50002" },
    { "url": "electrum2.x1coin.org:50002" }
  ]
}




