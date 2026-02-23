# ElectrumX - python electrum server

```
Licence: MIT
Original Author: Neil Booth
Current Maintainers: The Electrum developers
Language: Python (>= 3.10)
```

[![Latest PyPI package](https://badge.fury.io/py/e_x.svg)](https://pypi.org/project/e-x/)
[![Build Status](https://api.cirrus-ci.com/github/spesmilo/electrumx.svg?branch=master)](https://cirrus-ci.com/github/spesmilo/electrumx)
[![Test coverage statistics](https://coveralls.io/repos/github/spesmilo/electrumx/badge.svg?branch=master)](https://coveralls.io/github/spesmilo/electrumx)

This project is a fork of [kyuupichan/electrumx](https://github.com/kyuupichan/electrumx).
The original author dropped support for Bitcoin, which we intend to keep.

ElectrumX allows users to run their own Electrum server. It connects to your
full node and indexes the blockchain, allowing efficient querying of the history of
arbitrary addresses. The server can be exposed publicly, and joined to the public network
of servers via peer discovery. As of May 2020, a significant chunk of the public
Electrum server network runs ElectrumX.

## DIVI Vault Support

This fork includes enhanced support for **DIVI coin** with full **vault transaction** support:

- **DIVI Block Structure**: Handles DIVI's custom 112-byte block headers (vs standard 80 bytes)
- **Vault Detection**: Automatically identifies and tracks DIVI vault transactions
- **Enhanced Balance Queries**: Returns separate `vault_balance` and `spendable_balance` in balance responses
- **UTXO Tracking**: Properly stores and retrieves vault flags with UTXO data
- **Backward Compatibility**: Maintains compatibility with existing UTXO formats

### DIVI-Specific Features

- Custom block header deserialization with `acc_checkpoint` field support
- Vault script detection and address extraction (owner/host addresses)
- Dual hashing support: Quark hash for genesis block, Double SHA256 for subsequent blocks
- Enhanced transaction parsing with vault metadata

### Running DIVI

- **Mainnet** (default): Set `COIN=Divi`; `NET` defaults to `mainnet`. Use your mainnet daemon and a dedicated `DB_DIRECTORY`.
- **Testnet**: Set `COIN=Divi` and `NET=testnet`. Use a **separate** `DB_DIRECTORY` (e.g. `db_testnet`) and point `DAEMON_URL` at your testnet daemon (default RPC port 51474). Same vault and block behaviour as mainnet; only chain params differ.

### Documentation

See [readthedocs](https://electrumx-spesmilo.readthedocs.io).

### Releases

ElectrumX is generally mature software and usually running git HEAD in production is fine.
Alternatively, conservative people can run from the latest tag, for which there are also releases on PyPI:
```
$ pip install e-x
```
