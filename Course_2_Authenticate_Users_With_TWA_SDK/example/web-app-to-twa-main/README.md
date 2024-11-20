# Authenticate Users Using `@twa-dev/sdk` in Your Next.js Frontend

This repository provides a quickstart guide for turning a Next.js app into a Telegram Web App (TWA) using the `@twa-dev/sdk`, enabling a seamless experience for Telegram users. Since users are already logged into Telegram, they can jump straight into using your app without additional sign-ins.

With this setup, you can fetch user data directly, allowing you to personalize content and store information easily, even without a dedicated backend.

## Overview

This example includes:
- Setting up a **Next.js project** with **TypeScript** and **App Router**
- Configuring `@twa-dev/sdk` to manage user authentication in a TWA
- Fetching and displaying user data such as ID and username within the app

## Quickstart

Clone the repository or use it as a reference:

[GitHub Repository](https://github.com/bz-hashtag-0780/web-app-to-twa) | [Live Demo](https://t.me/WebAppToTwaBot/webapp)

## Getting Started

1. **Set Up Next.js with TypeScript**:
   ```bash
   npx create-next-app@latest my-telegram-app --typescript --use-npm
   cd my-telegram-app
   npm install @twa-dev/sdk --legacy-peer-deps
   ```

2. **Authentication Context Setup**:
   Create `AuthContext.tsx` in a `context` folder, using `@twa-dev/sdk` to manage and provide Telegram user data across the app.

3. **Wrap the App with `AuthContextProvider`**:
   Update `layout.tsx` to make the context globally accessible.

4. **UI Setup**:
   Use the `useAuth` hook in `page.tsx` to access and display user information such as ID, username, and viewport height.

5. **Deploy**:
   Deploy your app on [Vercel](https://vercel.com/) or a preferred hosting platform.

6. **Create a Telegram Bot and Set Up TWA**:
   - Go to [BotFather](https://t.me/BotFather) and create a new bot using `/newbot`.
   - Use `/newapp` to convert the bot into a TWA and set its domain to your deployment URL.

## Conclusion

This tutorial guides you through setting up a Next.js app with TypeScript, configuring a Telegram Web App with `@twa-dev/sdk`, and displaying authenticated user data from Telegram within your app.

For further details, please refer to the [tutorial on Notion](https://flowfoundation.notion.site/Authenticate-Users-Using-TWA-in-Next-js-b9f5b5b73f534f3e9cfb27f35f2488ef).
