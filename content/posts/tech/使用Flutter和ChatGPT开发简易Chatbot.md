---
title: "使用 Flutter 和 ChatGPT开发简易 Chatbot"
date: 2025-05-07T18:34:25+08:00
lastmod: 2025-05-07T22:54:22+08:00
draft: false
math: true
categories:
- 编程
tags:
- Flutter
- ChatBot
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

## 前言

一直想做一个自己的聊天机器人APP来满足我本人的个性化需求，但一直没有行动。经过多天的努力，我终于完成了第一步——能够正常交互。后续会添加模型选择等功能。

项目UI参考自[Flutter Gemini ChatBot || Flutter Gemini API](https://www.youtube.com/watch?v=lQfScXATEDs)，相关代码链接如下所示： https://github.com/Nabinji/100-DaysOf-Futter/blob/main/api_integration/lib/Gemini%20ChatBot

## Flutter 基础命令

创建项目：`flutter create project_name`

调试项目：`flutter run`

打包成APK文件：`flutter build apk`
## 项目代码

相关`.dart`文件统一放到`lib`文件夹即可。
### main.dart

```dart
import 'package:chatwithalice/gemini_ai.dart';
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: GeminiChatBot(),
    );
  }
}
```

### gemini_ai.dart

```dart
import 'package:flutter/material.dart';
import 'package:intl/intl.dart';
import 'openai_service.dart';
import 'model.dart';

class GeminiChatBot extends StatefulWidget {
  const GeminiChatBot({super.key});
  @override
  State<GeminiChatBot> createState() => _GeminiChatBotState();
}

class _GeminiChatBotState extends State<GeminiChatBot> {
  TextEditingController promprController = TextEditingController();
  final OpenAIService openAIService = OpenAIService();
  final List<ModelMessage> prompt = [];

  Future<void> sendMessage() async {
    final message = promprController.text;
    // for prompt
    setState(() {
      promprController.clear();
      prompt.add(
        ModelMessage(isPrompt: true, message: message, time: DateTime.now()),
      );
    });
    // for respond
    final content = message;
    final response = await openAIService.chatGPTAPI(content);
    setState(() {
      prompt.add(
        ModelMessage(
          isPrompt: false,
          message: response,
          time: DateTime.now(),
        ),
      );
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.blue[100],
      appBar: AppBar(
        elevation: 3,
        backgroundColor: Colors.blue[100],
        title: const Text("AI ChatBot"),
      ),
      body: Column(
        children: [
          Expanded(
            child: ListView.builder(
              itemCount: prompt.length,
              itemBuilder: (context, index) {
                final message = prompt[index];
                return userPrompt(
                  isPrompt: message.isPrompt,
                  message: message.message,
                  date: DateFormat('hh:mm a').format(message.time),
                );
              },
            ),
          ),
          Padding(
            padding: const EdgeInsets.all(25),
            child: Row(
              children: [
                Expanded(
                  flex: 20,
                  child: TextField(
                    controller: promprController,
                    style: const TextStyle(color: Colors.black, fontSize: 20),
                    decoration: InputDecoration(
                      border: OutlineInputBorder(
                        borderRadius: BorderRadius.circular(20),
                      ),
                      hintText: "Enter a prompt here",
                    ),
                  ),
                ),
                const Spacer(),
                GestureDetector(
                  onTap: () {
                    sendMessage();
                  },
                  child: const CircleAvatar(
                    radius: 29,
                    backgroundColor: Colors.green,
                    child: Icon(Icons.send, color: Colors.white, size: 32),
                  ),
                ),
              ],
            ),
          ),
        ],
      ),
    );
  }

  Container userPrompt({
    required final bool isPrompt,
    required String message,
    required String date,
  }) {
    return Container(
      width: double.infinity,
      padding: const EdgeInsets.all(15),
      margin: const EdgeInsets.symmetric(
        vertical: 15,
      ).copyWith(left: isPrompt ? 80 : 15, right: isPrompt ? 15 : 80),
      decoration: BoxDecoration(
        color: isPrompt ? Colors.green : Colors.grey,
        borderRadius: BorderRadius.only(
          topLeft: const Radius.circular(20),
          topRight: const Radius.circular(20),
          bottomLeft: isPrompt ? const Radius.circular(20) : Radius.zero,
          bottomRight: isPrompt ? Radius.zero : const Radius.circular(20),
        ),
      ),
      child: Column(
        crossAxisAlignment: CrossAxisAlignment.start,
        children: [
          // for prompt and response
          Text(
            message,
            style: TextStyle(
              fontWeight: isPrompt ? FontWeight.bold : FontWeight.normal,
              fontSize: 18,
              color: isPrompt ? Colors.white : Colors.black,
            ),
          ),
          // for prompt and response time
          Text(
            date,
            style: TextStyle(
              fontSize: 14,
              color: isPrompt ? Colors.white : Colors.black,
            ),
          ),
        ],
      ),
    );
  }
}

```

### model.dart

```dart
class ModelMessage {
  final bool isPrompt;
  final String message;
  final DateTime time;

  ModelMessage({
    required this.isPrompt,
    required this.message,
    required this.time,
  });
}
```
### openai_service.dart

```dart
import 'dart:convert';
import 'secrets.dart';
import 'package:http/http.dart' as http;

class OpenAIService {
  final List<Map<String, String>> messages = [];

  Future<String> isArtPromptAPI(String prompt) async {
    try {
      final res = await http.post(
        //Uri.parse('https://api.openai.com/v1/chat/completions'),
        Uri.parse('https://api.chatanywhere.tech/v1/chat/completions'),
        headers: {
          'Content-Type': 'application/json',
          'Authorization': 'Bearer $openAIAPIKey',
        },
        body: jsonEncode({
          "model": "gpt-3.5-turbo",
          "messages": [
            {
              'role': 'user',
              'content':
                  'Does this message want to generate an AI picture, image, art or anything similar? $prompt . Simply answer with a yes or no.',
            }
          ],
        }),
      );
      print(res.body);
      if (res.statusCode == 200) {
        String content =
            jsonDecode(res.body)['choices'][0]['message']['content'];
        content = content.trim();

        switch (content) {
          case 'Yes':
          case 'yes':
          case 'Yes.':
          case 'yes.':
            final res = await dallEAPI(prompt);
            return res;
          default:
            final res = await chatGPTAPI(prompt);
            return res;
        }
      }
      return 'An internal error occurred';
    } catch (e) {
      return e.toString();
    }
  }

  Future<String> chatGPTAPI(String prompt) async {
    messages.add({
      'role': 'user',
      'content': prompt,
    });
    try {
      final res = await http.post(
        Uri.parse('https://api.chatanywhere.tech/v1/chat/completions'),
        headers: {
          'Content-Type': 'application/json',
          'Authorization': 'Bearer $openAIAPIKey',
        },
        body: jsonEncode({
          "model": "gpt-3.5-turbo",
          "messages": messages,
        }),
      );

      if (res.statusCode == 200) {
        String content =
            jsonDecode(res.body)['choices'][0]['message']['content'];
        content = content.trim();

        messages.add({
          'role': 'assistant',
          'content': content,
        });
        return content;
      }
      return 'An internal error occurred';
    } catch (e) {
      return e.toString();
    }
  }

  Future<String> dallEAPI(String prompt) async {
    messages.add({
      'role': 'user',
      'content': prompt,
    });
    try {
      final res = await http.post(
        Uri.parse('https://api.chatanywhere.tech/v1/images/generations'),
        headers: {
          'Content-Type': 'application/json',
          'Authorization': 'Bearer $openAIAPIKey',
        },
        body: jsonEncode({
          'prompt': prompt,
          'n': 1,
        }),
      );

      if (res.statusCode == 200) {
        String imageUrl = jsonDecode(res.body)['data'][0]['url'];
        imageUrl = imageUrl.trim();

        messages.add({
          'role': 'assistant',
          'content': imageUrl,
        });
        return imageUrl;
      }
      return 'An internal error occurred';
    } catch (e) {
      return e.toString();
    }
  }
}
```

注意：这里需要自己的情况配置`BaseURL`
### secrets.dart

```dart
const openAIAPIKey = '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';
```

注意：这里需要配置自己的`openAIAPIKey`

### pubspec.yaml

```yaml
name: chatwithalice
description: "A new Flutter project."
# The following line prevents the package from being accidentally published to
# pub.dev using `flutter pub publish`. This is preferred for private packages.
publish_to: 'none' # Remove this line if you wish to publish to pub.dev

# The following defines the version and build number for your application.
# A version number is three numbers separated by dots, like 1.2.43
# followed by an optional build number separated by a +.
# Both the version and the builder number may be overridden in flutter
# build by specifying --build-name and --build-number, respectively.
# In Android, build-name is used as versionName while build-number used as versionCode.
# Read more about Android versioning at https://developer.android.com/studio/publish/versioning
# In iOS, build-name is used as CFBundleShortVersionString while build-number is used as CFBundleVersion.
# Read more about iOS versioning at
# https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Articles/CoreFoundationKeys.html
# In Windows, build-name is used as the major, minor, and patch parts
# of the product and file versions while build-number is used as the build suffix.
version: 1.0.0+1

environment:
  sdk: ^3.7.2

# Dependencies specify other packages that your package needs in order to work.
# To automatically upgrade your package dependencies to the latest versions
# consider running `flutter pub upgrade --major-versions`. Alternatively,
# dependencies can be manually updated by changing the version numbers below to
# the latest version available on pub.dev. To see which dependencies have newer
# versions available, run `flutter pub outdated`.
dependencies:
  flutter:
    sdk: flutter

  # The following adds the Cupertino Icons font to your application.
  # Use with the CupertinoIcons class for iOS style icons.
  cupertino_icons: ^1.0.8
  http: ^1.4.0
  intl: ^0.20.2

dev_dependencies:
  flutter_test:
    sdk: flutter

  # The "flutter_lints" package below contains a set of recommended lints to
  # encourage good coding practices. The lint set provided by the package is
  # activated in the `analysis_options.yaml` file located at the root of your
  # package. See that file for information about deactivating specific lint
  # rules and activating additional ones.
  flutter_lints: ^5.0.0

# For information on the generic Dart part of this file, see the
# following page: https://dart.dev/tools/pub/pubspec

# The following section is specific to Flutter packages.
flutter:

  # The following line ensures that the Material Icons font is
  # included with your application, so that you can use the icons in
  # the material Icons class.
  uses-material-design: true

  # To add assets to your application, add an assets section, like this:
  # assets:
  #   - images/a_dot_burr.jpeg
  #   - images/a_dot_ham.jpeg

  # An image asset can refer to one or more resolution-specific "variants", see
  # https://flutter.dev/to/resolution-aware-images

  # For details regarding adding assets from package dependencies, see
  # https://flutter.dev/to/asset-from-package

  # To add custom fonts to your application, add a fonts section here,
  # in this "flutter" section. Each entry in this list should have a
  # "family" key with the font family name, and a "fonts" key with a
  # list giving the asset and other descriptors for the font. For
  # example:
  # fonts:
  #   - family: Schyler
  #     fonts:
  #       - asset: fonts/Schyler-Regular.ttf
  #       - asset: fonts/Schyler-Italic.ttf
  #         style: italic
  #   - family: Trajan Pro
  #     fonts:
  #       - asset: fonts/TrajanPro.ttf
  #       - asset: fonts/TrajanPro_Bold.ttf
  #         weight: 700
  #
  # For details regarding fonts from package dependencies,
  # see https://flutter.dev/to/font-from-package

```

## 关于Android应用联网权限的问题解析与解决方案

在正常情况下，打包完成的APK安装后应能正常联网，否则可能出现发送消息后无回复的情况，甚至伴随`SocketException`报错。常见错误示例为：

```
SocketException: Failed host lookup: 'www.xyz.com' (OS Error: No address associated with hostname, errno = 7)
```

对此问题，可以参考这篇详细的解答：[如何解决SocketException: Failed host lookup？](https://dev59.com/1VQJ5IYBdhLWcg3wHSA8)。

---

### 常见原因与解决步骤

很多时候，应用在调试模式下一切正常，发布后却无法联网，极大概率是权限配置不完整导致。请确认在你的`AndroidManifest.xml`中是否正确声明了联网相关权限。通常涉及以下几个Manifest文件：

- `your_project_root_directory/android/app/src/debug/AndroidManifest.xml`
- `your_project_root_directory/android/app/src/main/AndroidManifest.xml`
- `your_project_root_directory/android/app/src/profile/AndroidManifest.xml`

如果你在这些文件里没有以下权限声明，请务必添加：

```xml
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
```

---

### 两条权限声明的具体作用区别

1. **`<uses-permission android:name="android.permission.INTERNET"/>`**
    
    - 这个权限允许应用访问互联网，是任何进行网络请求（API调用、网页加载、发送消息等）不可缺少的核心权限。
    - 没有该权限，应用无法建立网络连接，网络相关功能会直接失败。
2. **`<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>`**
    
    - 允许应用查询当前的网络状态，比如是否联网、网络类型（Wi-Fi、移动数据）等。
    - 本身不允许进行数据传输，但通常用于逻辑判断，比如在没有网络时提醒用户，或在不同网络下调整数据加载策略。

---

### 权限总结及最佳实践

|权限名称|权限功能|是否必须联网可用|
|---|---|---|
|`INTERNET`|允许应用访问网络，进行数据传输。|必须|
|`ACCESS_NETWORK_STATE`|获取网络连接状态信息，判断是否联网及网络类型。|建议添加（非必需，但有助于更好用户体验）|

**建议：**

- 至少声明`INTERNET`权限，确保应用能正常联网。
- 若需要根据当前网络状态做业务判断或优化，建议同时声明`ACCESS_NETWORK_STATE`权限。

---

如果你添加权限仍然遇到问题，建议检查网络权限是否被系统或用户限制，比如安卓10以后的隐私权限策略，或设备网络环境是否正常。也可进一步查看具体异常栈信息进行排查。






