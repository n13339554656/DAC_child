/**
  @page ADC_Oversampling ADC example
  
  @verbatim
  ******************************************************************************
  * @file    Examples/ADC/ADC_Oversampling/readme.txt 
  * @author  MCD Application Team
  * @brief   Description of the ADC_Oversampling example.
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

@par Example Description
Use ADC to convert a single channel but using oversampling feature to increase resolution. 

Example configuration:
ADC is configured to convert a single channel, in single conversion mode,
from SW trigger.
Oversampling is configured to perform 128 conversions
with a right shift of 3 before returning a result.

Example execution:
The ADC performs conversions of the selected channel in continuous mode from SW start
trigger.
Then, SW is waiting for conversion to complete. When done, it reads conversion data from
ADC data register, stores it into a variable, and convert it into mVolt in another one?

For debug: variables to monitor with debugger watch window:
 - "uhADCxConvertedData": ADC group regular conversion data
 - "uhADCxConvertedData_Voltage_mVolt": ADC conversion data computation to physical values

Connection needed:
None, if ADC channel and DAC channel are selected on the same GPIO.
Otherwise, connect a wire between DAC channel output and ADC input.

Other peripherals used:
  1 GPIO for LED
  1 GPIO for analog input: PA4 (connector CN10 pin 6)
  DAC
  1 GPIO for DAC channel output PA4 (connector CN10 pin 6)
  1 GPIO for push button

Board settings:
 - ADC is configured to convert ADC_CHANNEL_9 (connector CN10 pin 6).
 - The voltage input on ADC channel is provided from DAC (DAC1_CHANNEL_1).
   ADC input from pin PA4 and DAC ouput to pin PA4:
   If same pin is used no connection is required, it is done internally. Otherwise, user need to connect a wire between connector CN10 pin 6 and connector CN10 pin 6
 - Voltage is increasing at each click on Tamper push-button, from 0 to maximum range in 4 steps.
   Clicks on Tamper push-button follow circular cycles: At clicks counter maximum value reached, counter is set back to 0.


To observe voltage level applied on ADC channel through GPIO, connect a voltmeter on
pin PA4 (connector CN10 pin 6).

STM32G081B-EVAL board LED is be used to monitor the program execution status:
 - Normal operation: LED1 is toggling at each conversion.
 - Error: In case of error, LED1 is toggling twice at a frequency of 1Hz.

@par Keywords

Analog, ADC, Analog to Digital, single conversion , Software trigger, Over sampling.

@par Directory contents 

  - ADC/ADC_Oversampling/Inc/stm32g0xx_it.h          Interrupt handlers header file
  - ADC/ADC_Oversampling/Inc/main.h                        Header for main.c module  
  - ADC/ADC_Oversampling/Src/stm32g0xx_it.c          Interrupt handlers
  - ADC/ADC_Oversampling/Src/main.c                        Main program
  - ADC/ADC_Oversampling/Src/stm32g0xx_hal_msp.c     HAL MSP module
  - ADC/ADC_Oversampling/Src/system_stm32g0xx.c      STM32G0xx system source file


@par Hardware and Software environment

  - This example runs on STM32G081xx devices.
    
  - This example has been tested with STM32G081B-EVAL board and can be
    easily tailored to any other supported device and development board.


@par How to use it ? 

In order to make the program work, you must do the following :
 - Open your preferred toolchain
 - Rebuild all files and load your image into target memory
 - Run the example

 * <h3><center>&copy; COPYRIGHT STMicroelectronics</center></h3>
 */

/**
  @page ADC_Oversampling ADC example
  
  @verbatim
  ******************************************************************************
  * @file    Examples/ADC/ADC_Oversampling/readme.txt 
  * @author  MCD Application Team
  * @brief   Description of the ADC_Oversampling example.
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
  ----------------3c开源协议----------------
  
例程描述：
ADC被配置成一个单通道，但使用过采样特性增加分辨率的模式

运行实例：
软件起始触发，ADC执行所选通道的连续转换。
然后软件等待转换完成。完成后，将从ADC数据寄存器读取转换数据，存至一个变量，并将其转换成毫伏存至另一个变量。

关于调试：
	观察窗下的监控变量：
	 - "uhADCxConvertedData":ADC组定期的转换数据
	 - "uhADCxConvertedData_Voltage_mVolt": ADC转换数据的具体物理数值

必要连接：无
如果ADC采样与DAC输出为同一管脚，则不需要额外连接。

其他使用到的外围器件：
一个对应LED的GPIO
一个对应模拟输入的GPIO（CN10插座的PIN_6）
DAC
一个对应模拟输出的GPIO（CN10插座的PIN_6）
一个对应按键的GPIO

开发板设置：
	-ADC被配置成转换ADC_CHANNEL_9（CN10号插座的pin_6）。
	-ADC的输入电压通过DAC提供（DAC1_CHANNEL_1）。
	ADC从PA4管脚输入，DAC输出至PA4管脚：
		如果使用相同的管脚就不需要其他连接，而直接在其内部完成。否则，你需要手动在CN10插座的pin_6上连线。
	-随着Tamper按钮的按下，电压逐渐上升，从0至最大幅度共4档.
		电压达到最大后切换至0，如此往复。
	为了观察ADC采样通道上的电压，可在PA4（CN10号插座的pin_6）上连接一电压表。

关键字：ADC，模数转换，单转换，软件触发，过采样

目录内容：
- ADC/ADC_MultiChannelSingleConversion/Inc/stm32g0xx_it.h          中断处理程序头文件
  - ADC/ADC_MultiChannelSingleConversion/Inc/main.h                        main.c 头文件模块  
  - ADC/ADC_MultiChannelSingleConversion/Src/stm32g0xx_it.c          中断处理程序
  - ADC/ADC_MultiChannelSingleConversion/Src/stm32g0xx_hal_msp.c     IP 硬件资源初始化
  - ADC/ADC_MultiChannelSingleConversion/Src/main.c                        主程序
  - ADC/ADC_MultiChannelSingleConversion/Src/system_stm32g0xx.c      STM32G0xx系统源文件

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
	

