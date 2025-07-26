
<p align="center">
  <img src="https://raw.githubusercontent.com/OxCheatcode/Minimal-Account-Abstraction/main/assets/banner.png" alt="Minimal Account Abstraction by @OxCheatcode" width="100%" />
</p>

# 🧱 Minimal Account Abstraction (AA) – @Cheatcode's Smart Contract Journal!

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

<p align="center">
  <img src="https://raw.githubusercontent.com/OxCheatcode/Minimal-Account-Abstraction/main/assets/aa-flow.png" alt="AA architecture diagram" width="80%" />
</p>

> This shows how a `UserOperation` flows through the `EntryPoint`, gets validated by the smart wallet, and finally executes a transaction.

---

## 🔍 Repo Overview

```bash
.
├── contracts/
│   ├── EntryPoint.sol            # Hub for UserOps – validates and routes them
│   ├── Wallet.sol                # Minimal smart wallet with custom validation
│   └── SimpleAccountFactory.sol # Deterministic wallet deployer
│
├── scripts/
│   ├── deploy.ts                 # Deploy smart contracts
│   └── sendUserOp.ts             # Send a UserOperation from smart wallet
│
├── test/
│   └── Wallet.t.sol              # Foundry tests for wallet logic
│
├── assets/                       # Visuals & banners
│   ├── banner.png
│   └── aa-flow.png
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


