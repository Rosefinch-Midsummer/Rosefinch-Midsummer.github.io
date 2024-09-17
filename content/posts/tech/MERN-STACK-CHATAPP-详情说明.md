---
title: "MERN-STACK-CHATAPP-详情说明"
date: 2024-09-17T12:34:25+08:00
lastmod: 2024-09-17T22:54:22+08:00
draft: false
math: true
categories:
- 编程
tags:
- 聊天工具
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

# Build and Deploy a Complete Chat App with MERN Stack | JWT, Socket.io, MongoDB | Beginner Friendly

[在线试用](https://chatapp-tianhan.onrender.com)

[Youtube视频链接](https://www.youtube.com/watch?v=HwCqsOis894)

[原作者GitHub仓库链接](https://github.com/burakorkmez/mern-chat-app)

[本人Github仓库链接](https://github.com/Rosefinch-Midsummer/ChatAPP)

## 简介

Build a Realtime Chat App with MERN Stack. Completely beginner friendly.

Some Features of This App:

- 🌟 Tech stack: MERN + Socket.io + TailwindCSS + Daisy UI
- 🎃 Authentication && Authorization with JWT
- 👾 Real-time messaging with Socket.io   
- 🚀 Online user status (Socket.io and React Context)
- 👌  Global state management with Zustand
- 🐞 Error handling both on the server and on the client
- ⭐ At the end Deployment like a pro for FREE!
- ⏳ And much more!


## 项目使用说明

Setup .env file

```
PORT=...
MONGO_DB_URI=...
JWT_SECRET=...
NODE_ENV=...
```

Build the app

```shell
npm run build
```

Start the app

```shell
npm start
```

## 开发过程 Timestamps

### 00:00:00 - Demo App
### 00:02:18 - Project Setup

执行如下两条命令

```
cd frontend
npm create vite@latest .
```

成功时输出如下信息：

```
> npx
> create-vite .

? Select a framework: › - Use arrow-keys. Return to submit.
❯   Vanilla
? Select a framework: › - Use arrow-keys. Return to submit.
    Vanilla
? Select a framework: › - Use arrow-keys. Return to submit.
    Vanilla
? Select a framework: › - Use arrow-keys. Return to submit.
    Vanilla
? Select a framework: › - Use arrow-keys. Return to submit.
    Vanilla
✔ Select a framework: › React
✔ Select a variant: › JavaScript

Scaffolding project in /home/username/chatapp/frontend...

Done. Now run:

  npm install
  npm run dev
```

接着执行如下两条命令

```
npm install
npm run dev
```

执行`npm install`输出信息如下：

```
added 264 packages in 3m

102 packages are looking for funding
  run `npm fund` for details
```

执行`npm run dev`输出信息如下：

```
> frontend@0.0.0 dev
> vite


  VITE v5.4.5  ready in 290 ms

  ➜  Local:   http://localhost:5173/
  ➜  Network: use --host to expose
  ➜  press h + enter to show help
```

`ctrl+c`终止后执行`cd ..`返回上一级目录

执行`npm init -y`此时`chatapp`目录下生成了`package.json`文件

```
Wrote to /home/username/chatapp/package.json:

{
  "name": "chatapp",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "description": ""
}
```

然后把`chatapp/package.json`中的`"main": "index.js"`换成`"main": "server.js"`，并在`backend`目录下添加`server.js`文件

在`chatapp`目录下执行`npm install express dotenv cookie-parser bcryptjs mongoose socket.io jsonwebtoken`，输出信息如下：

```
added 125 packages in 4s

15 packages are looking for funding
  run `npm fund` for details

```

把`chatapp/package.json`中的`"test": "echo \"Error: no test specified\" && exit 1"`替换为`"server": "node backend/server.js"`

在`chatapp`目录下执行`npm run server`出现如下信息：

```
> chatapp@1.0.0 server
> node backend/server.js

Server Running on port 5000
```

在`chatapp`目录下执行`npm install nodemon --save-dev`出现如下信息：

```

added 28 packages in 2s

19 packages are looking for funding
  run `npm fund` for details
```

把`chatapp/package.json`中的`"server": "node backend/server.js"`替换为`"server": "nodemon backend/server.js"`

目的：实现不重启更新内容

仍旧使用`npm run server`启动

添加`.env`文件

添加`dotenv` VSCode扩展（这个貌似可以省略）

在把`chatapp/package.json`中添加`"type": "module",`

然后可以把server.js中的`const express = require("express"); const dotenv = require("dotenv");`替换成`import express from "express"; import dotenv from "dotenv";`

### 00:12:20 - Auth Routes Setup

测试样本

```js
app.get("/", (req, res) => {
     //root route http://localhost:5000/
     res.send("Hello baobaodaren!");
 })
```

为了代码的维护，要把本该写入 `server.js`中的

```js
app.get("/api/auth/signup", (req, res) => {
    console.log("signup route");
})
app.get("/api/auth/login", (req, res) => {
    console.log("login route");
})
app.get("/api/auth/logout", (req, res) => {
    console.log("logout route");
})
```

变成：

```js
app.use("/api/auth", authRoutes);
```

然后在`backend`目录下创建`routes/auth.routes.js`文件

在`server.js`中引用时需要加上`.js`后缀例如`import authRoutes from "./routes/auth.routes.js";`

此时`auth.routes.js`文件内容如下：

```js
import express from "express";

const router = express.Router();

router.get("/signup", (req, res) => {
    res.send("signup route");
})
router.get("/login", (req, res) => {
    res.send("login route");
})
router.get("/logout", (req, res) => {
    res.send("logout route");
})
export default router;
```

然后抽象出controllers组件

配置 PostMan

### 00:23:20 - MongoDB Setup

https://cloud.mongodb.com/

创建新的 Project

从`Security`下的`quickstart`处获取数据库密码 xxxxxxpassword

Create a database user using a username and password. Users will be given the _read and write to any database_ [privilege](https://docs.atlas.mongodb.com/security-add-mongodb-users/#database-user-privileges) by default. You can update these permissions and/or create additional users later. Ensure these credentials are different to your MongoDB Cloud username and password.

Add your connection string into your application code

Use this connection string in your application

View full code sample

```
mongodb+srv://username:<db_password>@cluster0.mmsyy.mongodb.net/chatapp?retryWrites=true&w=majority&appName=Cluster0
```

其中`chatapp`是需要手动添加的数据库名称

### 00:28:30 - Create User Model 

创建 User 表

注意：暂时没有加入时间戳
### 00:32:20 - Sign Up Endpoint

### 00:45:00 - Generate JWT 

JWT_SECRET 可以是任意值，推荐使用`openssl rand -base64 32`生成一个 32 位的独特字符串例如`/A/c2fLb5Ui+10KS8C01rRh0u5jjVwcx7mn+ItaCCNQ=`

`utils/generateToken.js`：

```js
import jwt from "jsonwebtoken";

const generateTokenAndSetCookie = (userId, res) => {
	const token = jwt.sign({ userId }, process.env.JWT_SECRET, {
		expiresIn: "15d",
	});

	res.cookie("jwt", token, {
		maxAge: 15 * 24 * 60 * 60 * 1000, // MS
		httpOnly: true, // prevent XSS attacks cross-site scripting attacks
		sameSite: "strict", // CSRF attacks cross-site request forgery attacks
		secure: process.env.NODE_ENV !== "development",
	});
};

export default generateTokenAndSetCookie;
```

Token 和 Cookie 是用于在 Web 应用程序中进行身份验证和授权的两种常用方法，它们之间的主要区别如下：

1. 存储位置：
- Cookie 存储在客户端的浏览器中，它是作为 HTTP 头部发送给服务器的一小段文本信息，用于存储会话信息、用户偏好设置等。
- Token 则通常存储在客户端的本地存储或内存中，一般是作为 JSON Web Token (JWT) 的形式存储在客户端，它包含了用户的身份信息和权限信息，并通过签名和加密保护其完整性和安全性。在 Web 应用程序中，Token 是通过在 HTTP 请求头中发送给服务器进行认证和授权的。

2. 安全性：
- Cookie 存储在客户端的浏览器中，可能会受到一些安全风险，比如跨站点脚本攻击（XSS）、跨站点请求伪造（CSRF）等，因此需要设置相关的安全选项来增强其安全性。
- Token 由于是存储在客户端本地，只有在服务器端进行验证才能起到作用，因此相对来说更为安全，可以通过设置签名和加密来保护其安全性。

3. 可移植性：
- Token 可以在不同的系统和应用之间进行传递和共享，因为它是一个标准格式的数据结构，而且不依赖于特定的应用程序或服务器实现。
- Cookie 则局限于特定的域和路径，只能在设置了Cookie的域下进行传递和共享。

综上所述，Token 相对于 Cookie 来说更为灵活、安全和通用，因此在现代 Web 应用程序中更加常用和推荐使用。

添加`NODE_ENV`环境变量

### 00:52:50 - Login Endpoint

`const isPasswordCorrect = await bcrypt.compare(password, user?.password || "");`后面必须带`""`，不然无法处理某些特殊情况

### 00:56:50 - Logout Endpoint


### 00:58:50 - Create Message Model

启用三个model的时间戳

### 01:03:10 - Create Conversation Model

启用三个model的时间戳

### 01:06:15 - Send Message Endpoint


### 01:10:11 - Protect Route Middleware

报错`Error in protectRoute middleware:  Cannot read properties of undefined (reading 'jwt')`

报错是因为`jwt`没有被正确导入，可能是因为没有正确安装`jsonwebtoken`包导致的。请确保在项目中安装了`jsonwebtoken`包，并且在文件中正确导入。

你可以尝试以下步骤来解决问题：

1. 在项目根目录下打开终端，并执行以下命令安装`jsonwebtoken`包：
   ```
   npm install jsonwebtoken
   ```

2. 确保`jsonwebtoken`包已经正确安装，并且在文件中正确导入，代码如下：
   ```js
   import jwt from "jsonwebtoken";
   ```

3. 如果上述步骤都已经完成，但仍然报错，可以尝试删除`node_modules`文件夹并重新安装依赖：
   ```
   rm -rf node_modules
   npm install
   ```

通过以上步骤，应该可以解决`Error in protectRoute middleware: Cannot read properties of undefined (reading 'jwt')`报错问题。


解决办法：在`server.js`中添加如下两条语句

```js
import cookieParser from "cookie-parser";
app.use(cookieParser());
```

I would suspect your sending your JWT token as an authentication header bearer token not as a Cookie, therefore the cookie jwt does not exist. Can you please check how the token is being provided in Postman (see Authorziation tab in request/ collection or have a look at the request in the Postman console and check Set-Cookie and Authentication headers) and edit the post accordingly. 

You should never get this error since the req.cookies should be by default an empty object so the question is do you use cookie-parser ?? 

I had forgotten to add cookie parser. Thank you for pointing it out. 

### 01:25:10 - Get Messages Endpoint

POSTMAN 测试无法获得正确 Message

### 01:31:20 - Get Users for Sidebar Endpoint

获取侧边栏用户（不包含自身）

git 提交但要忽略 .env

### 01:38:19 - UI Design

执行如下指令

```
cd frontend
npm run dev
```

输出如下内容：

```
> frontend@0.0.0 dev
> vite


  VITE v5.4.5  ready in 611 ms

  ➜  Local:   http://localhost:5173/
  ➜  Network: use --host to expose
  ➜  press h + enter to show help
```

https://tailwindcss.com/docs/guides/vite

在`frontend`目录下执行`npm install -D tailwindcss postcss autoprefixer`

输出结果如下：

```

added 85 packages in 8s

125 packages are looking for funding
  run `npm fund` for details
```

再执行`npx tailwindcss init`

```
Created Tailwind CSS config file: tailwind.config.js
```

`npx tailwindcss init -p`和`npx tailwindcss init`有什么区别？

`npx tailwindcss init` 是在当前目录下初始化 Tailwind CSS 的配置文件，而`-p`选项表示在 package.json 文件中添加 Tailwind CSS 的 npm script。所以两者的区别在于是否添加了 npm script。

添加 npm script 可以让您通过命令行更方便地运行一些常用的操作，比如编译 CSS 文件、启动开发服务器等。如果您经常需要在项目中使用 Tailwind CSS，那么添加 npm script 可以帮助您更快速地执行这些操作，提高工作效率。如果您并不打算经常使用 Tailwind CSS，或者有其他方式来编译 CSS 文件，那么可以选择不添加 npm script。至于具体使用与否，取决于您个人的开发需求和习惯。

补充执行`npx tailwindcss init -p`输出如下信息：

```

tailwind.config.js already exists.
Created PostCSS config file: postcss.config.js
```

此时才不影响`daisyui`生效

手动把生成的`tailwind.config.js`变成如下形式：

```js
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{ts,js,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

向`index.css`文件中加入如下内容：

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

安装`daisyUI`  

[The most popular component library for Tailwind CSS](https://daisyui.com/docs/install/)

`npm i -D daisyui@latest`

输出信息如下：

```

added 4 packages in 5s

126 packages are looking for funding
  run `npm fund` for details
```

Add daisyUI to tailwind.config.js:

```js
module.exports = {
  //...
  plugins: [
    require('daisyui'),
  ],
}
```

删除App.css中所有内容

可以在VSCode中添加TailwindCSS  Intelligent插件、安装ES7+ React/Redux 插件


在public下增加bg.png

https://tailwindcss-glassmorphism.vercel.app/


Login.jsx中`{"Don't"} have an account?`要加{}否则报错

此时的App.jsx内容如下：

```jsx
import './App.css'
import Login from "./pages/login/Login";

function App() {

  return (
    <>
      <div className='p-4 h-screen flex items-center justify-center'>
			<Login />
		</div>
    </>
  )
}

export default App

```

安装 `react-icons`

https://react-icons.github.io/react-icons/

执行`npm install react-icons --save`

输出结果如下：

```

added 1 package in 8s

126 packages are looking for funding
  run `npm fund` for details
```

确定基本框架

在index.css中添加如下内容：

```css
/* dark mode looking scrollbar */
::-webkit-scrollbar {
	width: 8px;
}

::-webkit-scrollbar-track {
	background: #555;
}

::-webkit-scrollbar-thumb {
	background: #121212;
	border-radius: 5px;
}

::-webkit-scrollbar-thumb:hover {
	background: #242424;
}
```


### 02:27:50 - SignUp Functionality

在`frontend`目录下安装`react-router-dom`

```
cd frontend
npm i react-router-dom
```

输出信息如下：

```
added 3 packages in 3s

126 packages are looking for funding
  run `npm fund` for details
```

修改`main.jsx`增加`BrowserRouter`

```jsx
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import App from './App.jsx'
import './index.css'
import { BrowserRouter } from "react-router-dom";

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </StrictMode>,
)
```

然后在`App.jsx`中引入`<Routes></Routes>`

```jsx
import { Route, Routes } from "react-router-dom";
import "./App.css";
import Home from "./pages/home/Home";
import Login from "./pages/login/Login";
import SignUp from "./pages/signup/SignUp";


function App() {
	return (
		<div className='p-4 h-screen flex items-center justify-center'>
			<Routes>
				<Route path='/' element={<Home /> } />
				<Route path='/login' element={<Login />} />
				<Route path='/signup' element={<SignUp />} />
			</Routes>
		</div>
	);
}

export default App;

```

修改前端启动端口号，对应文件内容为`vite.config.js`

```js
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react()],
  server: {
    port: 3000,
  }
})
```

使用`<Link></Link>切换`属性为`to='/signup'`

在`.eslintrc.cjs`下的`rules`中添加`"react/prop-types":"off",`

我这里并没有添加，因为我这里只有`eslint.config.js`文件，事后证明两种方式都行。

这两个文件都是用于配置eslint规则的文件，主要作用是定义代码规范，检测代码质量，帮助开发团队在遵循一致的代码规范的同时提高代码质量。

它们的区别在于，`.eslintrc.cjs`是CommonJS模块形式的配置文件，而`eslint.config.js`是ES module形式的配置文件。二者在配置规则和使用方法上没有本质区别，只是写法稍有不同。

要生成这两个文件，可以通过使用eslint官方提供的`--init`选项来生成初始配置文件，具体操作如下：

1. 在项目根目录下执行以下命令初始化eslint配置文件：

```
npx eslint --init
```

2. 然后按照提示选择配置选项，最终生成`.eslintrc.cjs`或`eslint.config.js`文件。

增加`hooks/useSignUp.js`文件

安装`react-hot-toast`组件

[The Best Toast in Town. Smoking hot React notifications.](https://react-hot-toast.com/)

执行指令：

```
cd frontend
npm i react-hot-toast
```

输出信息如下：

```
added 2 packages in 3s

126 packages are looking for funding
  run `npm fund` for details
```

在`App.jsx`中启用

```jsx
import { Route, Routes } from "react-router-dom";
import "./App.css";
import Home from "./pages/home/Home";
import Login from "./pages/login/Login";
import SignUp from "./pages/signup/SignUp";
import { Toaster } from "react-hot-toast";

function App() {
	return (
		<div className='p-4 h-screen flex items-center justify-center'>
			<Routes>
				<Route path='/' element={<Home /> } />
				<Route path='/login' element={<Login />} />
				<Route path='/signup' element={<SignUp />} />
			</Routes>
      <Toaster />
		</div>
	);
}

export default App;

```

前后端交互方式：

```jsx
const res = await fetch("/api/auth/signup", {
				method: "POST",
				headers: { "Content-Type": "application/json" },
				body: JSON.stringify({ fullName, username, password, confirmPassword, gender }),
			});
```

前端启动`npm run dev`

后端启动`npm run server`

避免提交数据时出现Cors报错在`vite.config.js`中添加如下内容：

```js
proxy: {
      "/api": {
        target: "http://localhost:5000",
      }
    }
```

重启前端

注意：这里`fetch("/api/auth/signup"`是省略写法，如果不添加proxy则前面还应该有`http://localhost:5000`

### 02:50:00 - Create AuthContext 

Web聊天工具中的AuthContext是一个用来管理用户身份验证和授权信息的上下文对象。它通常用来存储用户的登录状态、权限信息以及其他与用户身份相关的数据。使用AuthContext可以方便地对用户进行身份验证，并在需要进行权限验证时进行检查。具体作用包括但不限于：

1. 管理用户的登录状态：AuthContext可以存储用户的登录信息，如用户的登录名和密码等，以便对用户进行身份验证。

2. 存储用户的权限信息：AuthContext可以存储用户的权限信息，如用户所拥有的角色、权限等，以便在需要进行权限验证时进行检查。

3. 提供用户身份验证的方法：AuthContext提供了一些方法来进行用户身份验证，例如登录、注销等操作。

4. 提供访问权限控制：AuthContext可以通过检查用户的权限信息来限制用户对某些功能的访问，以增强系统的安全性。

总的来说，AuthContext在Web聊天工具中扮演着用户身份验证和权限管理的重要角色，可以帮助确保用户的安全和数据的保护。

在`main.jsx`中引入

```jsx
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import App from './App.jsx'
import './index.css'
import { BrowserRouter } from "react-router-dom";
import { AuthContextProvider } from './context/AuthContext.jsx';

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <BrowserRouter>
      <AuthContextProvider>
        <App />
      </AuthContextProvider>
    </BrowserRouter>
  </StrictMode>,
)
```

在`App.jsx`中引入

```jsx
import { Navigate, Route, Routes } from "react-router-dom";
import "./App.css";
import Home from "./pages/home/Home";
import Login from "./pages/login/Login";
import SignUp from "./pages/signup/SignUp";
import { Toaster } from "react-hot-toast";
import { useAuthContext } from "./context/AuthContext";

function App() {
	const { authUser } = useAuthContext();
	return (
		<div className='p-4 h-screen flex items-center justify-center'>
			<Routes>
				<Route path='/' element={authUser ? <Home /> : <Navigate to={"/login"} />} />
				<Route path='/login' element={authUser ? <Navigate to='/' /> : <Login />} />
				<Route path='/signup' element={authUser ? <Navigate to='/' /> : <SignUp />} />
			</Routes>
			<Toaster />
		</div>
	);
}

export default App;
```

引入之后不用每次都登陆

### 02:59:00 - Logout Functionality

登出会删除本地存储空间中的数据

### 03:03:20 - Login Functionality

### 03:11:50 - Get Conversations

添加`ZUSTAND`在`frontend`目录下执行`npm i zustand`

输出结果如下：

```
added 1 package in 5s

126 packages are looking for funding
  run `npm fund` for details
```

https://zustand-demo.pmnd.rs/

A small, fast, and scalable bearbones state management solution. Zustand has a comfy API based on hooks. It isn't boilerplatey or opinionated, but has enough convention to be explicit and flux-like.

Don't disregard it because it's cute, it has claws! Lots of time was spent to deal with common pitfalls, like the dreaded [zombie child problem](https://react-redux.js.org/api/hooks#stale-props-and-zombie-children), [React concurrency](https://github.com/bvaughn/rfcs/blob/useMutableSource/text/0000-use-mutable-source.md), and [context loss](https://github.com/facebook/react/issues/13332) between mixed renderers. It may be the one state manager in the React space that gets all of these right.

You can try a live demo [here](https://codesandbox.io/s/dazzling-moon-itop4).

Zustand is available as a package on NPM for use:

```bash
# NPM
npm install zustand
# Or, use any package manager of your choice.
```

`zustand` 是一个用于管理 React 状态的轻量级库，主要作用是提供一个简单而强大的状态管理解决方案。它可以帮助开发者在 React 应用中更方便地创建和管理状态，而无需引入复杂的状态管理工具，如 Redux。

`zustand` 的主要特点包括：

1. 简单易用：使用简单的 API 和语法，减少了状态管理的复杂性。
2. 高效：采用了基于 Proxy 对象的响应式状态更新机制，可以高效地追踪状态变化。
3. 轻量级：整个库只有几百行代码，没有任何依赖，不会增加应用的体积。
4. 声明式：状态的声明和更新是直接的，可以提高代码的可读性和维护性。
5. 支持胶水代码：可以很好地与其他状态管理库或工具结合使用。

总的来说，`zustand` 可以帮助开发者更加轻松地管理 React 应用的状态，并且提供了灵活性和性能优势。

创建zustand目录或store目录创建`useConversation.js`

下面的代码的作用是什么？

```js
import { create } from "zustand";

const useConversation = create((set) => ({
	selectedConversation: null,
	setSelectedConversation: (selectedConversation) => set({ selectedConversation }),
	messages: [],
	setMessages: (messages) => set({ messages }),
}));

export default useConversation;
```

这段代码使用了 `zustand` 库来创建了一个自定义的状态管理 hook，名为 `useConversation`。这个 hook 包含了两个状态变量 `selectedConversation` 和 `messages`，以及对应的更新方法 `setSelectedConversation` 和 `setMessages`。

- `selectedConversation` 用来存储当前选中的对话信息。
- `setSelectedConversation` 是一个函数，用来更新 `selectedConversation` 的值。
- `messages` 用来存储对话消息。
- `setMessages` 是一个函数，用来更新 `messages` 的值。

这个 `useConversation` hook 可以在 React 组件中被调用和使用，用来管理和更新关于对话和消息的状态信息。

在用户名后添加随机表情

### 03:29:00 - Send Message Functionality

### 03:35:30 - Get Messages

添加skeleton，加载特效

定制化时间显示

切换特效

```jsx
const lastMessageRef = useRef();

	useEffect(() => {
		setTimeout(() => {
			lastMessageRef.current?.scrollIntoView({ behavior: "smooth" });
		}, 100);
	}, [messages]);
```

### 03:54:00 - Search Conversation

细节：

```jsx
const handleSubmit = (e) => {
		e.preventDefault();
		if (!search) return;
		if (search.length < 3) {
			return toast.error("Search term must be at least 3 characters long");
		}

		const conversation = conversations.find((c) => c.fullName.toLowerCase().includes(search.toLowerCase()));

		if (conversation) {
			setSelectedConversation(conversation);
			setSearch("");
		} else toast.error("No such user found!");
	};
```

### 03:58:20 - Implementing Socket.io

第四阶段

backend 添加 socket.js

```js
import { Server } from "socket.io";
import http from "http";
import express from "express";

const app = express();

const server = http.createServer(app);
const io = new Server(server, {
	cors: {
		origin: ["http://localhost:3000"],
		methods: ["GET", "POST"],
	},
});

export const getReceiverSocketId = (receiverId) => {
	return userSocketMap[receiverId];
};

const userSocketMap = {}; // {userId: socketId}

io.on("connection", (socket) => {
	console.log("a user connected", socket.id);

	const userId = socket.handshake.query.userId;
	if (userId != "undefined") userSocketMap[userId] = socket.id;

	// io.emit() is used to send events to all the connected clients
	io.emit("getOnlineUsers", Object.keys(userSocketMap));

	// socket.on() is used to listen to the events. can be used both on client and server side
	socket.on("disconnect", () => {
		console.log("user disconnected", socket.id);
		delete userSocketMap[userId];
		io.emit("getOnlineUsers", Object.keys(userSocketMap));
	});
});

export { app, io, server };
```

修改`server.js`内容

添加`SocketContext.jsx`文件

```jsx
import { createContext, useState, useEffect, useContext } from "react";
import { useAuthContext } from "./AuthContext";
import io from "socket.io-client";

const SocketContext = createContext();

export const useSocketContext = () => {
	return useContext(SocketContext);
};

export const SocketContextProvider = ({ children }) => {
	const [socket, setSocket] = useState(null);
	const [onlineUsers, setOnlineUsers] = useState([]);
	const { authUser } = useAuthContext();

	useEffect(() => {
		if (authUser) {
			const socket = io("https://chat-app-yt.onrender.com", {
				query: {
					userId: authUser._id,
				},
			});

			setSocket(socket);

			// socket.on() is used to listen to the events. can be used both on client and server side
			socket.on("getOnlineUsers", (users) => {
				setOnlineUsers(users);
			});

			return () => socket.close();
		} else {
			if (socket) {
				socket.close();
				setSocket(null);
			}
		}
	}, [authUser]);

	return <SocketContext.Provider value={{ socket, onlineUsers }}>{children}</SocketContext.Provider>;
};
```

在`main.jsx`中添加相应内容：

```jsx
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App.jsx";
import "./index.css";
import { BrowserRouter } from "react-router-dom";
import { AuthContextProvider } from "./context/AuthContext.jsx";
import { SocketContextProvider } from "./context/SocketContext.jsx";

ReactDOM.createRoot(document.getElementById("root")).render(
	<React.StrictMode>
		<BrowserRouter>
			<AuthContextProvider>
				<SocketContextProvider>
					<App />
				</SocketContextProvider>
			</AuthContextProvider>
		</BrowserRouter>
	</React.StrictMode>
);
```

在`frontend`目录下安装`socket.io-client`，对应指令为`npm i socket.io-client`

输出信息如下：

```

added 7 packages in 3s

126 packages are looking for funding
  run `npm fund` for details
```

修改`message.controller.js`文件

```js
// SOCKET IO FUNCTIONALITY WILL GO HERE
		const receiverSocketId = getReceiverSocketId(receiverId);
		if (receiverSocketId) {
			// io.to(<socket_id>).emit() used to send events to specific client
			io.to(receiverSocketId).emit("newMessage", newMessage);
		}
```

新增`useListenMessages.js`文件并添加提示音

```js
import { useEffect } from "react";

import { useSocketContext } from "../context/SocketContext";
import useConversation from "../zustand/useConversation";

import notificationSound from "../assets/sounds/notification.mp3";

const useListenMessages = () => {
	const { socket } = useSocketContext();
	const { messages, setMessages } = useConversation();

	useEffect(() => {
		socket?.on("newMessage", (newMessage) => {
			newMessage.shouldShake = true;
			const sound = new Audio(notificationSound);
			sound.play();
			setMessages([...messages, newMessage]);
		});

		return () => socket?.off("newMessage");
	}, [socket, setMessages, messages]);
};
export default useListenMessages;
```

实现监听

新增 shake 效果 包括在`assets/sounds`文件夹下添加提示音

`index.css`中添加

```css
/* SHAKE ANIMATION ON HORIZONTAL DIRECTION */
.shake {
	animation: shake 0.82s cubic-bezier(0.36, 0.07, 0.19, 0.97) 0.2s both;
	transform: translate3d(0, 0, 0);
	backface-visibility: hidden;
	perspective: 1000px;
}

@keyframes shake {
	10%,
	90% {
		transform: translate3d(-1px, 0, 0);
	}

	20%,
	80% {
		transform: translate3d(2px, 0, 0);
	}

	30%,
	50%,
	70% {
		transform: translate3d(-4px, 0, 0);
	}

	40%,
	60% {
		transform: translate3d(4px, 0, 0);
	}
}
```

### 04:25:22 - Finally Deployment!

添加 path

修改项目下的`package.json`文件，添加`"start": "node backend/server.js"`

`npm install --prefix frontend`相当于`cd frontend`然后执行`npm install`

在项目目录下执行`npm run build`即可

然后执行`npm start`从`localhost:5000`启动

最后把项目部署在render上

[Build, deploy, and scale your apps with unparalleled ease – from your first user to your billionth.](https://render.com/)

Configure and deploy your new Web Service

指令为`npm run build`

`npm run start`

手动添加环境变量

删除node_env ，也不要改为 production

https://chatapp-tianhan.onrender.com/login

用`https://chatapp-tianhan.onrender.com/`替换SocketContext中的`http://localhost:5000`防止cors报错。


# 改进方向

怎么支持多开账户？用无痕模式或新的浏览器

可以增加好友、黑名单、用户界面、群关系。

添加发送文件、图片、表情包、emoji表情功能

用户自定义主页Profile

删除账号和删除消息

嵌入聊天机器人

視頻聊天

可参考`https://mern-chat-web-app-iwwq.onrender.com/`










