---
title: "权限认证工具Clerk"
date: 2025-04-06T18:34:25+08:00
lastmod: 2025-04-06T22:54:22+08:00
draft: false
math: true
categories:
- 编程
- 计算机
tags:
- 权限认证
# description->需要自己编写的文章描述，是搜索引擎呈现在搜索结果链接下方的网页简介，建议设置
description: ""
weight: # 输入1可以顶置文章，用来给文章展示排序，不填就默认按时间排序
slug: ""
draft: false # 是否为草稿
comments: true
showToc: true # 显示目录
TocOpen: true # 自动展开目录
hidemeta: false # 是否隐藏文章的元信息，如发布日期、作者等
disableShare: true # 底部不显示分享栏
---

# 前言

以前使用过Clerk，但没有写过相关内容。这次没用使用Clerk做权限认证，但仍有必要写点东西给自己留点记忆。

# Clerk简介

[官网](https://clerk.com/docs)

## [Explore by frontend framework](https://clerk.com/docs#explore-by-frontend-framework)

### [Next.js](https://clerk.com/docs/quickstarts/nextjs)

Easily add secure, beautiful, and fast authentication to Next.js with Clerk.

### [React](https://clerk.com/docs/quickstarts/react)

Get started installing and initializing Clerk in a new React + Vite app.

### [Astro](https://clerk.com/docs/quickstarts/astro)

Easily add secure and SSR-friendly authentication to your Astro application with Clerk.

### [Chrome Extension](https://clerk.com/docs/quickstarts/chrome-extension)

Use the Chrome Extension SDK to authenticate users in your Chrome extension.

### [Expo](https://clerk.com/docs/quickstarts/expo)

Use Clerk with Expo to authenticate users in your React Native application.

### [iOS](https://clerk.com/docs/quickstarts/ios)

Use the Clerk iOS SDK to authenticate users in your native Apple applications.

### [JavaScript](https://clerk.com/docs/quickstarts/javascript)

The Clerk JavaScript SDK gives you access to prebuilt components and helpers to make user authentication easier.

### [Nuxt](https://clerk.com/docs/quickstarts/nuxt)

Easily add secure, beautiful, and fast authentication to Nuxt with Clerk.

### [React Router](https://clerk.com/docs/quickstarts/react-router)

Easily add secure, edge- and SSR-friendly authentication to React Router with Clerk.

### [Remix](https://clerk.com/docs/quickstarts/remix)

Easily add secure, edge- and SSR-friendly authentication to Remix with Clerk.
### [TanStack React StartBeta](https://clerk.com/docs/quickstarts/tanstack-react-start)

Easily add secure and SSR-friendly authentication to your TanStack React Start application with Clerk.
### [Vue](https://clerk.com/docs/quickstarts/vue)

Get started installing and initializing Clerk in a new Vue + Vite app.

## [Explore by backend framework](https://clerk.com/docs#explore-by-backend-framework)

### [JS Backend SDK](https://clerk.com/docs/references/backend/overview)

The Clerk Backend SDK exposes our Backend API resources and low-level authentication utilities for JavaScript environments.

### [C#](https://github.com/clerk/clerk-sdk-csharp/blob/main/README.md)

The Clerk C# SDK is a wrapper around our Backend API to make it easier to integrate Clerk into your backend.

### [Express](https://clerk.com/docs/quickstarts/express)

Quickly add authentication and user management to your Express application.

### [Go](https://clerk.com/docs/references/go/overview)

The Clerk Go SDK is a wrapper around the Backend API written in Golang to make it easier to integrate Clerk into your backend.

### [Fastify](https://clerk.com/docs/quickstarts/fastify)

Build secure authentication and user management flows for your Fastify server.

### [Python](https://github.com/clerk/clerk-sdk-python/blob/main/README.md)

The Clerk Python SDK is a wrapper around the Backend API written in Python to make it easier to integrate Clerk into your backend.

### [Ruby on Rails](https://clerk.com/docs/quickstarts/ruby)

Integrate authentication and user management into your Ruby application.

## [Explore by feature](https://clerk.com/docs#explore-by-feature)

### [Authentication](https://clerk.com/docs/authentication/overview)

Clerk supports multiple authentication strategies so you can implement the strategy that makes sense for your users.

### [User management](https://clerk.com/docs/users/overview)

Complete user management. Add sign up, sign in, and profile management to your application in minutes.

### [Database integrations](https://clerk.com/docs/integrations/overview)

Enable Clerk-managed users to authenticate and interact directly with your database with Clerk's integrations.

### [Customization](https://clerk.com/docs/customization/overview)

Clerk's components can be customized to match the look and feel of your application.

### [Organizations](https://clerk.com/docs/organizations/overview)

Organizations are shared accounts, useful for project and team leaders. Members with elevated privileges can manage member access to the organization's data and resources.

### [SDKs](https://clerk.com/docs/references/overview)

Clerk's SDKs allow you to call the Clerk server API without having to implement the calls yourself.

# Vue Clerk

Clerk composables and components

Easiest way to add authentication and user management to your Vue application

[What is Vue Clerk?](https://vue-clerk.vercel.app/what-is-vue-clerk)

[Quickstart](https://vue-clerk.vercel.app/getting-started)

[View on GitHub](https://github.com/wobsoriano/vue-clerk)

## Pre-built Components

Components for sign up, sign in, user management, and more.

## Composables

Composables for working with user, session and more.

## Authentication & Users

Passwords, SSO, OTP, MFA and other advanced security features.
## Getting Started[​](https://vue-clerk.vercel.app/getting-started#getting-started)

You need to create a Clerk Application in your [Clerk Dashboard](https://dashboard.clerk.com/) before you can set up Vue Clerk. For more information, check out our [Set up your application](https://clerk.com/docs/authentication/set-up-your-application) guide.

### 1. Set up a Vue application use Vite[​](https://vue-clerk.vercel.app/getting-started#_1-set-up-a-vue-application-use-vite)

Scaffold your new Vue application using [Vite](https://vitejs.dev/guide/#scaffolding-your-first-vite-project).

```bash
npm create vite@latest vue-clerk-quickstart --template vue-ts
cd vue-clerk-quickstart
npm install
npm run dev
```

### 2. Install Vue Clerk[​](https://vue-clerk.vercel.app/getting-started#_2-install-vue-clerk)

The Vue Clerk SDK gives you access to prebuilt components, composables, and helpers for Vue.

To get started using Clerk with Vue, add the SDK to your project:

```
npm install vue-clerk
```

### 3. Set your environment variables[​](https://vue-clerk.vercel.app/getting-started#_3-set-your-environment-variables)

1. If you don't have an `.env.local` file in the root directory of your Vue project, create one now.
2. Find your Clerk publishable key. If you're signed into Clerk, the `.env.local` snippet below will contain your key. Otherwise:

- Navigate to the [Clerk Dashboard](https://dashboard.clerk.com/) and select your application.
- In the navigation sidebar, select API Keys.
- You can copy your key from the Quick Copy section.

3. Add your key to your `.env.local` file.

The final result should look like this:

```
VITE_CLERK_PUBLISHABLE_KEY=pk_test_************************
```

### 4. Import the Clerk publishable key[​](https://vue-clerk.vercel.app/getting-started#_4-import-the-clerk-publishable-key)

You will need to import your Clerk publishable key into your application. You can add an `if` statement to check that it is imported and that it exists. This will prevent running the application without the publishable key, and will also prevent TypeScript errors.

```ts
import { createApp } from 'vue'
import App from './App.vue'

const PUBLISHABLE_KEY = import.meta.env.VITE_CLERK_PUBLISHABLE_KEY

if (!PUBLISHABLE_KEY) {
  throw new Error('Missing Publishable Key')
}

const app = createApp(App)
app.mount('#app')
```
### 5. Add the Clerk plugin to your app[​](https://vue-clerk.vercel.app/getting-started#_5-add-the-clerk-plugin-to-your-app)

The plugin provides active session and user context.

To make this data available across your entire app, install the Clerk plugin. You must pass your publishable key as a prop to the plugin.

```ts
import { createApp } from 'vue'
import App from './App.vue'
import { clerkPlugin } from 'vue-clerk'

const PUBLISHABLE_KEY = import.meta.env.VITE_CLERK_PUBLISHABLE_KEY

if (!PUBLISHABLE_KEY) {
  throw new Error('Missing Publishable Key')
}

const app = createApp(App)
app.use(clerkPlugin, {
  publishableKey: PUBLISHABLE_KEY
})
app.mount('#app')
```

### 6. Create a header with Clerk components[​](https://vue-clerk.vercel.app/getting-started#_6-create-a-header-with-clerk-components)

You can control which content signed in and signed out users can see with Clerk's [prebuilt components](https://clerk.com/docs/components/overview). To get started, create a header for your users to sign in or out. To do this, you will use:

- [`<SignedIn>`](https://vue-clerk.vercel.app/components/control/signed-in): Children of this component can only be seen while signed in.
- [`<SignedOut>`](https://vue-clerk.vercel.app/components/control/signed-out): Children of this component can only be seen while signed out.
- [`<UserButton />`](https://vue-clerk.vercel.app/components/user/user-button): A prebuilt component that comes styled out of the box to show the avatar from the account the user is signed in with.
- [`<SignInButton />`](https://vue-clerk.vercel.app/components/unstyled/sign-in-button): An unstyled component that links to the sign-in page or displays the sign-in modal.

```vue
<script setup>
import { SignedIn, SignedOut, SignInButton, UserButton } from 'vue-clerk'
</script>

<template>
  <SignedOut>
    <SignInButton />
  </SignedOut>
  <SignedIn>
    <UserButton />
  </SignedIn>
</template>
```

Then, visit your app's homepage at [http://localhost:5173](http://localhost:5173/) while signed out to see the sign-in button. Once signed in, your app will render the user button.












