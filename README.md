# Bitcoin Wallet Example using BDK with Esplora (Regtest)

This example demonstrates how to create a Bitcoin wallet using Bitcoin Development Kit (BDK) with Esplora blockchain explorer in regtest mode. The example shows:

1. Creating/loading a wallet
2. Generating addresses
3. Receiving regtest bitcoins
4. Sending bitcoins to another address

## Prerequisites

- Rust development environment
- Setup a local Bitcoin Core node daemon in regtest mode
- Setup a local regtest esplora API server using the mempool.space version of electrs

## Bitcoin Core Setup

Run Bitcoin Core in regtest mode:

```bash
bitcoind -regtest -rpcuser=<username> -rpcpassword=<password>
```

## Esplora Server Setup (mempool.space version of electrs)

1. Clone the mempool.space version of electrs:
```bash
git clone https://github.com/mempool/electrs.git
cd electrs
```

2. Run electrs in regtest mode connected to your Bitcoin Core node:
```bash
cargo run --release --bin electrs -- -vvv --daemon-dir ~/.bitcoin --network=regtest --cors http://localhost:5000
```

3. Run Esplora
```bash
git clone https://github.com/blockstream/esplora.git
cd esplora
npm run dev-server
```

Note: Adjust paths as needed for your Bitcoin Core data directory.

## Running the Example

1. Make sure Bitcoin Core is running in regtest mode
2. Make sure the Esplora server (electrs) is running
3. Run the example:

```bash
cargo run
```

## Code Explanation

The code:
1. Creates or loads a BDK wallet from file storage
2. Generates two addresses - one for receiving funds and another for demonstrating sending
3. Mines 101 blocks to the first address, generating spendable bitcoin
4. Syncs the wallet with the blockchain via Esplora
5. Creates a transaction sending funds to the second address
6. Signs and broadcasts the transaction

## Configuration

The example uses the following constants that you may need to adjust:

- `NETWORK`: Set to Network::Regtest
- `EXTERNAL_DESC` and `INTERNAL_DESC`: BIP32 descriptors for the wallet
- `ESPLORA_URL`: URL of your Esplora server
- `RPC_URL`, `RPC_USER`, `RPC_PASSWORD`: Bitcoin Core RPC connection details

## Note

This is a simple example for competency test purposes. 
In production environments, you would need more robust error handling and security considerations.