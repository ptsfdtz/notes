# qt

Qt 用于开发跨平台桌面应用，常用 C++ 编写界面和业务逻辑。

## 创建项目

安装 Qt Online Installer 和 Qt Creator，创建 `Qt Widgets Application` 或 `Qt Quick Application` 项目。命令行 CMake 项目可以这样构建：

```powershell
cmake -S . -B build
cmake --build build --config Debug
```

## 信号和槽

```cpp
connect(ui->pushButton, &QPushButton::clicked, this, [this] {
    ui->label->setText("hello qt");
});
```

信号用于通知事件，槽函数用于处理事件。耗时任务不要放在 GUI 线程中，否则窗口会失去响应。

## 串口通信

安装并链接 `Qt Serial Port` 模块后可使用：

```cpp
QSerialPort serial;
serial.setPortName("COM3");
serial.setBaudRate(QSerialPort::Baud115200);
serial.open(QIODevice::ReadWrite);
```

## 经验总结

1. UI 更新必须在 GUI 线程执行，后台工作使用 `QThread` 或任务机制。
2. 串口数据可能分包到达，应使用缓冲区按协议拼包，不能假设一次 `readAll()` 就是一帧。
3. 发布前在目标机器验证 Qt 运行库是否已随安装包部署。
