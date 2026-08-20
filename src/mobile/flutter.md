# flutter

Flutter 使用 Dart 开发跨平台移动应用，通过自身渲染引擎构建界面。

## 安装和验证

安装 Flutter SDK 并把 `flutter\bin` 加入 `Path` 后执行：

```powershell
flutter doctor
flutter --version
```

`flutter doctor` 会提示 Android SDK、模拟器或 IDE 插件等缺少的环境。

## 创建项目

```powershell
flutter create my_app
cd my_app
flutter run
```

## 基础界面

```dart
import 'package:flutter/material.dart';

void main() => runApp(const MaterialApp(home: HomePage()));

class HomePage extends StatelessWidget {
  const HomePage({super.key});

  @override
  Widget build(BuildContext context) {
    return const Scaffold(body: Center(child: Text('hello flutter')));
  }
}
```

## 常用命令

```powershell
flutter pub get
flutter analyze
flutter test
flutter build apk
```

## 经验总结

1. 页面状态不要全部放在 `setState`，复杂项目使用 Provider、Riverpod 或 Bloc 等统一管理。
2. 网络与存储操作都是异步的，界面要处理加载、失败和取消状态。
3. 打包前使用真机测试权限、深色模式、横竖屏和低网速场景。
