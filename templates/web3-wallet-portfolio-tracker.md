---
title: Web3 Wallet Portfolio Tracker
app_type: web3-wallet-portfolio-tracker
wallet: 0x4d9dc6f2bfcd4fddfba76b4e36b2d2995d1a45ac
---

Build a Web3 wallet portfolio tracker dashboard that lets users monitor all their on-chain assets across multiple EVM-compatible chains in one place.

## Target Users

Crypto-native users and degens who hold assets across multiple wallets and chains (Ethereum, Base, Arbitrum, Optimism, Polygon) and want a clean, fast overview without connecting to a third-party custodial app.

## Pages and Features

### 1. Home — Portfolio Overview

- Hero section showing total portfolio value in USD with 24h change percentage and dollar delta (green/red)
- Wallet input field at the top: paste any `0x` address or ENS name to load portfolio (read-only, no wallet connection required)
- Support up to 5 watched wallets simultaneously, stored in localStorage
- Chain selector tabs: All Chains / Ethereum / Base / Arbitrum / Optimism / Polygon
- Token holdings table:
  - Columns: Token logo, Name, Symbol, Balance, Price, 24h Change, Value (USD)
  - Sortable by any column
  - Color-coded 24h change (green positive, red negative)
  - Show small balances toggle (hide tokens worth less than $1)
- NFT holdings section below tokens: grid of NFT cards with collection name, token ID, floor price in ETH and USD
- DeFi positions section: LP positions, staking, lending/borrowing with current APY and position value

### 2. Transactions Page

- Full transaction history for the watched wallet
- Filter bar: All / Sends / Receives / Swaps / NFT / Contract Interactions
- Date range picker
- Each row: tx hash (truncated, links to Etherscan/Basescan), type badge, from/to addresses, asset, amount, USD value at time, timestamp
- Infinite scroll pagination

### 3. Analytics Page

- Portfolio value over time line chart (1D / 1W / 1M / 3M / 1Y / All)
- Asset allocation donut chart by token and by chain
- Top gainers and losers this week (table)
- Gas spent over time bar chart
- PnL tracker: realized and unrealized gains per asset

### 4. Alerts Page (UI only, no backend required)

- Form to create price alerts: token, condition (above/below), price target, notification method (email or browser push)
- List of active alerts with toggle and delete
- Alert history log

## UI Layout and Components

- Left sidebar navigation (collapsible on mobile): icons + labels for Home, Transactions, Analytics, Alerts
- Top bar: wallet address display, chain selector, USD/ETH toggle, dark/light theme toggle
- All data displayed in cards with subtle borders, no heavy shadows
- Skeleton loading states for all async data sections
- Empty states with clear CTAs when no wallet is loaded
- Responsive: sidebar collapses to bottom tab bar on mobile (< 768px)
- Color scheme: dark mode default, neutral grays with blue and green accents

## Data and State

- Fetch token balances and prices from CoinGecko public API and Alchemy or Moralis for on-chain data (mock the API calls with realistic dummy data if APIs are unavailable at build time)
- Cache responses in localStorage with a 60-second TTL
- Global state managed with React Context or Zustand
- All monetary values formatted with Intl.NumberFormat, locale-aware

## Tech Stack

- TypeScript, React, Tailwind CSS (already in base stack)
- Recharts for all charts
- React Query for data fetching and caching
- React Router for page navigation
- Viem for address validation and ENS resolution

## Edge Cases and Error States

- Invalid wallet address entered: show inline error "Invalid address" without crashing
- API rate limit hit: show "Data temporarily unavailable, retry in Xs" banner and use cached data
- Wallet with zero assets: show friendly empty state "No assets found on this chain"
- Network error: show offline banner with retry button
- ENS name that does not resolve: show "ENS name not found" error

## Error Boundaries

- Wrap each page section in an error boundary so one broken section does not crash the whole dashboard
- Each error boundary shows a minimal "Something went wrong — reload section" fallback with a retry button
