# stm32

STM32 是常用的 ARM Cortex-M 微控制器系列。STM32CubeMX 可用于配置时钟、引脚和外设并生成初始化代码。

## 基本流程

1. 在 STM32CubeMX 选择准确芯片或开发板型号。
2. 配置时钟树、GPIO、调试接口和所需外设。
3. 生成 Keil 或 CMake 工程后编译、下载并验证。

## GPIO 点灯例子

```c
HAL_GPIO_WritePin(LED_GPIO_Port, LED_Pin, GPIO_PIN_SET);
HAL_Delay(500);
HAL_GPIO_WritePin(LED_GPIO_Port, LED_Pin, GPIO_PIN_RESET);
HAL_Delay(500);
```

## UART 接收

```c
uint8_t byte;
HAL_UART_Receive(&huart1, &byte, 1, HAL_MAX_DELAY);
HAL_UART_Transmit(&huart1, &byte, 1, 100);
```

中断或 DMA 接收更适合持续数据流；不要在中断回调中执行长时间处理。

## 经验总结

1. 首先让 LED、串口日志和下载调试工作，再接入复杂外设。
2. 时钟配置错误会导致串口波特率、定时器和延时全部异常。
3. 使用逻辑分析仪或示波器验证波形，不能只根据代码判断硬件时序正确。
