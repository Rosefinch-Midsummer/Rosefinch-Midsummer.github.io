---
title: "MERN全栈项目——Netflix-clone简介"
date: 2024-10-01T12:34:25+08:00
lastmod: 2024-10-01T15:54:22+08:00
draft: false
math: true
categories:
- 编程
tags:
- MERN全栈
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

# Netflix-clone


## 简介

[How To Build a Netflix Clone with MERN Stack in 2024 - Full Course](https://www.youtube.com/watch?v=gRroBZczKAU&t=415s)

[burakorkmez/mern-netflix-clone](https://github.com/burakorkmez/mern-netflix-clone)

[相关资源](https://drive.google.com/drive/u/0/folders/18FzSOPrw40T4lzGimv7QazSznCx-H4Ds)

注意：要把资源中`avatar2.jpg`改成`avatar2.png`

[在线试用](https://netflix-tianhan.onrender.com/)

## 特色

About This Course:

- ⚛️ Tech Stack: React.js, Node.js, Express.js, MongoDB, Tailwind
- 🔐 Authentication with JWT
- 📱 Responsive UI
- 🎬 Fetch Movies and Tv Show
- 🔎 Search for Actors and Movies
- 🎥 Watch Trailers 
- 🔥  Fetch Search History
- 🐱‍👤 Get  Similar Movies/Tv Shows
- 💙 Awesome Landing Page
- 🌐 Deployment
- 🚀 And Many More Cool Features


## 本地使用

Setup .env file

```
PORT=5000
MONGO_URI=your_mongo_uri
NODE_ENV=development
JWT_SECRET=your_jwt_secre
TMDB_API_KEY=your_tmdb_api_key
```

Run this app locally

```shell
npm run build
```

Start the app

```shell
npm run start
```

## Timestamps:

### 00:00:00 - App Showcase
### 00:07:50 - Backend Setup

在项目根目录下执行`npm init -y`

然后执行如下语句：

```
npm install express jsonwebtoken mongoose cookie-parser dotenv axios bcryptjs
```

这里没说安装`cors`

相比`bcryptjs`，使用`bcrypt`更好

输出结果如下所示：

```
npm warn deprecated inflight@1.0.6: This module is not supported, and leaks memory. Do not use it. Check out lru-cache if you want a good and tested way to coalesce async requests by a key value, which is much more comprehensive and powerful.
npm warn deprecated npmlog@5.0.1: This package is no longer supported.
npm warn deprecated rimraf@3.0.2: Rimraf versions prior to v4 are no longer supported
npm warn deprecated are-we-there-yet@2.0.0: This package is no longer supported.
npm warn deprecated glob@7.2.3: Glob versions prior to v9 are no longer supported
npm warn deprecated gauge@3.0.2: This package is no longer supported.

added 167 packages in 11s

19 packages are looking for funding
  run `npm fund` for details
```

修改根目录下的package.json文件使得文件内容如下所示：

```json
{
  "name": "netflix",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "dev": "node backend/server.js"
  },
  "keywords": [],
  "type": "module",
  "author": "",
  "license": "ISC",
  "description": "",
  "dependencies": {
    "axios": "^1.7.7",
    "bcrypt": "^5.1.1",
    "cookie-parser": "^1.4.6",
    "dotenv": "^16.4.5",
    "express": "^4.21.0",
    "jsonwebtoken": "^9.0.2",
    "mongoose": "^8.6.3"
  }
}

```

在项目根目录下使用`npm run dev`运行如下server.js文件

```js
import express from "express";

const app = express();

app.get("/", (req, res) => {
    res.send("Server is ready!");
})

app.listen(5000, () => {
    console.log("Server started at http://localhost:5000");
})

```

为了跟踪变化可以使用`"dev": "node --watch backend/server.js"`

但这种方式不常用。使用nodemon更好。在开发模式下安装nodemon执行`npm i nodemon -D`

把`"dev": "node backend/server.js"`改成`"dev": "nodemon backend/server.js"`

代码分层——在backend目录下新增routes文件夹

此时auth.route.js文件内容如下：

```js
import express from "express";

const router = express.Router();

router.get("/signup", (req, res) => {
    res.send("Signup route");
})
router.get("/login", (req, res) => {
    res.send("Login route");
})
router.get("/logout", (req, res) => {
    res.send("Logout route");
})

export default router;
```

server.js文件内容如下所示：

```js
import authRoutes from "./routes/auth.route.js";

const app = express();

app.use("/api/v1/auth", authRoutes);

app.listen(5000, () => {
    console.log("Server started at http://localhost:5000");
})
```

在项目根目录下执行`npm run dev`然后访问`http://localhost:5000/api/v1/auth/logout`

代码分层——在backend目录下新增controllers文件夹

注意：引用.js文件时需要加.js后缀，否则报错，报错信息如下所示：

```
Error [ERR_MODULE_NOT_FOUND]: Cannot find module '/home/xxxxxxxx/netflix/backend/controllers/auth.controller' imported from /home/xxxxxxxx/netflix/backend/routes/auth.route.js
    at finalizeResolution (node:internal/modules/esm/resolve:257:11)
    at moduleResolve (node:internal/modules/esm/resolve:914:10)
    at defaultResolve (node:internal/modules/esm/resolve:1039:11)
    at ModuleLoader.defaultResolve (node:internal/modules/esm/loader:554:12)
    at ModuleLoader.resolve (node:internal/modules/esm/loader:523:25)
    at ModuleLoader.getModuleJob (node:internal/modules/esm/loader:246:38)
    at ModuleJob._link (node:internal/modules/esm/module_job:126:49) {
  code: 'ERR_MODULE_NOT_FOUND',
  url: 'file:///home/xxxxxxx/netflix/backend/controllers/auth.controller'
}
```

此时auth.route.js文件内容如下所示：

```js
import express from "express";
import { login, logout, signup } from "../controllers/auth.controller.js";

const router = express.Router();

router.get("/signup", signup);
router.get("/login", login);
router.get("/logout", logout);

export default router;
```

auth.controller.js

```js
export async function signup(res, req) {
    res.send("Signup route");
}

export async function login(res, req) {
    res.send("Login route");
}

export async function logout(res, req) {
    res.send("Logout route");
}
```


### 00:23:00 - Database (MongoDB) Setup

https://cloud.mongodb.com/

新建项目`netflix-webapp`

Deploy your cluster

Create a database user 保存密码

Use a template below or set up advanced configuration options. You can also edit these configuration options once the cluster is created.

Connecting with MongoDB Driver

`MONGO_DB_URI`需要在?前面添加数据库名称，具体情况如下所示：

```
mongodb+srv://<username>:<password>@cluster0.tqcon.mongodb.net/<database-name>?retryWrites=true&w=majority&appName=Cluster0
```

Add a connection IP address

在Network Access中新增`0.0.0.0`（即任意IP均可访问）

将`MONGO_DB_URI`加入`.env`文件，在`server.js`中通过`dotenv`引用。

新增`config`目录，在该目录下新增`envVars.js`（定义别名）和`db.js`

把`dotenv`相关内容放到`envVars.js`中，`envVars.js`最终内容如下所示：

```js
import dotenv from "dotenv";

dotenv.config();

export const ENV_VARS = {
	MONGO_DB_URI: process.env.MONGO_DB_URI,
	PORT: process.env.PORT || 5000,
	JWT_SECRET: process.env.JWT_SECRET,
	NODE_ENV: process.env.NODE_ENV,
	TMDB_API_KEY: process.env.TMDB_API_KEY,
};
```

此时在`server.js`中使用`const PORT = ENV_VARS.PORT;`引入`PORT`

`server.js`内容如下所示：

```js
import express from "express";

import authRoutes from "./routes/auth.route.js";
import { ENV_VARS } from "./config/envVars.js";


const app = express();

const PORT = ENV_VARS.PORT;

app.use("/api/v1/auth", authRoutes);

app.listen(PORT, () => {
    console.log("Server started at http://localhost:" + PORT);
})
```

`db.js`内容如下所示：

```js
import mongoose from "mongoose";
import { ENV_VARS } from "./envVars.js";

export const connectDB = async () => {
	try {
		const conn = await mongoose.connect(ENV_VARS.MONGO_DB_URI);
		console.log("MongoDB connected: " + conn.connection.host);
	} catch (error) {
		console.error("Error connecting to MONGODB: " + error.message);
		process.exit(1); // 1 means there was an error, 0 means success
	}
};
```

新增`models/user.model.js`文件，文件内容如下所示：

```js
import mongoose from "mongoose";

const userSchema = mongoose.Schema({
	username: {
		type: String,
		required: true,
		unique: true,
	},
	email: {
		type: String,
		required: true,
		unique: true,
	},
	password: {
		type: String,
		required: true,
	},
	image: {
		type: String,
		default: "",
	},
	searchHistory: {
		type: Array,
		default: [],
	},
});

export const User = mongoose.model("User", userSchema);
```

### 00:35:54 - Signup Logic in Backend

修改`auth.controller.js`文件

在`server.js`中新增`app.use(express.json()); // will allow us to parse req.body`

此时`auth.controller.js`内容如下所示：

```js
import { User } from "../models/user.model.js";
import bcrypt from "bcrypt";
export async function signup(req, res) {
	try {
		const { email, password, username } = req.body;

		if (!email || !password || !username) {
			return res.status(400).json({ success: false, message: "All fields are required" });
		}

		const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;

		if (!emailRegex.test(email)) {
			return res.status(400).json({ success: false, message: "Invalid email" });
		}

		if (password.length < 6) {
			return res.status(400).json({ success: false, message: "Password must be at least 6 characters" });
		}

		const existingUserByEmail = await User.findOne({ email: email });

		if (existingUserByEmail) {
			return res.status(400).json({ success: false, message: "Email already exists" });
		}

		const existingUserByUsername = await User.findOne({ username: username });

		if (existingUserByUsername) {
			return res.status(400).json({ success: false, message: "Username already exists" });
		}

		const salt = await bcrypt.genSalt(10);
		const hashedPassword = await bcrypt.hash(password, salt);

		const PROFILE_PICS = ["/avatar1.png", "/avatar2.png", "/avatar3.png"];

		const image = PROFILE_PICS[Math.floor(Math.random() * PROFILE_PICS.length)];

		const newUser = new User({
			email,
			password: hashedPassword,
			username,
			image,
		});
		await newUser.save();
	} catch (error) {
		console.log("Error in signup controller", error.message);
		res.status(500).json({ success: false, message: "Internal server error" });
	}
}

export async function login(res, req) {
    res.send("Login route");
}

export async function logout(res, req) {
    res.send("Logout route");
}

```

此时使用`PostMan`测试，，测试只能失败，不能成功（显示`Sending request...`，因为`save`之后没有任何有效输出信息）。但MongoDB中数据库和表都已被创建。

`PostMan`成功执行时输出信息如下所示：

```json
{
    "success": true,
    "user": {
        "username": "bob",
        "email": "bob@gmail.com",
        "password": "",
        "image": "/avatar2.png",
        "searchHistory": [],
        "_id": "66f6ba60ffa30445a6a529c2",
        "__v": 0
    }
}
```

此时才加入对密码加密的代码。

### 00:54:26 - Generate JWT

在`.env`中新增`JWT_SECRET`和`NODE_ENV`。

`JWT_SECRET`这个可以随意，下面的`openssl`生成的：

```
39cd7527a217f289590110725fa0885fd067cc835eb97bebdbeaa3373658d68ab9164ebf20285bdbc83e0a354e9a2932a0b46c00d02ed5d2a4dd3bed30c320df
```

新增`utils/generateToken.js`文件，文件内容如下所示：

```js
import jwt from "jsonwebtoken";
import { ENV_VARS } from "../config/envVars.js";

export const generateTokenAndSetCookie = (userId, res) => {
	const token = jwt.sign({ userId }, ENV_VARS.JWT_SECRET, { expiresIn: "15d" });

	res.cookie("jwt-netflix", token, {
		maxAge: 15 * 24 * 60 * 60 * 1000, // 15 days in MS
		httpOnly: true, // prevent XSS attacks cross-site scripting attacks, make it not be accessed by JS
		sameSite: "strict", // CSRF attacks cross-site request forgery attacks
		secure: ENV_VARS.NODE_ENV !== "development",
	});

	return token;
};
```

在`auth.controller.js`中引入`generateTokenAndSetCookie(newUser._id, res);`

### 01:02:40 - Logout Logic in Backend


### 01:04:30 - Login Logic in Backend


### 01:08:30 - A Quick Recap


### 01:11:25 - Fetching Movies From API

[TMDB官网](https://www.themoviedb.org/)

注册账号然后获得相应的API

新建`services/tmdb.service.js`文件

```js
import axios from "axios";
import { ENV_VARS } from "../config/envVars.js";

export const fetchFromTMDB = async (url) => {
	const options = {
		headers: {
			accept: "application/json",
			Authorization: "Bearer " + ENV_VARS.TMDB_API_KEY,
		},
	};

	const response = await axios.get(url, options);

	if (response.status !== 200) {
		throw new Error("Failed to fetch data from TMDB" + response.statusText);
	}

	return response.data;
};
```

使用VSCode插件`VSCode Great Icons`能使文件图标多样化显示。

新增`movie.route.js`文件和`movie.controller.js`


下面的代码有问题，具体是`const response = await axios.get(url, options);`，你要帮我找出解决办法。

```js
import axios from "axios";
import { ENV_VARS } from "../config/envVars.js";

export const fetchFromTMDB = async (url) => {
	console.log("here1")
	const options = {
		headers: {
			accept: "application/json",
			Authorization: "Bearer " + ENV_VARS.TMDB_API_KEY,
		},
	};

	console.log("here2")

	const response = await axios.get(url, options);

	console.log("here3")

	if (response.status !== 200) {
		throw new Error("Failed to fetch data from TMDB" + response.statusText);
	}

	return response.data;
};
```

其他相关代码

```js
import express from "express";
import {
	getMovieDetails,
	getMoviesByCategory,
	getMovieTrailers,
	getSimilarMovies,
	getTrendingMovie,
} from "../controllers/movie.controller.js";

const router = express.Router();

router.get("/trending", getTrendingMovie);
router.get("/:id/trailers", getMovieTrailers);
router.get("/:id/details", getMovieDetails);
router.get("/:id/similar", getSimilarMovies);
router.get("/:category", getMoviesByCategory);

export default router;
```

```js
import { fetchFromTMDB } from "../services/tmdb.service.js";

export async function getTrendingMovie(req, res) {
    try {
        const data = await fetchFromTMDB("https://api.themoviedb.org/3/trending/movie/day?language=en-US");
        const randomMovie = data.results[Math.floor(Math.random() * data.results?.length)];
        res.json({ success: true, content: randomMovie });
    } catch (error) {
        res.status(500).json({ success: false, message: "Internal Server Error" });
    }
}
```

解决办法：在Windows10系统上运行，不要在WSL2——Ubuntu系统上运行。

另外需要把`bcrypt`改成`bcryptjs`（和原作者的代码保持一致）

电影预告片（movie-trailer）是电影的简短视频宣传片，通常包含片段的一小部分，以引起观众的兴趣和好奇心，让他们想要看更多。而电影详情（movie-detail）则是关于电影的详细信息，包括演员阵容、剧情梗概、上映日期、制片人等信息。电影预告片主要是用来概括电影内容和吸引观众，而电影详情则是提供更全面、深入的信息。

注意：如何在路由中表示参数

```js
router.get("/trending", getTrendingMovie);
router.get("/:id/trailers", getMovieTrailers);
router.get("/:id/details", getMovieDetails);
router.get("/:id/similar", getSimilarMovies);
router.get("/:category", getMoviesByCategory);
```

在路由中，使用冒号（:）表示参数化路径段，即路径中的某一部分是动态变化的，并且会被传递到处理程序中。在上述代码示例中，使用了冒号的路径是带有参数的，可能是根据电影的ID或类别来获取电影相关信息，而不带冒号的路径是固定的路径，用于获取趋势电影、电影预告片等静态信息。冒号表示这部分路径为参数，区别于静态路径。

### 01:42:00 - Fetching TV Shows From API

在`server.js`中新增`app.use("/api/v1/tv", tvRoutes);`及相关代码。

这块和`movie`非常相似，只需要修改函数名。

### 01:48:50 - Protecting Routes (Middleware)

新增`middleware/protectRoute.js`，内容如下所示：

```js
import jwt from "jsonwebtoken";
import { User } from "../models/user.model.js";
import { ENV_VARS } from "../config/envVars.js";

export const protectRoute = async (req, res, next) => {
	try {
		const token = req.cookies["jwt-netflix"];

		if (!token) {
			return res.status(401).json({ success: false, message: "Unauthorized - No Token Provided" });
		}

		const decoded = jwt.verify(token, ENV_VARS.JWT_SECRET);

		if (!decoded) {
			return res.status(401).json({ success: false, message: "Unauthorized - Invalid Token" });
		}

		const user = await User.findById(decoded.userId).select("-password");

		if (!user) {
			return res.status(404).json({ success: false, message: "User not found" });
		}

		req.user = user;

		next();
	} catch (error) {
		console.log("Error in protectRoute middleware: ", error.message);
		res.status(500).json({ success: false, message: "Internal Server Error" });
	}
};
```

这段代码是一个中间件函数，用于保护路由，即在请求到达某个特定路由之前对请求进行验证和授权处理。具体解释如下：

1. 首先导入jsonwebtoken模块、User模型和环境变量配置。
2. 定义了一个名为`protectRoute`的异步函数，接受req、res和next三个参数。
3. 在函数体内部进行了以下操作：
   - 从请求的cookie中获取名为"jwt-netflix"的token。
   - 如果token不存在，则返回401状态码和错误消息"Unauthorized - No Token Provided"。
   - 使用jwt库中的`verify`方法验证token的有效性，并解码token获得用户id。
   - 如果解码失败，则返回401状态码和错误消息"Unauthorized - Invalid Token"。
   - 根据解码后的用户id，在数据库中查找对应的用户信息，去除密码字段。
   - 如果找不到对应用户，则返回404状态码和错误消息"User not found"。
   - 将查询到的用户信息保存在req对象的user属性中，便于后续路由处理中使用。
   - 调用`next`函数，将控制权交给下一个中间件或路由处理函数。
4. 如果在处理过程中捕获到异常，则记录错误信息并返回500状态码和错误消息"Internal Server Error"。

这里的`next`函数的作用是将控制权交给下一个中间件或路由处理函数，可以用来串联多个中间件以实现请求处理流程的划分和处理。在本例中，当对请求进行验证和授权处理完成之后，通过调用`next()`函数将请求继续传递给下一个中间件或路由处理函数。

在`server.js`中新增`app.use("/api/v1/tv", protectRoute, tvRoutes);`及相关代码。

在`server.js`中引入`cookie-parser`，此外`protectRoute.js`和`generateToken.js`中`cookie`名称要统一，这里都叫`jwt-netflix`

### 01:59:15 - Search Routes

注意搜索记录的使用


### 02:28:52 - Frontend Setup

进入`frontend`目录，执行`npm create vite@latest .`

选择`React`和`JavaScript`

之后执行`npm install`和`npm run dev`

执行`npm i axios lucide-react react-player react-hot-toast react-router-dom zustan`安装所需组件

安装`VSCode`插件`ESLint`            

`ESLint`         Integrates ESLint JavaScript into VS Code.

删除`App.css`文件

[Install Tailwind CSS with Vite](https://tailwindcss.com/docs/guides/vite)

Install Tailwind CSS
    
Install `tailwindcss` and its peer dependencies, then generate your `tailwind.config.js` and `postcss.config.js` files.

```
npm install -D tailwindcss postcss autoprefixernpx tailwindcss init -p
```

Configure your template paths

Add the paths to all of your template files in your `tailwind.config.js` file.

tailwind.config.js

```js
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

Add the Tailwind directives to your CSS

Add the `@tailwind` directives for each of Tailwind’s layers to your `./src/index.css` file.

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

Start your build process

Run your build process with `npm run dev`.

推荐安装`VSCode`插件`Tailwind CSS IntelliSense`

此时`main.js`文件内容如下所示：

```js
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App.jsx";
import "./index.css";
import { BrowserRouter } from "react-router-dom";

ReactDOM.createRoot(document.getElementById("root")).render(
	<React.StrictMode>
		<BrowserRouter>
			<App />
		</BrowserRouter>
	</React.StrictMode>
);
```

推荐安装`VSCode`插件`VS Code ES7 React/Redux/React-Native/JS snippets`

修改`App.jsx`文件内容，增加`HomePage.jsx`、`Login.jsx`和`SignUp.jsx`

此时`App.jsx`文件内容如下所示：

```jsx
import { Route, Routes } from "react-router-dom";
import HomePage from "./pages/HomePage";
import LoginPage from "./pages/LoginPage";
import SignUpPage from "./pages/SignUpPage";

function App() {

  return (
		<>
			<Routes>
				<Route path='/' element={<HomePage />} />
				<Route path='/login' element={<LoginPage />} />
				<Route path='/signup' element={<SignUpPage />} />
			</Routes>
		</>
	);
}

export default App

```

执行`npm run dev`

输出结果如下所示：

```
> frontend@0.0.0 dev
> vite


  VITE v5.4.8  ready in 516 ms

  ➜  Local:   http://localhost:5173/
  ➜  Network: use --host to expose
  ➜  press h + enter to show help
```

下载相关图片，并调整`index.html`文件内容

在`index.css`中把图片做成属性，例如：

```css
.hero-bg {
	background-image: linear-gradient(rgba(0, 0, 0, 0.8), rgba(0, 0, 0, 0.1)), url("/hero.png");
}
```

### 02:41:45 - Signup Page and Login Page UI Design

### 02:55:25 - Auth Screen UI Design

新建`home`目录，然后把`HomePage.jsx`移动到`home`目录

在`home`目录下新增`AuthScreen.jsx`和`HomeScreen.jsx`

新增`components/Footer.jsx`文件，文件内容如下所示：

```jsx
const Footer = () => {
	return (
		<footer className='py-6 md:px-8 md:py-0 bg-black text-white border-t border-gray-800'>
			<div className='flex flex-col items-center justify-between gap-4 md:h-24 md:flex-row'>
				<p className='text-balance text-center text-sm leading-loose text-muted-foreground md:text-left'>
					Built by{" "}
					<a
						href='https://github.com/burakorkmez'
						target='_blank'
						className='font-medium underline underline-offset-4'
					>
						you
					</a>
					. The source code is available on{" "}
					<a
						href='https://github.com/burakorkmez'
						target='_blank'
						rel='noreferrer'
						className='font-medium underline underline-offset-4'
					>
						GitHub
					</a>
					.
				</p>
			</div>
		</footer>
	);
};
export default Footer;
```
### 03:28:30 - Signup, Login, Logout Functionality


在后端代码中加入`authCheck`相关内容：在`auth.route.js`中加入`router.get("/authCheck", protectRoute, authCheck);`，在`auth.controller.js`中加入如下代码：

```js
export async function authCheck(req, res) {
	try {
		console.log("req.user:", req.user);
		res.status(200).json({ success: true, user: req.user });
	} catch (error) {
		console.log("Error in authCheck controller", error.message);
		res.status(500).json({ success: false, message: "Internal server error" });
	}
}
```

使用`Zustand`组件管理应用程序中的状态

Zustand是一个用于React应用程序状态管理的库。它提供了一个简单易用的方式来管理应用程序中的状态，并使数据共享和状态更新变得更加容易。通过使用Zustand，开发人员可以轻松地创建可维护和可扩展的React应用程序。该库具有快速、响应式和透明的状态管理优势，可以帮助开发人员更有效地处理数据状态。

新增`store`目录，新增`authUser.js`文件，相关文件内容为

```js
import axios from "axios";
import toast from "react-hot-toast";
import { create } from "zustand";

export const useAuthStore = create((set) => ({
	user: null,
	isSigningUp: false,
	isCheckingAuth: true,
	isLoggingOut: false,
	isLoggingIn: false,
	signup: async (credentials) => {
		set({ isSigningUp: true });
		try {
			const response = await axios.post("/api/v1/auth/signup", credentials);
			set({ user: response.data.user, isSigningUp: false });
			toast.success("Account created successfully");
		} catch (error) {
			toast.error(error.response.data.message || "Signup failed");
			set({ isSigningUp: false, user: null });
		}
	},
	login: async (credentials) => {
		set({ isLoggingIn: true });
		try {
			const response = await axios.post("/api/v1/auth/login", credentials);
			set({ user: response.data.user, isLoggingIn: false });
		} catch (error) {
			set({ isLoggingIn: false, user: null });
			toast.error(error.response.data.message || "Login failed");
		}
	},
	logout: async () => {
		set({ isLoggingOut: true });
		try {
			await axios.post("/api/v1/auth/logout");
			set({ user: null, isLoggingOut: false });
			toast.success("Logged out successfully");
		} catch (error) {
			set({ isLoggingOut: false });
			toast.error(error.response.data.message || "Logout failed");
		}
	},
	authCheck: async () => {
		set({ isCheckingAuth: true });
		try {
			const response = await axios.get("/api/v1/auth/authCheck");

			set({ user: response.data.user, isCheckingAuth: false });
		} catch (error) {
			set({ isCheckingAuth: false, user: null });
			// toast.error(error.response.data.message || "An error occurred");
		}
	},
}));
```

以上代码是一个使用Zustand库创建的用于管理认证相关状态的自定义hook。该hook提供了一些属性和方法用于处理用户认证的不同操作，比如注册、登录、登出和检查认证状态。

具体来说，这个自定义hook中包含了以下属性和方法：

- user：用于存储当前登录用户的信息，初始值为null。
- isSigningUp、isCheckingAuth、isLoggingOut、isLoggingIn：用于表示注册、检查认证、登出、登录过程中的加载状态。
- signup(credentials)：异步方法，用于处理用户注册操作。在方法内部，会发送一个POST请求到"/api/v1/auth/signup"接口，如果请求成功则更新user状态并显示成功提示，如果失败则显示错误提示。
- login(credentials)：异步方法，用于处理用户登录操作。发送一个POST请求到"/api/v1/auth/login"接口，根据请求结果更新用户状态并显示相关提示。
- logout()：异步方法，用于处理用户登出操作。发送一个POST请求到"/api/v1/auth/logout"接口，根据请求结果更新用户状态并显示相关提示。
- authCheck()：异步方法，用于检查用户的认证状态。发送一个GET请求到"/api/v1/auth/authCheck"接口，根据请求结果更新用户状态。

通过使用Zustand提供的create方法，开发人员可以方便地管理和更新组件中的状态，并确保状态的一致性和可维护性。这样可以帮助开发人员更轻松地处理用户认证流程，同时保持代码的整洁和易读性。

修改`vite.config.js`文件，此时内容如下所示：

```js
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";

// https://vitejs.dev/config/
export default defineConfig({
	plugins: [react()],
	server: {
		proxy: {
			"/api": {
				target: "http://localhost:5000",
			},
		},
	},
});
```

修改`App.jsx`，增加`footer`和`toast`，并添加下面的代码以提供转场动画：

```jsx
if (isCheckingAuth) {
		return (
			<div className='h-screen'>
				<div className='flex justify-center items-center bg-black h-full'>
					<Loader className='animate-spin text-red-600 size-10' />
				</div>
			</div>
		);
	}
```

修改`HomePage.jsx`使得其内容如下所示：

```jsx
import { useAuthStore } from "../../store/authUser";
import AuthScreen from "./AuthScreen";
import HomeScreen from "./HomeScreen";

const HomePage = () => {
	const { user } = useAuthStore();

	return <>{user ? <HomeScreen /> : <AuthScreen />}</>;
};
export default HomePage;
```
### 04:03:45 - Building the Home Screen 

新增`components/Navbar.jsx`，文件内容如下所示：

```jsx
import { useState } from "react";
import { Link } from "react-router-dom";
import { LogOut, Menu, Search } from "lucide-react";
import { useAuthStore } from "../store/authUser";
// import { useContentStore } from "../store/content";

const Navbar = () => {
	const [isMobileMenuOpen, setIsMobileMenuOpen] = useState(false);
	const { user, logout } = useAuthStore();

	const toggleMobileMenu = () => setIsMobileMenuOpen(!isMobileMenuOpen);

	// const { setContentType } = useContentStore();

	return (
		<header className='max-w-6xl mx-auto flex flex-wrap items-center justify-between p-4 h-20'>
			<div className='flex items-center gap-10 z-50'>
				<Link to='/'>
					<img src='/netflix-logo.png' alt='Netflix Logo' className='w-32 sm:w-40' />
				</Link>

				{/* desktop navbar items */}
				<div className='hidden sm:flex gap-2 items-center'>
					{/* <Link to='/' className='hover:underline' onClick={() => setContentType("movie")}> */}
					<Link to='/' className='hover:underline'>
						Movies
					</Link>
					<Link to='/' className='hover:underline'>
					{/* <Link to='/' className='hover:underline' onClick={() => setContentType("tv")}> */}
						Tv Shows
					</Link>
					<Link to='/history' className='hover:underline'>
						Search History
					</Link>
				</div>
			</div>

			<div className='flex gap-2 items-center z-50'>
				<Link to={"/search"}>
					<Search className='size-6 cursor-pointer' />
				</Link>
				<img src={user.image} alt='Avatar' className='h-8 rounded cursor-pointer' />
				<LogOut className='size-6 cursor-pointer' onClick={logout} />
				<div className='sm:hidden'>
					<Menu className='size-6 cursor-pointer' onClick={toggleMobileMenu} />
				</div>
			</div>

			{/* mobile navbar items */}
			{isMobileMenuOpen && (
				<div className='w-full sm:hidden mt-4 z-50 bg-black border rounded border-gray-800'>
					<Link to={"/"} className='block hover:underline p-2' onClick={toggleMobileMenu}>
						Movies
					</Link>
					<Link to={"/"} className='block hover:underline p-2' onClick={toggleMobileMenu}>
						Tv Shows
					</Link>
					<Link to={"/history"} className='block hover:underline p-2' onClick={toggleMobileMenu}>
						Search History
					</Link>
				</div>
			)}
		</header>
	);
};
export default Navbar;
```

带有渐变效果的`HomeScreen.jsx`内容如下：

```jsx
import Navbar from "../../components/Navbar";

const HomeScreen = () => {

	return (
		<div className='h-screen text-white relative'>
			<Navbar />
			<img
				src="/extraction.jpg"
				alt="Hero img"
				className='absolute top-0 left-0 w-full h-full object-cover -z-50'
			/>
			<div className='absolute top-0 left-0 w-full h-full bg-black/50 -z-50' aria-hidden='true' />

			<div className='absolute top-0 left-0 w-full h-full flex flex-col justify-center px-8 md:px-16 lg:px-32'>
				<div
					className='bg-gradient-to-b from-black via-transparent to-transparent 
 				absolute w-full h-full top-0 left-0 -z-10'
				/>
			</div>
			<div className='flex mt-8'>
				<Link
					// to={`/watch/${trendingContent?.id}`}
					className='bg-white hover:bg-white/80 text-black font-bold py-2 px-4 rounded mr-4 flex
							 items-center'
				>
					<Play className='size-6 mr-2 fill-black' />
					Play
				</Link>

				<Link
					// to={`/watch/${trendingContent?.id}`}
					className='bg-gray-500/70 hover:bg-gray-500 text-white py-2 px-4 rounded flex items-center'
				>
					<Info className='size-6 mr-2' />
					More Info
				</Link>
			</div>
		</div>
	);
};

export default HomeScreen;
```

下面代码基于TailwindCSS，你要详细解释下下面代码的作用。此外告诉我这里的文本信息为何不能复制粘贴？

```jsx
<div className='max-w-2xl'>
	<h1 className='mt-4 text-6xl font-extrabold text-balance'>
		Extraction
	</h1>
	<p className='mt-2 text-lg'>
		2014|18+
	</p>

	<p className='mt-4 text-lg'>
		A thrilling adventure about a young man who is suddenly transported to another world.
	</p>
</div>
```

这段代码使用TailwindCSS的类来设计页面样式。具体解释如下：
1. `<div className='max-w-2xl'>`：设置包裹元素的最大宽度为2xl，即最大宽度为2列。
2. `<h1 className='mt-4 text-6xl font-extrabold text-balance'> Extraction </h1>`：设置标题样式，包括顶部外边距为4（mt-4）、文字大小为6xl（text-6xl）、字体加粗为extrabold（font-extrabold）、文字颜色为balance（text-balance）。标题内容为“Extraction”。
3. `<p className='mt-2 text-lg'> 2014|18+ </p>`：设置段落样式，包括顶部外边距为2（mt-2）、文字大小为lg（text-lg）。段落内容为“2014|18+”。
4. `<p className='mt-4 text-lg'> A thrilling adventure about a young man who is suddenly transported to another world. </p>`：设置另一个段落的样式，包括顶部外边距为4（mt-4）、文字大小为lg（text-lg）。段落内容为“A thrilling adventure about a young man who is suddenly transported to another world”。

关于文本信息无法复制粘贴的问题，可能是因为代码中的文本信息是作为图片或者基于图形渲染的方式呈现的，而非实际的文本内容。这种情况下，文本信息无法以普通的复制粘贴方式获取。您可以尝试查看页面源代码或者开发者工具来获取文本信息的实际内容。

新增`store/content.js`文件，文件内容如下所示：

```js
import { create } from "zustand";

export const useContentStore = create((set) => ({
	contentType: "movie",
	setContentType: (type) => set({ contentType: type }),
}));
```

修改`Navbar.jsx`

新增`hooks/useGetTrendingContent.jsx`，文件内容如下所示：

```jsx
import { useEffect, useState } from "react";
import { useContentStore } from "../store/content";
import axios from "axios";

const useGetTrendingContent = () => {
	const [trendingContent, setTrendingContent] = useState(null);
	const { contentType } = useContentStore();

	useEffect(() => {
		const getTrendingContent = async () => {
			const res = await axios.get(`/api/v1/${contentType}/trending`);
			setTrendingContent(res.data.content);
		};

		getTrendingContent();
	}, [contentType]);

	return { trendingContent };
};
export default useGetTrendingContent;
```

新增`utils/constants.js`，文件内容如下所示：

```js
export const SMALL_IMG_BASE_URL = "https://image.tmdb.org/t/p/w500";
export const ORIGINAL_IMG_BASE_URL = "https://image.tmdb.org/t/p/original";

export const MOVIE_CATEGORIES = ["now_playing", "top_rated", "popular", "upcoming"];
export const TV_CATEGORIES = ["airing_today", "on_the_air", "popular", "top_rated"];
```

作用：设定图片等的`BASE_URL`

[相关链接🔗](https://developer.themoviedb.org/docs/image-basics)

推荐`VSCode`插件`Better Comments`

`loading spinner`是指在网页或移动应用程序中用于展示页面正在加载或处理中的动画图标。通常是一个旋转的圆圈或其他图形，用来提醒用户当前页面正在进行某种操作，以避免用户误解为页面无响应或卡顿。这样的设计可以提升用户体验，增加用户等待过程中的耐心。

在`HomeScreen.jsx`中实现`loading spinner`，具体代码如下所示：

```jsx
if (!trendingContent)
		return (
			<div className='h-screen text-white relative'>
				<Navbar />
				<div className='absolute top-0 left-0 w-full h-full bg-black/70 flex items-center justify-center -z-10 shimmer' />
			</div>
		);
```

`shimmer`需要在`index.css`中定义，相关代码如下所示：

```css
.shimmer {
	animation: shimmer 2s infinite linear;
	background: linear-gradient(to right, #2c2c2c 4%, #333 25%, #2c2c2c 36%);
	background-size: 1000px 100%;
}

@keyframes shimmer {
	0% {
		background-position: -1000px 0;
	}
	100% {
		background-position: 1000px 0;
	}
}
```

新增`components/MovieSlider.jsx`，文件内容如下所示：

```jsx
import { useEffect, useRef, useState } from "react";
import { useContentStore } from "../store/content";
import axios from "axios";
import { Link } from "react-router-dom";
import { SMALL_IMG_BASE_URL } from "../utils/constants";
import { ChevronLeft, ChevronRight } from "lucide-react";

const MovieSlider = ({ category }) => {
	const { contentType } = useContentStore();
	const [content, setContent] = useState([]);
	const [showArrows, setShowArrows] = useState(false);

	const sliderRef = useRef(null);

	const formattedCategoryName =
		category.replaceAll("_", " ")[0].toUpperCase() + category.replaceAll("_", " ").slice(1);
	const formattedContentType = contentType === "movie" ? "Movies" : "TV Shows";

	useEffect(() => {
		const getContent = async () => {
			const res = await axios.get(`/api/v1/${contentType}/${category}`);
			setContent(res.data.content);
		};

		getContent();
	}, [contentType, category]);

	const scrollLeft = () => {
		if (sliderRef.current) {
			sliderRef.current.scrollBy({ left: -sliderRef.current.offsetWidth, behavior: "smooth" });
		}
	};
	const scrollRight = () => {
		sliderRef.current.scrollBy({ left: sliderRef.current.offsetWidth, behavior: "smooth" });
	};

	return (
		<div
			className='bg-black text-white relative px-5 md:px-20'
			onMouseEnter={() => setShowArrows(true)}
			onMouseLeave={() => setShowArrows(false)}
		>
			<h2 className='mb-4 text-2xl font-bold'>
				{formattedCategoryName} {formattedContentType}
			</h2>

			<div className='flex space-x-4 overflow-x-scroll scrollbar-hide' ref={sliderRef}>
				{content.map((item) => (
					<Link to={`/watch/${item.id}`} className='min-w-[250px] relative group' key={item.id}>
						<div className='rounded-lg overflow-hidden'>
							<img
								src={SMALL_IMG_BASE_URL + item.backdrop_path}
								alt='Movie image'
								className='transition-transform duration-300 ease-in-out group-hover:scale-125'
							/>
						</div>
						<p className='mt-2 text-center'>{item.title || item.name}</p>
					</Link>
				))}
			</div>

			{showArrows && (
				<>
					<button
						className='absolute top-1/2 -translate-y-1/2 left-5 md:left-24 flex items-center justify-center
            size-12 rounded-full bg-black bg-opacity-50 hover:bg-opacity-75 text-white z-10
            '
						onClick={scrollLeft}
					>
						<ChevronLeft size={24} />
					</button>

					<button
						className='absolute top-1/2 -translate-y-1/2 right-5 md:right-24 flex items-center justify-center
            size-12 rounded-full bg-black bg-opacity-50 hover:bg-opacity-75 text-white z-10
            '
						onClick={scrollRight}
					>
						<ChevronRight size={24} />
					</button>
				</>
			)}
		</div>
	);
};
export default MovieSlider;
```

上面代码通过`category`映射成多样`MovieSlider`

注意这里有红色警告：`'category' is missing in props validationeslint[react/prop-types]`

原作者解决办法：修改`.eslintrc.cjs`，增添`"react/prop-types": "off",`，此时`.eslintrc.cjs`内容如下所示：

```js
module.exports = {
	root: true,
	env: { browser: true, es2020: true },
	extends: [
		"eslint:recommended",
		"plugin:react/recommended",
		"plugin:react/jsx-runtime",
		"plugin:react-hooks/recommended",
	],
	ignorePatterns: ["dist", ".eslintrc.cjs"],
	parserOptions: { ecmaVersion: "latest", sourceType: "module" },
	settings: { react: { version: "18.2" } },
	plugins: ["react-refresh"],
	rules: {
		"react/jsx-no-target-blank": "off",
		"react-refresh/only-export-components": ["warn", { allowConstantExport: true }],
		"react/no-unescaped-entities": "off",
		"react/prop-types": "off",
	},
};
```

按照上面的代码，我修改了本项目相关文件`eslint.config.js`，现在该内容如下所示：

```js
import js from '@eslint/js'
import globals from 'globals'
import react from 'eslint-plugin-react'
import reactHooks from 'eslint-plugin-react-hooks'
import reactRefresh from 'eslint-plugin-react-refresh'

export default [
  { ignores: ['dist'] },
  {
    files: ['**/*.{js,jsx}'],
    languageOptions: {
      ecmaVersion: 2020,
      globals: globals.browser,
      parserOptions: {
        ecmaVersion: 'latest',
        ecmaFeatures: { jsx: true },
        sourceType: 'module',
      },
    },
    settings: { react: { version: '18.3' } },
    plugins: {
      react,
      'react-hooks': reactHooks,
      'react-refresh': reactRefresh,
    },
    rules: {
      ...js.configs.recommended.rules,
      ...react.configs.recommended.rules,
      ...react.configs['jsx-runtime'].rules,
      ...reactHooks.configs.recommended.rules,
      'react/jsx-no-target-blank': 'off',
      'react/prop-types': 'off',
      'react-refresh/only-export-components': [
        'warn',
        { allowConstantExport: true },
      ],
    },
  },
]

```

在`frontend`目录下执行指令`npm i tailwind-scrollbar-hide`安装`tailwind-scrollbar-hide`

修改`tailwind.config.js`文件，此时`tailwind.config.js`文件内容如下所示：

```js
import tailwindScrollbarHide from "tailwind-scrollbar-hide";
/** @type {import('tailwindcss').Config} */
export default {
	content: ["./index.html", "./src/**/*.{js,ts,jsx,tsx}"],
	theme: {
		extend: {},
	},
	plugins: [tailwindScrollbarHide],
};
```

此时启用`scrollbar-hide`，`Slider`中只剩下左右按键移动方式

### 05:13:00 - Building the Watch Page

新增`WatchPage.jsx`并修改`App.jsx`文件

注意这里`import WatchPageSkeleton from "../components/skeletons/WatchPageSkeleton";`暂时报错

播放需要使用`react-player`

新增`utils/dateFunction.js`，文件内容如下所示：

```js
export function formatReleaseDate(date) {
	return new Date(date).toLocaleDateString("en-US", {
		year: "numeric",
		month: "long",
		day: "numeric",
	});
}
```

新增`components/skeletons/WatchPageSkeleton.jsx`，文件内容如下所示：

```jsx
const WatchPageSkeleton = () => {
	return (
		<div className='animate-pulse'>
			<div className='bg-gray-700 rounded-md w-40 h-6 mb-4 shimmer'></div>
			<div className='bg-gray-700 rounded-md w-full h-96 mb-4 shimmer'></div>
			<div className='bg-gray-700 rounded-md w-3/4 h-6 mb-2 shimmer'></div>
			<div className='bg-gray-700 rounded-md w-1/2 h-6 mb-4 shimmer'></div>
			<div className='bg-gray-700 rounded-md w-full h-24 shimmer'></div>
		</div>
	);
};
export default WatchPageSkeleton;
```

作用：增加转场动画效果

最后新增`WatchPage.jsx`文件内容如下所示：

```jsx
import { useEffect, useRef, useState } from "react";
import { Link, useParams } from "react-router-dom";
import { useContentStore } from "../store/content";
import axios from "axios";
import Navbar from "../components/Navbar";
import { ChevronLeft, ChevronRight } from "lucide-react";
import ReactPlayer from "react-player";
import { ORIGINAL_IMG_BASE_URL, SMALL_IMG_BASE_URL } from "../utils/constants";
import { formatReleaseDate } from "../utils/dateFunction";
import WatchPageSkeleton from "../components/skeletons/WatchPageSkeleton";

const WatchPage = () => {
	const { id } = useParams();
	const [trailers, setTrailers] = useState([]);
	const [currentTrailerIdx, setCurrentTrailerIdx] = useState(0);
	const [loading, setLoading] = useState(true);
	const [content, setContent] = useState({});
	const [similarContent, setSimilarContent] = useState([]);
	const { contentType } = useContentStore();

	const sliderRef = useRef(null);

	useEffect(() => {
		const getTrailers = async () => {
			try {
				const res = await axios.get(`/api/v1/${contentType}/${id}/trailers`);
				setTrailers(res.data.trailers);
			} catch (error) {
				if (error.message.includes("404")) {
					setTrailers([]);
				}
			}
		};

		getTrailers();
	}, [contentType, id]);

	useEffect(() => {
		const getSimilarContent = async () => {
			try {
				const res = await axios.get(`/api/v1/${contentType}/${id}/similar`);
				setSimilarContent(res.data.similar);
			} catch (error) {
				if (error.message.includes("404")) {
					setSimilarContent([]);
				}
			}
		};

		getSimilarContent();
	}, [contentType, id]);

	useEffect(() => {
		const getContentDetails = async () => {
			try {
				const res = await axios.get(`/api/v1/${contentType}/${id}/details`);
				setContent(res.data.content);
			} catch (error) {
				if (error.message.includes("404")) {
					setContent(null);
				}
			} finally {
				setLoading(false);
			}
		};

		getContentDetails();
	}, [contentType, id]);

	const handleNext = () => {
		if (currentTrailerIdx < trailers.length - 1) setCurrentTrailerIdx(currentTrailerIdx + 1);
	};
	const handlePrev = () => {
		if (currentTrailerIdx > 0) setCurrentTrailerIdx(currentTrailerIdx - 1);
	};

	const scrollLeft = () => {
		if (sliderRef.current) sliderRef.current.scrollBy({ left: -sliderRef.current.offsetWidth, behavior: "smooth" });
	};
	const scrollRight = () => {
		if (sliderRef.current) sliderRef.current.scrollBy({ left: sliderRef.current.offsetWidth, behavior: "smooth" });
	};

	if (loading)
		return (
			<div className='min-h-screen bg-black p-10'>
				<WatchPageSkeleton />
			</div>
		);

	if (!content) {
		return (
			<div className='bg-black text-white h-screen'>
				<div className='max-w-6xl mx-auto'>
					<Navbar />
					<div className='text-center mx-auto px-4 py-8 h-full mt-40'>
						<h2 className='text-2xl sm:text-5xl font-bold text-balance'>Content not found 😥</h2>
					</div>
				</div>
			</div>
		);
	}

	return (
		<div className='bg-black min-h-screen text-white'>
			<div className='mx-auto container px-4 py-8 h-full'>
				<Navbar />

				{trailers.length > 0 && (
					<div className='flex justify-between items-center mb-4'>
						<button
							className={`
							bg-gray-500/70 hover:bg-gray-500 text-white py-2 px-4 rounded ${
								currentTrailerIdx === 0 ? "opacity-50 cursor-not-allowed " : ""
							}}
							`}
							disabled={currentTrailerIdx === 0}
							onClick={handlePrev}
						>
							<ChevronLeft size={24} />
						</button>

						<button
							className={`
							bg-gray-500/70 hover:bg-gray-500 text-white py-2 px-4 rounded ${
								currentTrailerIdx === trailers.length - 1 ? "opacity-50 cursor-not-allowed " : ""
							}}
							`}
							disabled={currentTrailerIdx === trailers.length - 1}
							onClick={handleNext}
						>
							<ChevronRight size={24} />
						</button>
					</div>
				)}

				<div className='aspect-video mb-8 p-2 sm:px-10 md:px-32'>
					{trailers.length > 0 && (
						<ReactPlayer
							controls={true}
							width={"100%"}
							height={"70vh"}
							className='mx-auto overflow-hidden rounded-lg'
							url={`https://www.youtube.com/watch?v=${trailers[currentTrailerIdx].key}`}
						/>
					)}

					{trailers?.length === 0 && (
						<h2 className='text-xl text-center mt-5'>
							No trailers available for{" "}
							<span className='font-bold text-red-600'>{content?.title || content?.name}</span> 😥
						</h2>
					)}
				</div>

				{/* movie details */}
				<div
					className='flex flex-col md:flex-row items-center justify-between gap-20 
				max-w-6xl mx-auto'
				>
					<div className='mb-4 md:mb-0'>
						<h2 className='text-5xl font-bold text-balance'>{content?.title || content?.name}</h2>

						<p className='mt-2 text-lg'>
							{formatReleaseDate(content?.release_date || content?.first_air_date)} |{" "}
							{content?.adult ? (
								<span className='text-red-600'>18+</span>
							) : (
								<span className='text-green-600'>PG-13</span>
							)}{" "}
						</p>
						<p className='mt-4 text-lg'>{content?.overview}</p>
					</div>
					<img
						src={ORIGINAL_IMG_BASE_URL + content?.poster_path}
						alt='Poster image'
						className='max-h-[600px] rounded-md'
					/>
				</div>

				{similarContent.length > 0 && (
					<div className='mt-12 max-w-5xl mx-auto relative'>
						<h3 className='text-3xl font-bold mb-4'>Similar Movies/Tv Show</h3>

						<div className='flex overflow-x-scroll scrollbar-hide gap-4 pb-4 group' ref={sliderRef}>
							{similarContent.map((content) => {
								if (content.poster_path === null) return null;
								return (
									<Link key={content.id} to={`/watch/${content.id}`} className='w-52 flex-none'>
										<img
											src={SMALL_IMG_BASE_URL + content.poster_path}
											alt='Poster path'
											className='w-full h-auto rounded-md'
										/>
										<h4 className='mt-2 text-lg font-semibold'>{content.title || content.name}</h4>
									</Link>
								);
							})}

							<ChevronRight
								className='absolute top-1/2 -translate-y-1/2 right-2 w-8 h-8
										opacity-0 group-hover:opacity-100 transition-all duration-300 cursor-pointer
										 bg-red-600 text-white rounded-full'
								onClick={scrollRight}
							/>
							<ChevronLeft
								className='absolute top-1/2 -translate-y-1/2 left-2 w-8 h-8 opacity-0 
								group-hover:opacity-100 transition-all duration-300 cursor-pointer bg-red-600 
								text-white rounded-full'
								onClick={scrollLeft}
							/>
						</div>
					</div>
				)}
			</div>
		</div>
	);
};
export default WatchPage;
```


### 05:49:50 - Building the Search Page

新增`pages/SearchPage.jsx`文件，文件内容如下所示：

```jsx
import { useState } from "react";
import { useContentStore } from "../store/content";
import Navbar from "../components/Navbar";
import { Search } from "lucide-react";
import toast from "react-hot-toast";
import axios from "axios";
import { ORIGINAL_IMG_BASE_URL } from "../utils/constants";
import { Link } from "react-router-dom";

const SearchPage = () => {
	const [activeTab, setActiveTab] = useState("movie");
	const [searchTerm, setSearchTerm] = useState("");

	const [results, setResults] = useState([]);
	const { setContentType } = useContentStore();

	const handleTabClick = (tab) => {
		setActiveTab(tab);
		tab === "movie" ? setContentType("movie") : setContentType("tv");
		setResults([]);
	};

	const handleSearch = async (e) => {
		e.preventDefault();
		try {
			const res = await axios.get(`/api/v1/search/${activeTab}/${searchTerm}`);
			setResults(res.data.content);
		} catch (error) {
			if (error.response.status === 404) {
				toast.error("Nothing found, make sure you are searching under the right category");
			} else {
				toast.error("An error occurred, please try again later");
			}
		}
	};

	return (
		<div className='bg-black min-h-screen text-white'>
			<Navbar />
			<div className='container mx-auto px-4 py-8'>
				<div className='flex justify-center gap-3 mb-4'>
					<button
						className={`py-2 px-4 rounded ${
							activeTab === "movie" ? "bg-red-600" : "bg-gray-800"
						} hover:bg-red-700`}
						onClick={() => handleTabClick("movie")}
					>
						Movies
					</button>
					<button
						className={`py-2 px-4 rounded ${
							activeTab === "tv" ? "bg-red-600" : "bg-gray-800"
						} hover:bg-red-700`}
						onClick={() => handleTabClick("tv")}
					>
						TV Shows
					</button>
					<button
						className={`py-2 px-4 rounded ${
							activeTab === "person" ? "bg-red-600" : "bg-gray-800"
						} hover:bg-red-700`}
						onClick={() => handleTabClick("person")}
					>
						Person
					</button>
				</div>

				<form className='flex gap-2 items-stretch mb-8 max-w-2xl mx-auto' onSubmit={handleSearch}>
					<input
						type='text'
						value={searchTerm}
						onChange={(e) => setSearchTerm(e.target.value)}
						placeholder={"Search for a " + activeTab}
						className='w-full p-2 rounded bg-gray-800 text-white'
					/>
					<button className='bg-red-600 hover:bg-red-700 text-white p-2 rounded'>
						<Search className='size-6' />
					</button>
				</form>

				<div className='grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4'>
					{results.map((result) => {
						if (!result.poster_path && !result.profile_path) return null;

						return (
							<div key={result.id} className='bg-gray-800 p-4 rounded'>
								{activeTab === "person" ? (
									<div className='flex flex-col items-center'>
										<img
											src={ORIGINAL_IMG_BASE_URL + result.profile_path}
											alt={result.name}
											className='max-h-96 rounded mx-auto'
										/>
										<h2 className='mt-2 text-xl font-bold'>{result.name}</h2>
									</div>
								) : (
									<Link
										to={"/watch/" + result.id}
										onClick={() => {
											setContentType(activeTab);
										}}
									>
										<img
											src={ORIGINAL_IMG_BASE_URL + result.poster_path}
											alt={result.title || result.name}
											className='w-full h-auto rounded'
										/>
										<h2 className='mt-2 text-xl font-bold'>{result.title || result.name}</h2>
									</Link>
								)}
							</div>
						);
					})}
				</div>
			</div>
		</div>
	);
};
export default SearchPage;
```


### 06:05:20 - Building the Search History Page

新增`pages/SearchHistoryPage.jsx`，文件内容如下所示：

```jsx
import axios from "axios";
import { useEffect, useState } from "react";
import Navbar from "../components/Navbar";
import { SMALL_IMG_BASE_URL } from "../utils/constants";
import { Trash } from "lucide-react";
import toast from "react-hot-toast";

function formatDate(dateString) {
	// Create a Date object from the input date string
	const date = new Date(dateString);

	const monthNames = ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"];

	// Extract the month, day, and year from the Date object
	const month = monthNames[date.getUTCMonth()];
	const day = date.getUTCDate();
	const year = date.getUTCFullYear();

	// Return the formatted date string
	return `${month} ${day}, ${year}`;
}

const SearchHistoryPage = () => {
	const [searchHistory, setSearchHistory] = useState([]);

	useEffect(() => {
		const getSearchHistory = async () => {
			try {
				const res = await axios.get(`/api/v1/search/history`);
				setSearchHistory(res.data.content);
			} catch (error) {
				setSearchHistory([]);
			}
		};
		getSearchHistory();
	}, []);

	const handleDelete = async (entry) => {
		try {
			await axios.delete(`/api/v1/search/history/${entry.id}`);
			setSearchHistory(searchHistory.filter((item) => item.id !== entry.id));
		} catch (error) {
			toast.error("Failed to delete search item");
		}
	};

	if (searchHistory?.length === 0) {
		return (
			<div className='bg-black min-h-screen text-white'>
				<Navbar />
				<div className='max-w-6xl mx-auto px-4 py-8'>
					<h1 className='text-3xl font-bold mb-8'>Search History</h1>
					<div className='flex justify-center items-center h-96'>
						<p className='text-xl'>No search history found</p>
					</div>
				</div>
			</div>
		);
	}

	return (
		<div className='bg-black text-white min-h-screen'>
			<Navbar />

			<div className='max-w-6xl mx-auto px-4 py-8'>
				<h1 className='text-3xl font-bold mb-8'>Search History</h1>
				<div className='grid grid-cols-1 sm:grid-cols-2 md:grid-cols-2 lg:grid-cols-3  gap-4'>
					{searchHistory?.map((entry) => (
						<div key={entry.id} className='bg-gray-800 p-4 rounded flex items-start'>
							<img
								src={SMALL_IMG_BASE_URL + entry.image}
								alt='History image'
								className='size-16 rounded-full object-cover mr-4'
							/>
							<div className='flex flex-col'>
								<span className='text-white text-lg'>{entry.title}</span>
								<span className='text-gray-400 text-sm'>{formatDate(entry.createdAt)}</span>
							</div>

							<span
								className={`py-1 px-3 min-w-20 text-center rounded-full text-sm  ml-auto ${
									entry.searchType === "movie"
										? "bg-red-600"
										: entry.searchType === "tv"
										? "bg-blue-600"
										: "bg-green-600"
								}`}
							>
								{entry.searchType[0].toUpperCase() + entry.searchType.slice(1)}
							</span>
							<Trash
								className='size-5 ml-4 cursor-pointer hover:fill-red-600 hover:text-red-600'
								onClick={() => handleDelete(entry)}
							/>
						</div>
					))}
				</div>
			</div>
		</div>
	);
};
export default SearchHistoryPage;
```

代码中`searchHistory?.length === 0`这是什么意思？

这段代码是对`searchHistory`这个变量进行空值或者未定义的判断。`searchHistory?.length`中的问号是可选链操作符，它在对象的属性链上允许读取目标对象及其子对象的属性。如果`searchHistory`是null或者undefined，那么整个表达式的值为undefined，不会报错。最后，`=== 0`是判断`searchHistory`数组的长度是否为0，即判断是否为空。整个代码的意思就是判断`searchHistory`数组是否为空。
### 06:14:55 - Building a Custom 404 Page

修改`App.jsx`文件，增加`<Route path='/*' element={<NotFoundPage />} />`

新增`pages/404.jsx`，文件内容如下所示：

```jsx
import { Link } from "react-router-dom";

const NotFoundPage = () => {
	return (
		<div
			className='min-h-screen bg-cover bg-center flex flex-col justify-center items-center text-white'
			style={{ backgroundImage: `url('/404.png')` }}
		>
			<header className='absolute top-0 left-0 p-4 bg-black w-full '>
				<Link to={"/"}>
					<img src='/netflix-logo.png' alt='Netflix' className='h-8' />
				</Link>
			</header>
			<main className='text-center error-page--content z-10'>
				<h1 className='text-7xl font-semibold mb-4'>Lost your way?</h1>
				<p className='mb-6 text-xl'>
					Sorry, we can't find that page. You'll find lots to explore on the home page.
				</p>
				<Link to={"/"} className='bg-white text-black py-2 px-4 rounded'>
					Netflix Home
				</Link>
			</main>
		</div>
	);
};
export default NotFoundPage;
```

在`index.css`中加入如下内容：

```css
.error-page--content::before {
	background: radial-gradient(
		ellipse at center,
		rgba(0, 0, 0, 0.5) 0,
		rgba(0, 0, 0, 0.2) 45%,
		rgba(0, 0, 0, 0.1) 55%,
		transparent 70%
	);
	bottom: -10vw;
	content: "";
	left: 10vw;
	position: absolute;
	right: 10vw;
	top: -10vw;
	z-index: -1;
}
```
### 06:18:55 - Testing Our App and Small Fixes

### 附加功能：搜索时可以使用Enter键确认

在`SearchPage.jsx`中加入如下代码：

```jsx
const handleKeyDown = (e) => {
        if (e.key === "Enter") {
            handleSearch();
        }
    }
```

在`input`输入框中加入`onKeyDown={handleKeyDown}`
### 06:24:40 - Detailed Deployment Guide

修改`server.js`文件，现在`server.js`文件内容如下所示：

```js
import express from "express";
import cookieParser from "cookie-parser";
import path from "path";

import authRoutes from "./routes/auth.route.js";
import movieRoutes from "./routes/movie.route.js";
import tvRoutes from "./routes/tv.route.js";
import searchRoutes from "./routes/search.route.js";

import { ENV_VARS } from "./config/envVars.js";
import { connectDB } from "./config/db.js";
import { protectRoute } from "./middleware/protectRoute.js";

const app = express();

const PORT = ENV_VARS.PORT;
const __dirname = path.resolve();

app.use(express.json()); // will allow us to parse req.body
app.use(cookieParser());

app.use("/api/v1/auth", authRoutes);
app.use("/api/v1/movie", protectRoute, movieRoutes);
app.use("/api/v1/tv", protectRoute, tvRoutes);
app.use("/api/v1/search", protectRoute, searchRoutes);

if (ENV_VARS.NODE_ENV === "production") {
	app.use(express.static(path.join(__dirname, "/frontend/dist")));

	app.get("*", (req, res) => {
		res.sendFile(path.resolve(__dirname, "frontend", "dist", "index.html"));
	});
}

app.listen(PORT, () => {
	console.log("Server started at http://localhost:" + PORT);
	connectDB();
});
```

修改根目录下的`package.json`文件，现在`package.json`文件内容如下所示：

```json
{
  "name": "netflix",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "dev": "NODE_ENV=development nodemon backend/server.js",
		"start": "NODE_ENV=production node backend/server.js",
		"build": "npm install && npm install --prefix frontend && npm run build --prefix frontend"
  },
  "keywords": [],
  "type": "module",
  "author": "",
  "license": "ISC",
  "description": "",
  "dependencies": {
    "axios": "^1.7.7",
    "bcryptjs": "^2.4.3",
    "cookie-parser": "^1.4.6",
    "dotenv": "^16.4.5",
    "express": "^4.21.0",
    "jsonwebtoken": "^9.0.2",
    "mongoose": "^8.6.3"
  },
  "devDependencies": {
    "nodemon": "^3.1.7"
  }
}
```

移动`.gitignore`文件，并添加`.env`

部署到`Render`平台

指令`npm run build`和`npm run start`

注意：**环境变量不能添加任何`NODE_ENV`相关内容**，因为`package.json`文件中已指定
### 06:48:53 - Oops! I almost forgot this... bye

修改`SignUpPage.jsx`和`LoginPage.jsx`状态显示语句

在`index.css`中加入如下内容：

```css
::-webkit-scrollbar {
	width: 8px;
}

::-webkit-scrollbar-thumb {
	background-color: #4b5563;
	border-radius: 6px;
}

::-webkit-scrollbar-track {
	background-color: #1a202c;
}
```
