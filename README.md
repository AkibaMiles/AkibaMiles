# AkibaMiles

A loyalty rewards dApp built on [Celo](https://celo.org/) for [MiniPay](https://www.opera.com/products/minipay) users. Earn miles by completing daily quests and on-chain activities, then spend them on raffles and games to win real prizes.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

---

## How It Works

**Earn** — Complete daily quests, transaction streaks, and partner quests to earn AkibaMiles (a non-transferrable on-chain points token).

**Spend** — Use your miles to enter raffles for digital rewards (USDT) and physical prizes, or play the Dice game.

**Vault** — Deposit USDT to earn yield via Aave v3. Your principal is always redeemable 1:1 via akUSDT receipt tokens.

---

## Project Structure

```
AkibaMiles/
├── packages/
│   ├── react-app/        # Next.js frontend (MiniPay dApp)
│   ├── hardhat/          # Solidity smart contracts
│   ├── backend/          # API / off-chain services
│   └── akiba-dice/       # Dice game frontend
├── akiba/                # The Graph subgraph (raffle indexer)
└── packages/docs/        # Documentation
```

### Smart Contracts

| Contract | Description |
|---|---|
| `AkibaMiles` (MiniPoints) | Non-transferrable ERC-20 loyalty points token |
| `AkibaRaffleV6` | UUPS upgradeable raffle with Witnet randomness |
| `AkibaDiceGame` | 6-player dice game using Witnet randomness |
| `AkibaMilesVaultUUPS` | USDT vault that supplies to Aave v3, mints akUSDT |
| `akUSDT` | ERC-20 receipt token for vault deposits |

All contracts are deployed on **Celo mainnet**.

---

## Prerequisites

- Node.js v20+
- pnpm (or yarn)
- Git v2.38+

---

## Getting Started

### Install dependencies

```bash
pnpm install
```

### Frontend (MiniPay dApp)

```bash
# Copy and fill in env vars
cp packages/react-app/.env.template packages/react-app/.env

# Start dev server
pnpm react-app:dev
```

Required env vars:

| Variable | Description |
|---|---|
| `NEXT_PUBLIC_SUPABASE_URL` | Supabase project URL |
| `NEXT_PUBLIC_SUPABASE_ANON_KEY` | Supabase anon key |
| `NEXT_PUBLIC_WALLETCONNECT_PROJECT_ID` | WalletConnect Cloud project ID |

### Smart Contracts

```bash
cd packages/hardhat

# Copy and fill in env vars
cp .env.template .env   # add your PRIVATE_KEY

# Deploy to Celo testnet (Alfajores)
npx hardhat ignition deploy ./ignition/modules/MiniRaffle.ts --network alfajores

# Deploy to Celo mainnet
npx hardhat ignition deploy ./ignition/modules/MiniRaffle.ts --network celo
```

Get test CELO from the [Alfajores Faucet](https://faucet.celo.org/alfajores).

### Subgraph

```bash
cd akiba

# Build and deploy to The Graph Studio
graph codegen && graph build
graph deploy --node https://api.studio.thegraph.com/deploy/ akiba
```

---

## Tech Stack

- [Next.js](https://nextjs.org/) — frontend framework
- [Celo](https://celo.org/) — L1 blockchain
- [MiniPay](https://www.opera.com/products/minipay) — target wallet
- [Hardhat](https://hardhat.org/) — smart contract development
- [OpenZeppelin](https://openzeppelin.com/) — upgradeable contract libraries
- [Aave v3](https://aave.com/) — yield on deposited USDT
- [Witnet](https://witnet.io/) — on-chain randomness
- [The Graph](https://thegraph.com/) — raffle event indexing
- [Supabase](https://supabase.com/) — off-chain quest tracking
- [Tailwind CSS](https://tailwindcss.com/) + [shadcn/ui](https://ui.shadcn.com/) — UI

---

## License

MIT — see [LICENSE](./LICENSE) for details.
