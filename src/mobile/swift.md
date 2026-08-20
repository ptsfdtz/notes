# Swift

Swift 用于开发 Apple 平台（iOS、macOS）应用，配合 Xcode 使用；也可通过 Swift Package Manager 编写命令行工具和跨平台库。

## 创建项目

在 macOS 上安装 Xcode，创建 `App` 项目并选择 SwiftUI 或 UIKit。

命令行构建：

```bash
xcodebuild -project MyApp.xcodeproj -scheme MyApp -configuration Debug build
```

## 基础界面（SwiftUI）

```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        Text("hello swift")
    }
}

@main
struct MyApp: App {
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
}
```

## 常用命令

```bash
swift --version
swift run          # 运行 SwiftPM 可执行目标
swift build        # 构建 SwiftPM 包
xcodebuild build   # 构建 Xcode 工程
```

## 经验总结

1. 界面更新必须在主线程执行，网络等耗时操作使用 `async/await`，不要在后台线程直接修改 UI。
2. 相机、定位、通知等权限需在 `Info.plist` 声明用途说明，并在真机验证用户拒绝权限的流程。
3. 发布前在模拟器和真机上检查不同屏幕尺寸、深色模式、横竖屏和低网速场景。
