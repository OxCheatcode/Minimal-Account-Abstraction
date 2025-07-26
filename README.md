

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

##🧾 What Each Contract Does
src/ethereum/MinimalAccount.sol
Implements a smart wallet with:

validateUserOp(...) — checks signature, nonces, funds.

execute(...) — allows the wallet to call arbitrary actions.

Prefund logic (_payPrefund) to top up EntryPoint if needed 
GitHub
+11
updraft.cyfrin.io
+11
GitHub
+11
updraft.cyfrin.io
+4
GitHub
+4
GitHub
+4
GitHub
+3
updraft.cyfrin.io
+3
updraft.cyfrin.io
+3

src/ethereum/EntryPoint.sol
The universal hub for AA on Ethereum:

Validates and processes all UserOperations.

Handles gas accounting, bundlers, refunds, and execution routing.

src/ethereum/AccountFactory.sol (or configured in scripts)
Deploys wallet contracts deterministically (e.g. via CREATE2).

Often paired with HelperConfig.s.sol to manage deploy addresses across networks.

src/zksync/ZkMinimalAccount.sol
Implements the IAccount interface for native AA on zkSync Era.

Handles:

validateTransaction(...) — checks nonce, signature, funds.

executeTransaction(...) — executes after validation.

Interactions with system contracts like NonceHolder via simulation (requires --system-mode=true) 
GitHub
+5
updraft.cyfrin.io
+5
GitHub
+5
updraft.cyfrin.io
+2
GitHub
+2
GitHub
+2
updraft.cyfrin.io
+9
updraft.cyfrin.io
+9
updraft.cyfrin.io
+9

##🧪 Tests Overview
test/ethereum/MinimalAccountTest.t.sol: Tests entryPoint invocation, owner vs. non‑owner access, successful execute() calls, and revert conditions 
GitHub
+5
updraft.cyfrin.io
+5
GitHub
+5
.

test/zksync/ZkMinimalAccountTest.t.sol: Uses Foundry’s forge‑zksync with SystemContractsCaller to simulate nonce updates and transaction flow 
GitHub
+12
updraft.cyfrin.io
+12
updraft.cyfrin.io
+12
.

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
npm install

# Compile contracts
forge build

# Run tests with verbose output
forge test -vvv

# Deploy EntryPoint & Wallet
npx hardhat run scripts/deploy.ts

# Send a UserOperation
npx hardhat run scripts/sendUserOp.ts
```

---

## 🔥 Key Smart Contracts

### 🧠 `Wallet.sol`

* Verifies signature using `validateUserOp`
* Executes arbitrary calldata
* Allows upgradeable security logic

### 🛣️ `EntryPoint.sol`

* Acts as the traffic controller
* Validates, routes, and executes bundled operations

### 🧱 `SimpleAccountFactory.sol`

* Deploys smart wallets deterministically via `CREATE2`

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

I'm **@Cheatcode**, and I build my skills in public 💻
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


