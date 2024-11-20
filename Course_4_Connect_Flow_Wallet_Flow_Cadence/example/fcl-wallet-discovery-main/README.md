# Connect a Wallet on Flow Blockchain Cadence Environment

This repository provides a quickstart guide to connect a wallet on the Flow Blockchain using the Cadence environment. Connecting a wallet is essential for secure transactions and interacting with dApps on Flow.

Follow along with the **[tutorial here](https://flowfoundation.notion.site/Connect-a-Wallet-on-Flow-Blockchain-Cadence-Environment-13e1aee1232480e59f74ef956f6a1ddd)** for a step-by-step guide. This setup supports Flow-native wallets, like **Flow Wallet** and **Blocto**.

For more on connecting a wallet in the Flow EVM environment, check out the **[Telegram Wallet Guide for Flow EVM](https://www.notion.so/Connect-a-Telegram-Embedded-Wallet-UXUY-on-Flow-EVM-13e1aee12324809c800fda6c3186d10e?pvs=21)**.

## Overview

This example includes:
- Setting up a **Next.js project** with **TypeScript** and **App Router**
- Configuring Flow for mainnet/testnet
- Custom hooks and contexts for user authentication with Flow
- A sample wallet connection interface with optional Tailwind CSS styling

## Quickstart

Clone the repository or use it as a reference:

[GitHub Repository](https://github.com/bz-hashtag-0780/fcl-wallet-discovery) | [Live Demo](https://fcl-wallet-discovery.vercel.app/)

## Getting Started

1. **Set Up Next.js with TypeScript**:
   ```bash
   npx create-next-app@latest my-app --typescript
   cd my-app
   npm install --save @onflow/fcl @onflow/types
   ```

2. **Flow Configuration**:
   In `flow-config.ts`, configure `accessNode.api`, `flow.network`, and `discovery.wallet`.

3. **Authentication Hook**:
   Use the `useCurrentUser` hook for logging in and out of Flow wallets.

4. **Auth Context Setup**:
   Create `AuthContext.tsx` to manage wallet connection state globally.

5. **UI Setup**:
   Add a simple connect/disconnect button in your main `page.tsx`.

6. **Optional Styling**:
   Use Tailwind CSS for basic UI styling.

## Conclusion

By following these steps, you’ll have a Next.js application that enables wallet connection on Flow Cadence, ready for user interaction with Flow-native wallets.

For further details, please refer to the **[tutorial on Notion](https://flowfoundation.notion.site/Connect-a-Wallet-on-Flow-Blockchain-Cadence-Environment-13e1aee1232480e59f74ef956f6a1ddd)**.
