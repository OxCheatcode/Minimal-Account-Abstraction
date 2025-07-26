

# 🧱 Minimal Account Abstraction (AA) – Cheatcode's Smart Contract Journal!

This repo documents my hands-on learning of Account Abstraction using [Cyfrin's Minimal Account Abstraction](https://github.com/Cyfrin/minimal-account-abstraction) template. I explored how Ethereum is shifting towards more flexible, powerful, and user-friendly wallet experiences.

---

## 🤖 What is Account Abstraction?

> **Account Abstraction** (AA) is the ability for an Ethereum account to **sign and validate transactions using arbitrary logic** — not just a single private key.

AA enables:

- 🔐 Signing with Google, GitHub, or biometrics
- 🤝 Multi-sig with friends or family
- ⛽ Gas paid by third parties (sponsored txs)
- 🧠 Custom security rules, session keys, etc.

---

### ⚙️ How it works on different chains

| Chain     | AA Type            | Details                                                                 |
|-----------|--------------------|-------------------------------------------------------------------------|
| **Ethereum** | EIP-4337 ALT mempool | A parallel "userOp mempool" handles AA using contracts like `EntryPoint.sol`. |
| **zkSync**   | Native AA (built-in) | All accounts on zkSync are smart contracts by default (no EOAs).       |

---

## 📐 Visual Architecture



> This shows how a `UserOperation` flows through the `EntryPoint`, gets validated by the smart wallet, and finally executes a transaction.

---

## 🔍 Repo Overview

```bash
.
.
├── src/
│   ├── ethereum/
│   │   ├── MinimalAccount.sol      # ERC‑4337 compliant smart-wallet for Ethereum
│   │   ├── EntryPoint.sol          # Handles UserOperations & execution hub
│   │   └── AccountFactory.sol or HelperConfig # Deploys MinimalAccount
│   └── zksync/
│       └── ZkMinimalAccount.sol    # Native AA implementation for zkSync Era
│
├── test/
│   ├── ethereum/
│   │   └── MinimalAccountTest.t.sol  # Tests Ethereum AA behavior
│   └── zksync/
│       └── ZkMinimalAccountTest.t.sol # zkSync tests :contentReference[oaicite:6]{index=6}
│
├── script/
│   ├── DeployMinimal.s.sol
│   ├── SendPackedUserOp.s.sol      # Builds and sends userOps
│   └── HelperConfig.s.sol           # Chain/address config
│
├── lib/                            # Submodule dependencies (openzeppelin, forge-std, etc.) :contentReference[oaicite:7]{index=7}
├── Makefile                        # Standard build commands
├── foundry.toml / foundry‑zksync.toml
└── README.md

````



---

## 🚀 What I Built & Tested

✅ Deployed an `EntryPoint`
✅ Built a custom `Wallet` that validates signatures & executes txs
✅ Sent `UserOperations` through the bundler
✅ Simulated paymaster & sponsor gas flow
✅ Ran contract tests using **Foundry**

---

## 💻 Commands

```bash
# Install dependencies
forge install

# Compile contracts
forge build

# Run tests with verbose output
forge test -vvv


```

---

## 🔑 Key Smart Contracts

### `MinimalAccount.sol`
- A minimal smart contract wallet that supports EIP‑4337.
- Core responsibilities:
  - `validateUserOp(UserOperation, ...)`: Verifies signature and nonce, and ensures prefunding.
  - `execute(address dest, uint256 value, bytes calldata func)`: Executes any call as the wallet.
  - `owner()`: Returns the current wallet owner (EOA or contract).
- Complies with `IAccount`, enabling bundler compatibility.

---

### `EntryPoint.sol`
- The **core hub** of EIP‑4337 transactions.
- It:
  - Accepts `UserOperation` bundles.
  - Validates each op via the associated smart wallet.
  - Handles prefund logic, refunding gas, and executing the transaction.
- All UserOps must be sent through this contract.

---

### `AccountFactory.sol`
- A helper contract to deploy instances of `MinimalAccount` via **`CREATE2`**.
- Enables deterministic deployment of wallets based on a user-supplied salt.
- Useful for predicting wallet addresses *before* on-chain deployment.

---

### `ZkMinimalAccount.sol`
- A zkSync-native account abstraction contract.
- Implements `IAccount` interface for **zkSync Era**.
- Key methods:
  - `validateTransaction(...)`: Signature and nonce checks.
  - `executeTransaction(...)`: Runs validated calls.
- Interacts with zkSync system contracts like `NonceHolder`.

---

### `HelperConfig.s.sol`
- Stores configuration details (e.g. chain-specific addresses).
- Dynamically selects the correct deployer or entry point depending on the chain (Ethereum, zkSync, etc).


---

## 💎 Why Account Abstraction Matters

| Feature                                  | EOAs (legacy) ❌ | Smart Wallets (AA) ✅ |
| ---------------------------------------- | --------------- | -------------------- |
| Custom auth (FaceID, social, biometrics) | No              | Yes                  |
| Sponsored tx (gasless)                   | No              | Yes                  |
| Multi-sig, session keys, plugins         | No              | Yes                  |
| Recovery mechanisms                      | No              | Yes                  |

AA makes wallets secure, programmable, and **finally user-friendly** for mass adoption 🚀

---

## 🧠 Learn With Me

I'm **Cheatcode**, and this is my public journal for documenting every smart contract code learnt and written by me 💻
Follow me and let’s grow together:

* 🧠 GitHub: [@OxCheatcode](https://github.com/OxCheatcode)
* 🐦 X/Twitter: [@OxCheatcode](https://x.com/OxCheatcode)

Feel free to fork this repo and remix your own smart wallet flows.

---

## 🙏 Credits

Massive thanks to **Cyfrin** and [@PatrickAlphaC](https://github.com/PatrickAlphaC) for breaking down complex ideas into hands-on code.

Repo inspired by: [Cyfrin/minimal-account-abstraction](https://github.com/Cyfrin/minimal-account-abstraction)

---

## 📚 Resources

* 📖 [EIP-4337 Spec](https://eips.ethereum.org/EIPS/eip-4337)
* 📘 [Vitalik on AA](https://vitalik.ca/general/2021/01/11/account_abstraction.html)
* 🧪 [StackUp AA Dev Docs](https://docs.stackup.sh/docs)
* 📺 [Cyfrin Updraft AA Module](https://github.com/Cyfrin/updraft-account-abstraction)

---

## 🧾 License

MIT License – Fork freely, build openly, give due credits!🙌


