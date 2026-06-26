---
order: 0
---

# Introduction

## What is the JadeView E-Language SDK

The JadeView E-Language SDK is a WebView window library designed specifically for E-Language developers. Built on Rust, it provides a simple and easy-to-use API to help developers quickly build modern desktop applications.

## Why Choose the JadeView E-Language SDK

- **Modern Technology Stack**: Built on the latest WebView technology, supporting modern Web standards and HTML5 features
- **Simple and Easy to Use**: An API designed specifically for E-Language developers, easy to understand and use
- **High Performance**: Built on Rust at its core, offering excellent performance and stability
- **Cross-Platform Potential**: Although it currently supports primarily Windows, it is designed with cross-platform extension in mind
- **Active Development**: Continuously updated and improved, with new features and optimizations added regularly

## Getting Resources

- **GitHub Repository**: [Download the SDK source code](https://github.com/JadeViewDocs/JadeView/)
- **Gitee Repository**: [Download the SDK source code](https://gitee.com/ilinxuan/JadeView_library)
In the code files, find the `e_v0.xx` file, which contains the source code required for E-Language
- **Download the DLL**: [Github](https://github.com/JadeViewDocs/JadeView/releases) or [Gitee](https://gitee.com/ilinxuan/JadeView_library/releases)
- **E-Language DLL**: Generally use `JadeView_x86_dynamic.dll` or `JadeView_x86_static.dll`



## Key Features

### Window Management

- Supports creating and managing multiple WebView windows
- Flexible window configuration options (size, position, title, etc.)
- Supports window operations such as maximize, minimize, and fullscreen
- Supports always-on-top windows and focus management

### Theme Support

- Three built-in theme modes: light, dark, and automatically follow the system
- Themes can be switched dynamically
- Supports custom theme colors

### Window Styles

- Supports borderless windows
- Supports transparent windows and custom background colors
- Supports rounded window corners (depending on system support)
- Supports window shadow effects

### WebView Features

- Supports modern Web standards and HTML5 features
- Supports interaction between JavaScript and E-Language
- Supports injecting custom JavaScript code
- Supports developer tools (optional)

## Technical Architecture

The JadeView E-Language SDK adopts a layered architecture design:

1. **Core Layer**: A WebView core library built on Rust
2. **DLL Interface**: DLL functions provided for E-Language to call
3. **E-Language Wrapper**: E-Language modules and classes that simplify the use of the SDK
4. **Example Code**: Examples are provided for various usage scenarios

## System Requirements

- Operating System: Windows 7 and above
- E-Language Version: E-Language 5.3 and above
- .NET Framework: 4.0 and above
- Hardware Requirements: At least 2GB RAM, 50MB available disk space

## Use Cases

The JadeView E-Language SDK is suitable for the following scenarios:

1. **Modern Desktop Applications**: Build modern desktop application interfaces using Web technologies
2. **Legacy Application Upgrades**: Add a modern Web interface to legacy E-Language applications
3. **Tool Development**: Quickly build various tool-type applications
4. **Prototype Development**: Quickly validate application concepts and designs
5. **Web Application Desktopization**: Package existing Web applications as desktop applications

## License

The JadeView E-Language SDK is licensed under the MIT License, allowing free use, modification, and distribution.

## Community and Support

- GitHub Repository: [https://github.com/JadeViewDocs/docs](https://github.com/JadeViewDocs/docs)
- Documentation Website: [https://jadeviewdocs.github.io](https://jadeviewdocs.github.io)
- If you have any questions or suggestions, you are welcome to submit an Issue or Pull Request
