# Authenticate users using @twa-dev/sdk in your Next.js frontend

## Submit Your Solution

-   Submit your deeplink and GitHub repo in the README.md in the [solutions folder](solution/README.md)

## Example

View [Live Demo](https://t.me/WebAppToTwaBot/webapp)

View [Github Example](https://github.com/bz-hashtag-0780/web-app-to-twa/)

![Live Demo Example](../assets/images/image7.gif)

---

This guide walks you through turning a Next.js app into a Telegram Web App (TWA), letting you create a more seamless experience for Telegram users.

Since users are already logged into Telegram, they don’t need to sign in again, which means they can jump straight into using your app.

With this setup, you can fetch user data directly, allowing you to personalize content and store information easily, even without a dedicated backend.

## Step 1: Set Up a Next.js project with TypeScript and App Router

### 1. Run the command in your terminal

`bash npx create-next-app@latest my-telegram-app --typescript --use-npm`
​

### 2. Navigate to Your Project Directory

`bash cd my-telegram-app`
​

### 3. Install the @twa-dev/sdk with the —legacy-peer-deps flag

`bash npm install @twa-dev/sdk --legacy-peer-deps`

## Step 2: Set Up the Authentication Context with @twa-dev/sdk

We’ll use React’s Context API to manage authentication and Telegram Web App data, making it available across our app.

### 1. Create an `AuthContext.tsx` in a new `context` folder under `app`

```typescript
// app/context/AuthContext.tsx
'use client';

import React, { createContext, useContext, useEffect, useState } from 'react';
import WebApp from '@twa-dev/sdk';

type AuthContextType = {
	userID: number | null;
	username: string | null;
	windowHeight: number;
};

const AuthContext = createContext<AuthContextType | undefined>(undefined);

export const AuthContextProvider = ({
	children,
}: {
	children: React.ReactNode;
}) => {
	const [windowHeight, setWindowHeight] = useState<number>(0);
	const [userID, setUserID] = useState<number | null>(null);
	const [username, setUsername] = useState<string | null>(null);

	useEffect(() => {
		// Ensure this code only runs on the client side
		if (typeof window !== 'undefined' && WebApp) {
			WebApp.isVerticalSwipesEnabled = false;
			setWindowHeight(WebApp.viewportStableHeight || window.innerHeight);
			WebApp.ready();

			// Set Telegram user data
			const user = WebApp.initDataUnsafe.user;
			setUserID(user?.id || null);
			setUsername(user?.username || null);
		}
	}, []);

	const contextValue = {
		userID,
		username,
		windowHeight,
	};

	return (
		<AuthContext.Provider value={contextValue}>
			{children}
		</AuthContext.Provider>
	);
};

export const useAuth = () => {
	const context = useContext(AuthContext);
	if (context === undefined) {
		throw new Error('useAuth must be used within an AuthContextProvider');
	}
	return context;
};
```

## Step 3: Wrap your App with `AuthContextProvider`

1. Update `layout.tsx` to wrap the entire app

```typescript
// app/layout.tsx
import './globals.css';
import { AuthContextProvider } from '@/context/AuthContext';

export default function RootLayout({
	children,
}: Readonly<{
	children: React.ReactNode;
}>) {
	return (
		<html lang="en">
			<body>
				<AuthContextProvider>{children}</AuthContextProvider>
			</body>
		</html>
	);
}
```

## Step 4: Create DisplayUser.tsx and use it on Home Page

To test if it works, we’ll use the `useAuth` hook from `AuthContext` to access and display the Telegram-authenticated user’s ID, username, and viewport height.

### 1. Create `components/DisplayUser.tsx`

```typescript
// components/DisplayUser.tsx
'use client';

import { useAuth } from '@/context/AuthContext';

export default function DisplayUser() {
	const { userID, username, windowHeight } = useAuth();

	return (
		<div className="flex flex-col items-center justify-center min-h-screen text-center space-y-4">
			<h1 className="text-4xl font-bold">
				Welcome to the Telegram Web App!
			</h1>
			<p>User ID: {userID || 'Not available'}</p>
			<p>Username: {username || 'Not available'}</p>
			<p>Window Height: {windowHeight}</p>
		</div>
	);
}
```

### 2. Create `app/page.tsx`

```typescript
// app/page.tsx
import DisplayUser from '@/components/DisplayUser';

export default function Home() {
	return (
		<div>
			<DisplayUser />
		</div>
	);
}
```

## Step 5: Deploy your frontend to Vercel

### 1. Deploy your Next.js app to [Vercel](https://vercel.com/) (or your preferred hosting platform)

<img src="../assets/images/image8.webp" alt="Website Deployment" width="500" />

## Step 6: Create a Telegram Bot and Turn your Web App into a TWA

### 1. Go to [BotFather](https://t.me/BotFather) on Telegram and create a new bot

```bash
/newbot
```

### 2. Use `/newapp` command in BotFather to turn your web app into a TWA

```bash
/newapp
```

### 3. Set your bot’s domain to your deployment URL (e.g. https://web-app-to-twa.vercel.app/)

This will create a deep link (e.g. https://t.me/WebAppToTwaBot/webapp) that you can access to check if your telegram web app display’s the user’s id and username

<img src="../assets/images/image9.webp" alt="Final Result" width="300" />

## Conclusion

This tutorial takes you through setting up a Next.js app with TypeScript, configuring a Telegram Web App with @twa-dev/sdk, and displaying authenticated user data from Telegram within your app.
