# C/C++

## Windows 开发环境

可安装 Visual Studio Build Tools，并勾选“使用 C++ 的桌面开发”；或使用 MSYS2/MinGW。验证编译器：

```powershell
cl
g++ --version
```

## CMake 项目

```powershell
cmake -S . -B build
cmake --build build --config Debug
ctest --test-dir build -C Debug
```

将编译器选项、依赖和目标定义写入 `CMakeLists.txt`，不要依赖本机 IDE 的隐式配置。开启警告并尽可能在开发阶段将警告视为错误。

## 最小 CMake 项目

创建 `CMakeLists.txt`：

```cmake
cmake_minimum_required(VERSION 3.20)
project(hello LANGUAGES CXX)
set(CMAKE_CXX_STANDARD 20)
add_executable(hello main.cpp)
```

创建 `main.cpp`：

```cpp
#include <iostream>

int main() {
    std::cout << "hello c++\n";
}
```

## 常用命令

```powershell
cmake -S . -B build -DCMAKE_BUILD_TYPE=Debug
cmake --build build
cmake --build build --config Release
```

## 经验总结

1. 不要提交 `build` 目录，构建产物应由 CMake 重新生成。
2. Windows 下 MSVC 是多配置生成器，`--config Debug` 或 `Release` 不能省略。
3. 使用 sanitizers、静态分析和单元测试尽早发现内存与未定义行为问题。
