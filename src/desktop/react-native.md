# react-native

React Native 使用 JavaScript/TypeScript 构建原生移动应用。新项目可先使用 Expo：

```powershell
npx create-expo-app@latest my-app
cd my-app
npx expo start
```

将网络请求、权限状态和导航状态明确建模。真机与模拟器都应验证，尤其检查不同屏幕尺寸、离线状态和系统权限被拒绝时的表现。

## 基础组件

```tsx
import { Button, Text, View } from 'react-native'
import { useState } from 'react'

export default function App() {
  const [count, setCount] = useState(0)
  return <View><Text>count: {count}</Text><Button title="add" onPress={() => setCount(count + 1)} /></View>
}
```

## 常用命令

```bash
npx expo start
npx expo start --android
npx expo start --ios
npx expo export
```

## 经验总结

1. 不要假设 Android 和 iOS 的权限、返回行为和字体渲染完全一致。
2. 长列表使用 `FlatList`，避免一次性渲染大量 `ScrollView` 子元素。
3. 发布前使用真机检查通知、相机、存储等原生权限。
