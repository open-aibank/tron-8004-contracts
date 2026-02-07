# tron-8004-contracts

Smart contracts for **ERC-8004** (Trustless Agent) support on the **TRON** network.

## What is ERC-8004?

[ERC-8004](https://www.erc8004.org/) is an open, neutral standard for trustless AI agent identity, reputation, and validation. It provides a standardized way for agents to be registered as unique identities (NFTs) and builds a decentralized trust layer around them.

- **Identity First**: Agents are represented as ERC-721 tokens, making them ownable, transferable, and easily discoverable.
- **On-Chain Reputation**: A transparent feedback system for agents to build verifiable track records.
- **Independent Validation**: A framework for agents to request and receive third-party validation (TEE, zkML, or human audits) of their work.
- **Trustless Integration**: Verified payment wallets linked to agent identities for secure financial interactions.

## Features

- **ERC-721 Identity Registry**: Agents are minted as NFTs with unique IDs and metadata storage.
- **Verified Agent Wallets**: Secure linking of payment wallets to agents using EIP-712/ERC-1271 signatures.
- **Spam-Resistant Feedback**: Anyone can leave feedback, with on-chain aggregation and revocation support.
- **Validation Hooks**: Generic interface for requesting and recording independent validations.
- **Tron-Optimized**: Designed for the TRON network with high throughput and low fees.
- **Flexible Metadata**: On-chain key-value metadata storage for agent-specific configurations.

## Architecture

The project consists of three main registry contracts:

- **`IdentityRegistry.sol`**: The core contract that manages agent registration (as ERC-721), metadata, and payment wallet verification.
- **`ReputationRegistry.sol`**: Manages feedback and reputation scores, allowing clients to rate agents and agents to respond.
- **`ValidationRegistry.sol`**: Handles validation requests from agents to independent validators and records their responses.

### Flow
1. **Register**: An owner registers an agent in `IdentityRegistry`, receiving an NFT.
2. **Verify Wallet**: The agent's payment wallet signs a message to prove ownership, which is then recorded in `IdentityRegistry`.
3. **Validate**: The agent requests validation for a task in `ValidationRegistry`; a validator provider (e.g., a TEE) submits the result.
4. **Interact & Feedback**: Clients interact with the agent and provide feedback in `ReputationRegistry`.

## Deployed Addresses (Nile Testnet)

- `IdentityRegistry`: `[TRLTghbBbxEmB2BojVfk5EugUrTARSkeU4]`
- `ReputationRegistry`: `[TPXCSyfNi5G2UTQMXdr8PTWS2RXp3tPbU7]`
- `ValidationRegistry`: `[TTtRQ7csbUaWbFaJim5Lxp4RkkWiaj2dE3]`

## Requirements

- **Node.js**: v18+
- **pnpm** or **npm**
- **Solidity**: 0.8.25
- **For TRON Deployment**: [@sun-protocol/sunhat](https://github.com/sun-protocol/sunhat) and a TRON RPC URL + deployer private key.

## Quick Start

### Install Dependencies
```bash
npm install
# or
pnpm install
```

### Build
```bash
npm run compile
```

### Test
This project supports both Hardhat and Foundry for testing.

**Run Hardhat tests:**
```bash
npm test
```

**Run Foundry tests:**
```bash
npm run test-foundry
```

### Deploy (TRON)
Ensure your `.env` is configured with `TRON_PRIVATE_KEY` and `TRON_RPC_URL`.

```bash
npm run deploy
```

## Project Layout

- `contracts/`: Core smart contract logic.
  - `interfaces/`: Solidity interfaces for ERC-8004.
- `test/`: Hardhat and Foundry test suites.
- `scripts/`: Deployment and utility scripts.
- `deploy/`: Deployment configurations for Sunhat.

## Security

The `IdentityRegistry` uses **EIP-712** and **ERC-1271** for secure wallet verification. Agent wallets are automatically reset upon NFT transfer to ensure security of the new owner.

*Note: These contracts are reference implementations and should undergo a professional audit before mainnet deployment.*

## License

This project is licensed under **CC0-1.0**.
