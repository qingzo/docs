---
order: 90
---

# Quick Start

This guide will help you quickly understand how to use the JadeView E-Language SDK to create your first WebView application.

## Environment Requirements

- Operating system: Windows 7 or later
- E-Language version: E-Language 5.3 or later

## SDK Import Steps

1. **Download the SDK**: Download the latest version of the JadeView E-Language SDK source code and examples from the following channels:
   - GitHub Releases: [https://github.com/JadeViewDocs/JadeView/releases](https://github.com/JadeViewDocs/JadeView/releases)
   - Jingyi Forum: [https://bbs.ijingyi.com/thread-14870797-1-1.html](https://bbs.ijingyi.com/thread-14870797-1-1.html)
2. **Extract the files**: Extract the downloaded SDK archive to a suitable directory
3. **Import the module**:
   - Open the E-Language IDE
   - Create a new E-Language project or open an existing one
   - Click the menu bar's "Tools" → "Support Library Configuration"
   - Click the "Select All" button, then click "OK"
   - Click the menu bar's "Insert" → "Module Reference Table"
   - Click the "Add Module Reference" button
   - Browse to the SDK extraction directory and select the required E-Language module file
   - Click the "Open" button to complete the module import

## Simple Example Code

Below is a simple example that demonstrates how to use the JadeView E-Language SDK to create a WebView window:

```e
.版本 2
.支持库 spec

.程序集 程序集1
.程序集变量 窗口设置, JadeView窗口设置
.程序集变量 JadeView实例, JadeView

.子程序 _启动子程序, 整数型, , 本子程序在程序启动后最先执行
    .局部变量 开启DevTools, 逻辑型
    
    开启DevTools ＝ 假
    
    ' 初始化 JadeView 运行时（异步）
    JadeView实例.初始化(开启DevTools, 取运行目录() ＋ "\log.txt", 取运行目录())
    
    ' 注册程序事件，监听初始化完成
    JadeView实例.注册程序事件("app-ready", &JadeView准备就绪)
    
    ' 运行消息循环
    JadeView实例.消息循环()
    
    返回 (0)  ' 可以根据您的需要返回任意数值

.子程序 JadeView准备就绪
    .参数 成功否, 逻辑型
    .参数 err, 文本型
    
    .如果 (成功否)
        ' 初始化窗口设置
        窗口设置.标题 ＝ "我的第一个 JadeView 应用"
        窗口设置.宽度 ＝ 800
        窗口设置.高度 ＝ 600
        窗口设置.窗口主题 ＝ #主题_亮色
        窗口设置.最大化按钮 ＝ 真
        窗口设置.最小化按钮 ＝ 真
        窗口设置.可调整大小边框 ＝ 真
        
        ' 初始化视窗设置
        .局部变量 视窗设置, JadeView视窗设置
        视窗设置.自动播放媒体 ＝ 假
        视窗设置.禁用右键菜单 ＝ 假
        
        ' 创建 WebView 窗口
        .局部变量 窗口ID, 整数型
        窗口ID ＝ JadeView实例.创建窗口("https://www.example.com", , 窗口设置, 视窗设置)
        
        .如果真 (窗口ID ＞ 0)
            调试输出 ("WebView 窗口创建成功，窗口ID：" ＋ 到文本 (窗口ID))
        .如果真结束
    .否则
        调试输出 ("JadeView 初始化失败！" ＋ err)
    .如果结束

.子程序 订阅IPC消息
    
    ' 注册前端事件
    JadeView实例.ipc_订阅("setTheme", &ipc_设置主题)
    JadeView实例.ipc_订阅("message", &ipc_对话消息)
    
.子程序 ipc_设置主题
    ' 实现主题设置逻辑
    
.子程序 ipc_对话消息
    ' 实现消息处理逻辑
```

## Code Explanation

1. **Assembly variable declarations**: Declares the `窗口设置` and `JadeView实例` assembly variables for global access
2. **_启动子程序**: The program entry function
   - Initializes the JadeView runtime (asynchronously)
   - Registers program events to listen for the initialization-complete event
   - Starts the message loop to handle window events
3. **JadeView准备就绪**: The callback function invoked after initialization completes
   - Checks whether initialization succeeded
   - On success, configures the window settings and viewport settings
   - Calls the `创建窗口` method to create the WebView window
   - Outputs the window creation result
   - On failure, outputs the error message
4. **订阅IPC消息**: Registers front-end events to handle messages from the front end
5. **ipc_设置主题**: Handles theme setting requests from the front end
6. **ipc_对话消息**: Handles conversation messages from the front end

**Key Notes**:
- JadeView initialization is asynchronous; the completion of initialization is handled via an event callback
- Window creation is also asynchronous: it returns the window ID first, and the actual window is created later
- You must call the `消息循环` method to start message processing
- Various events are handled using an event-driven approach

This example demonstrates the basic workflow of the JadeView E-Language SDK, including core features such as initialization, event subscription, and window creation. You can modify and extend this example according to your own needs.

## Running Result

After running the above code, you will see a new window titled "我的第一个 JadeView 应用", measuring 800x600 pixels, displaying the content of the `https://www.example.com` web page.

## Standalone Public Methods

In addition to the JadeView class methods, the E-Language SDK also provides a number of standalone public methods. These methods can be called directly, without going through a JadeView class instance.

### Main Standalone Public Methods

1. **JadeView消息循环**: Runs and keeps the main process alive; must be called after initialization, and is used to handle window events and IPC messages
2. **JadeView创建本地服务**: Creates a local HTTP server for serving local files
3. **GBK文本到UTF8文本**: Converts GBK-encoded text to UTF-8-encoded text, used when interacting with JavaScript
4. **UTF8文本到GBK文本**: Converts UTF-8-encoded text to GBK-encoded text, used to process text data received from JavaScript

### Example Code

```e
.局部变量 开启DevTools, 逻辑型

' 根据是否为调试版决定是否开启开发者工具
开启DevTools ＝ 是否为调试版()

' 整个初始化都是异步的
JadeView.初始化(开启DevTools, GBK文本到UTF8文本(取运行目录()) ＋ "\log.txt", 取运行目录())

' 订阅IPC消息
订阅IPC消息()

' 在异步中，千万不要等待返回后执行任何创建窗口操作
JadeView消息循环()

返回 (0)  ' 可以根据您的需要返回任意数值
```

## Common Questions

### 1. Why does compilation report that the "JadeView窗口设置" type cannot be found?

Please make sure you have correctly imported the JadeView E-Language SDK module and that the module contains the definitions of these data types.

### 2. Why does the program report at runtime that the DLL file cannot be found?

Please make sure the JadeView.dll file is located in the same directory as your E-Language program, or has been added to the system PATH environment variable.

### 3. Why isn't the window displayed?

Please check that your code correctly calls the `create_webview_window` function and that the returned window ID is greater than 0. You can use the `调试输出` function to view the specific error message.

## Next Steps

- Read the [Constants](./reference/constants.mdx) reference to learn about all the constants defined in the SDK
- Read the [Data Types](./reference/data-types.mdx) reference to learn about all the data types defined in the SDK
- Read the [JadeView Class Methods](./reference/methods.mdx) reference to learn about all the class methods defined in the SDK
- Read the [Standalone Public Methods](./reference/public-methods.mdx) reference to learn about all the standalone public methods defined in the SDK
- Try modifying the example code to use different window settings and viewport settings
- Explore how to implement interaction between JavaScript and E-Language

You have now successfully created your first JadeView E-Language SDK application. Continue exploring more features of the SDK!
