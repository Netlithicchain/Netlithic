# Netlithic Node Setup (Local Devnet)

This guide covers what the current node software actually does: a local
proof-of-work devnet (chain id `netlithic-dev-1`) with Ed25519-signed
transfers and HTTP peer-to-peer sync. There is no public testnet yet, no
staking, and no validator set.

## 1. Requirements

- Python 3.10 or newer
- The `cryptography` package:

```
python -m pip install -r requirements.txt
```

## 2. Create a wallet

```
python wallet.py
```

This creates a new Ed25519 wallet, saves it to `wallets.json` in the
current folder, and prints its address. The printed output includes the
private key: do not paste it anywhere, and never share or commit
`wallets.json` (it is listed in `.gitignore`).

## 3. Start a node

```
python p2p_http.py 8000
```

- The first argument is the port (default `8000`). An optional second
  argument is the host to bind (default `127.0.0.1`, local only).
- `python node.py 8000` does the same thing; with no argument `node.py`
  uses port `5000`.
- On first start the node creates `chain.json` with the genesis block.
  If `chain.json` exists but does not validate, the node stops with an
  error instead of overwriting it.

Check it is running:

```
curl http://127.0.0.1:8000/status
```

## 4. Run a second node and connect them

There is no `--peer` flag. Start the second node, then tell it about the
first one:

```
python p2p_http.py 8001
curl -X POST http://127.0.0.1:8001/add_peer -H "Content-Type: application/json" -d "{\"peer\": \"http://127.0.0.1:8000\"}"
```

Peers are saved to `peers.json`, and nodes sync with each other every
few seconds.

> Run each node from its own folder. `chain.json`, `mempool.json`,
> `peers.json` and `state_contributions.json` are read from the current
> folder, so two nodes in one folder will share and overwrite these files.

## 5. Mine a block

```
curl -X POST http://127.0.0.1:8000/mine -H "Content-Type: application/json" -d "{\"miner_address\": \"<your address>\"}"
```

Each block pays a fixed reward of 10 NLT to the miner. Difficulty starts
at 3 and adjusts every 10 blocks.

## 6. Check a balance and send a transfer

```
curl "http://127.0.0.1:8000/balance?address=<address>"
python send_tx.py <from_address> <to_address> <amount> --node http://127.0.0.1:8000
```

`send_tx.py` signs with the sender's key from your local `wallets.json`.
The transfer is confirmed once a block is mined.

## 7. Other endpoints

- `GET /chain`, `GET /mempool`, `GET /peers`, `GET /status`
- `GET /account?address=<address>` (balance and nonce)
- `POST /sync` (pull the longest valid chain from peers now)

## 8. Start over with a fresh chain

```
python new_genesis.py --yes
```

This renames `chain.json`, `mempool.json` and `state_contributions.json`
to `.bak` files and creates a fresh genesis chain. It does not touch
`wallets.json` or `peers.json`. Every node must be reset the same way.
