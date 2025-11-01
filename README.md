

# 🪙 BitMicro — MicroBitcoin Python Library

**BitMicro** is a lightweight, Bitcash-style Python library for working with **[MicroBitcoin (MBC)](https://microbitcoin.org/)** — fully compatible with the **mainnet**.
It allows you to generate wallets, manage private keys, and interact with the blockchain via the public API.

> Author: **neoncorp (Code Creator)** & **Volbil (API Creator)**
> License: MIT
> PyPI: [https://pypi.org/project/bitmicro](https://pypi.org/project/bitmicro/)

---

## ✨ Features

✅ Fully compatible with **MicroBitcoin mainnet**
✅ Bitcash-style key management
✅ Simple **Wallet API** (create, load, balance, send)
✅ **Base58Check**, **WIF**, and **hash160** utilities
✅ Lightweight — no blockchain sync
✅ Pure Python (no heavy dependencies except `ecdsa` and `requests`)

---

## 🧩 Installation

```bash
pip install bitmicro
```

---

## 🚀 Quick Start

```python
from bitmicro import Wallet

# Generate new wallet
wallet = Wallet.new()
print("Address:", wallet.address)
print("WIF:", wallet.wif)

# Check balance
print("Balance:", wallet.get_balance(), "MBC")

# Send coins (example)
# txid = wallet.send("MBC_ADDRESS_HERE", 1000)
# print("Transaction ID:", txid)
```

---

## 🧠 Module Overview

### 🔹 `Crypto Utilities`

| Function                            | Description                                    |
| ----------------------------------- | ---------------------------------------------- |
| `sha256(b)`                         | SHA-256 hash                                   |
| `ripemd160(b)`                      | RIPEMD-160 hash                                |
| `hash160(b)`                        | RIPEMD160(SHA256(b))                           |
| `double_sha256(b)`                  | SHA256 twice                                   |
| `to_wif(privkey, compressed=False)` | Convert private key to WIF                     |
| `wif_to_privkey(wif)`               | Decode WIF to private key bytes                |
| `pubkey_to_address(pubkey)`         | Convert a public key to a MicroBitcoin address |

---

### 🔹 `Network` Class

Provides wrappers for [api.mbc.wiki](https://api.mbc.wiki).

| Method                      | Description                 |
| --------------------------- | --------------------------- |
| `Network.info()`            | Get node info               |
| `Network.balance(address)`  | Get balance of address      |
| `Network.unspent(address)`  | Get UTXO list               |
| `Network.history(address)`  | Get transaction history     |
| `Network.transaction(txid)` | Get transaction details     |
| `Network.broadcast(raw)`    | Broadcast a raw transaction |

Example:

```python
from bitmicro import Network
print(Network.info())
```

---

### 🔹 `Wallet` Class

Encapsulates private key, public key, address, and signing utilities.

| Method                                   | Description                             |
| ---------------------------------------- | --------------------------------------- |
| `Wallet.new()`                           | Generate a new random wallet            |
| `Wallet.from_wif(wif)`                   | Load a wallet from WIF                  |
| `.get_balance()`                         | Retrieve balance from API               |
| `.get_unspent()`                         | Retrieve UTXOs                          |
| `.get_history()`                         | Retrieve transaction history            |
| `.create_tx(to_address, amount, fee=10)` | Create transaction (simplified)         |
| `.sign_tx(tx)`                           | Sign transaction (demo only)            |
| `.send(to_address, amount)`              | Create, sign, and broadcast transaction |

---

## 🧰 Example Workflow

```python
from bitmicro import Wallet

# Load from WIF
wallet = Wallet.from_wif("L4k3H2...yourWIFkey...")
print("Loaded:", wallet.address)

# View history
for tx in wallet.get_history():
    print(tx)

# Create & broadcast (demo)
tx = wallet.create_tx("MBC_DEST_ADDRESS", 1000)
signed = wallet.sign_tx(tx)
print("Signed TX:", signed[:60], "...")
```

---

## ⚙️ Developer Notes

* Transaction signing is currently **simplified** and not a full Bitcoin-style serializer.
* This library is meant for **wallet management, learning, and lightweight integration** — not full node operations.
* Full serialization support (e.g., SegWit, deterministic TXs) may be added in later releases.

---

## 🧑‍💻 API Reference Summary

```python
from bitmicro import (
    sha256, ripemd160, hash160, double_sha256,
    to_wif, wif_to_privkey, pubkey_to_address,
    Network, Wallet
)
```

---

## 🧾 License

```
GNU General Public
Copyright (c) 2025 neoncorp
```

---

## 🌐 Contributors

| Name         | Role                                |
| ------------ | ----------------------------------- |
| **neoncorp** | Core library, wallet implementation |
| **Volbil**   | API developer (`api.mbc.wiki`)      |



I can generate either file ready for upload (`setup.py` or `pyproject.toml` compatible).
