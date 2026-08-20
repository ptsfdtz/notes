# android

Android 原生应用推荐使用 Kotlin 和 Android Studio 开发。

## 创建项目

在 Android Studio 中创建 `Empty Activity` 项目，选择 Kotlin。创建后先运行默认项目，确认模拟器或真机连接正常。

命令行构建：

```powershell
.\gradlew.bat assembleDebug
.\gradlew.bat test
.\gradlew.bat lint
```

## 权限声明

网络权限示例：

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

定位、蓝牙、相机等危险权限除了在 `AndroidManifest.xml` 声明外，还必须在运行时请求，并处理用户拒绝的结果。

## 经验总结

1. 不要在主线程执行网络、数据库或长时间 I/O 操作。
2. 使用 ViewModel 保存界面状态，避免旋转屏幕或进程重建后数据丢失。
3. 发布前检查 `minSdk`、签名文件、混淆规则和不同 Android 版本的权限行为。
