![License](https://img.shields.io/badge/license-MIT-blue)
![Status](https://img.shields.io/badge/status-devnet-orange)
![Language](https://img.shields.io/badge/python-3.10+-green)
<p align="center">
  <img src="netlithic-logo.png" width="220" alt="Netlithic logo">
</p>

# Netlithic

**The AI-native blockchain run by its contributors.**

Netlithic is a community-driven blockchain protocol designed for decentralized infrastructure and future AI-native applications.

The network is open source and governed by its contributors.

Instead of prioritizing speculation, Netlithic distributes NLT through **Proof of Contribution**, allowing developers, validators, and community members to earn NLT for running and improving the network.

---

## Core Principles

• Proof of Contribution (early, local-only prototype)  
• Contributor-Run Ecosystem (goal)  
• AI-Native Infrastructure (future direction)  

Today the devnet uses proof-of-work with a fixed 10 NLT block reward, no
supply cap and no pre-mine. See [Tokenomics](docs/Tokenomics.md) for what is
implemented and what is only proposed.

---

## Vision

Netlithic aims to become the **foundation layer for decentralized intelligence**.

The protocol is designed to support:

- decentralized applications
- contributor-run ecosystems
- validator security networks
- autonomous AI agents

The goal is for NLT to be earned by the people who build and run it.

---

## Run a Netlithic Node (Local Devnet)

Netlithic can currently be run locally for development and testing.

### Requirements

• Python 3.10+
• The `cryptography` package (`pip install -r requirements.txt`)

### Clone the Repository

```
git clone https://github.com/Netlithicchain/Netlithic.git
cd Netlithic
```

> Note: this repository holds the website and documentation. The node
> software (`p2p_http.py`, `core.py`, `wallet.py`, ...) is developed in a
> separate repository that is not public yet.

### Start a Node

```
python -m pip install -r requirements.txt
python p2p_http.py 8000
```

### Start a Second Node (Optional)

```
python p2p_http.py 8001
curl -X POST http://127.0.0.1:8001/add_peer -H "Content-Type: application/json" -d "{\"peer\": \"http://127.0.0.1:8000\"}"
```


For a full setup guide see:

[Full Node Setup Guide](docs/NODE_SETUP.md)

---

## Website

https://netlithicchain.com

---

## License

Netlithic is released as open-source software under the **MIT License**.

© 2026 Netlithic Protocol
