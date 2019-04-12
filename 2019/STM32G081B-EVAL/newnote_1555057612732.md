/**
  @page BSP  Example on how to use the BSP drivers
  
  @verbatim
  ******************************************************************************
  * @file    BSP/BSP_Example/readme.txt 
  * @author  MCD Application Team
  * @brief   Description of the BSP example.
  ******************************************************************************
  *
  * Copyright (c) 2018 STMicroelectronics. All rights reserved.
  *
  * This software component is licensed by ST under BSD 3-Clause license,
  * the "License"; You may not use this file except in compliance with the
  * License. You may obtain a copy of the License at:
  *                       opensource.org/licenses/BSD-3-Clause
  *
  ******************************************************************************
  @endverbatim

@par Example Description 

This example provides a description of how to use the different BSP drivers. 

At the beginning of the main program the HAL_Init() function is called to reset 
all the peripherals, initialize the Flash interface and the systick.
Then the SystemClock_Config() function is used to configure the system
clock (SYSCLK) to run at 56 MHz.

This example shows how to use the different functionalities of components 
available on the board by switching between all tests using Tamper push-button button. 

 ** Push the User button to start first Test.  
Blue Led (LD4) will blink between each test. Press Tamper push-button to start another test:

 ** JOYSTICK **
Use the joystick button to move a pointer inside a rectangle 
(up/down/right/left) and change the pointer color(select).

 ** LCD **
This example shows how to use the different LCD features to display string
with different fonts, to display different shapes and to draw a bitmap.

 ** SD **
This example shows how to erase, write and read the SD card and also 
how to detect the presence of the card.

 ** TSENSOR **
This example show how to read a Temperature using the temperature sensor.
Temperature sensor is phycicaly present on daughter board MB1315.
Please make sure that MB1351 daughter board is mounted on top of EVAL board.

 ** LCD LOG **
This example show how to use the LCD log features. 

@note Care must be taken when using HAL_Delay(), this function provides accurate delay (in milliseconds)
      based on variable incremented in HAL time base ISR. This implies that if HAL_Delay() is called from
      a peripheral ISR process, then the HAL time base interrupt must have higher priority (numerically lower)
      than the peripheral interrupt. Otherwise the caller ISR process will be blocked.
      To change the HAL time base interrupt priority you have to use HAL_NVIC_SetPriority() function.
      
@note The application needs to ensure that the HAL time base is always set to 1 millisecond
      to have correct HAL operation.

@par Directory contents 

  - BSP/Src/main.c                 Main program
  - BSP/Src/system_stm32g0xx.c     STM32G0xx system clock configuration file
  - BSP/Src/stm32g0xx_it.c         Interrupt handlers 
  - BSP/Src/joystick.c             joystick feature
  - BSP/Src/lcd.c                  LCD drawing features
  - BSP/Src/log.c                  LCD Log firmware functions
  - BSP/Src/sd.c                   SD features
  - BSP/Src/temperature_sensor.c   Temperature Sensor features
  - BSP/Inc/main.h                 Main program header file  
  - BSP/Inc/stm32g0xx_conf.h       HAL Configuration file
  - BSP/Inc/stm32g0xx_it.h         Interrupt handlers header file
  - BSP/Inc/lcd_log_conf.h         lcd_log configuration template file
  - BSP/Inc/stlogo.h               Image used for BSP example

@par Hardware and Software environment

  - This example runs on STM32G081RBTx devices.
    
  - This example has been tested with STMicroelectronics STM32G081B-EVAL board and can be
    easily tailored to any other supported device and development board.

@par How to use it ? 

In order to make the program work, you must do the following :
 - Open your preferred toolchain 
 - Rebuild all files and load your image into target memory
 - Run the example

 * <h3><center>&copy; COPYRIGHT STMicroelectronics</center></h3>
 */

/**
  @page ADC_MultiChannelSingleConversion ADC example

  @verbatim
  ******************************************************************************
  * @file    Examples/ADC/ADC_MultiChannelSingleConversion/readme.txt 
  * @author  MCD Application Team
  * @brief   Description of the ADC_MultiChannelSingleConversion example.
  ******************************************************************************
   * Copyright (c) 2018 STMicroelectronics. All rights reserved.
  *
  * This software component is licensed by ST under BSD 3-Clause license,
  * the "License"; You may not use this file except in compliance with the
  * License. You may obtain a copy of the License at:
  *                       opensource.org/licenses/BSD-3-Clause 
  *
  ******************************************************************************
  @endverbatim
  ----------------------以上是3C开源协议-----------------
  
例程描述：
这个例程提供了一份关于如何使用不同BSP驱动的描述。
主程序的开始HAL_Init()函数被调用来初始化所有外围器件，启动FLASH接口和系统定时器（systick）。
然后SystemClock_Config()函数被用来配置系统时钟（SYSCLK）频率运行至56MHz

这个例程演示了通过按下Tamper按键切换至所有测试程序来展示板上可用器件的不同机能。

按下Tamper按键开始测试。
蓝色LED（LD4）将在每个测试期间闪烁，按下Tamper开始另一个测试：

操纵杆：
使用操纵杆按钮使光标在矩形内移动（上下左右）并改变光标颜色（选择）（整体按下）。

LCD：
这个例程展示了如何使用LCD的不同特性显示不同字体的字符串，显示不同的形状，绘制位图。

SD：
这个例程展示了如何擦除、写入、读取SD卡并如何检测SD卡的的存在性。
	
温度传感器：
这个例程展示了如何使用温度传感器读取温度。
Tsensor实际存在于子板MB1351上。
请确认MB1351已安装至评估板。

LCD日志：
这个例程展示了如何使用LCD日志特性。

注意：
	谨慎使用HAL_Delay()函数，其提供了基于HAL时基ISR的增变量的精确延时（毫秒级）。这意味着HAL_Delay()被调用为一个外部ISR进程，那么HAL时基中断必须相较外部中断拥有更高优先级（较小数字）。否则这个ISR调用进程将被阻塞。
	你必须用HAL_NVIC_SetPriority()函数来改变HAL时基中断优先级。
	
	这个程序需要确保HAL时基总是被设置1毫秒来产生正确的操作。	
必要连接：无					

目录内容：
  - BSP/Src/main.c                 主程序
  - BSP/Src/system_stm32g0xx.c     STM32G0xx系统源文件（配置时钟）
  - BSP/Src/stm32g0xx_it.c         中断处理程序
  - BSP/Src/joystick.c             操纵杆功能
  - BSP/Src/lcd.c                  LCD绘图功能
  - BSP/Src/log.c                  LCD日志固件函数
  - BSP/Src/sd.c                   SD功能
  - BSP/Src/temperature_sensor.c   温度传感器功能
  - BSP/Inc/main.h                 main.c 头文件模块  
  - BSP/Inc/stm32g0xx_conf.h       HAL配置文件
  - BSP/Inc/stm32g0xx_it.h         中断处理程序头文件
  - BSP/Inc/lcd_log_conf.h         LCD日志配置模板文件
  - BSP/Inc/stlogo.h               用于BSP例程的图片
软硬件环境：
	-这个例程运行在STM32G081xx系列器件上
	-这个例程已经在STM32G081B-EVAL开发板上经过测试，可以轻松地裁剪至其他支持的硬件或者开发板上
	
如何使用？
	为了让程序运行，你必须按如下操作：
	-打开常用的工具链（toolchain）
	-重编译所有文件并在目标内存中加载
	-运行实例
 * <h3><center>&copy; COPYRIGHT STMicroelectronics</center></h3>
 */
	
