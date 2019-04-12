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

@par Example Description
Use ADC to convert a several channels using sequencer in discontinuous mode, 
conversion data are transferred by DMA into an array, indefinitely (circular mode).

Example configuration:
ADC is configured to convert a three channels (one external analog, 2 internals),
in sequence conversion mode, one by one from SW trigger.
DMA is configured to transfer conversion data in an array, in circular mode.

Example execution:
From the start, the ADC converts the selected channels in sequence, one by one
(discontinuous mode) at each trig from Tamper push-button click.
DMA transfers conversion data to the array, DMA transfer complete interruption occurs.
Results array is updated indefinitely (DMA in circular mode).
LED1 is turned on when the DMA transfer is completed (results array full)
and turned off at next DMA half-transfer (result array first half updated).
Note: If DMA buffer is full when user click on Tamper push-button, the buffer is reset
(to ease user observe behavior).

For debug: variables to monitor with debugger watch window:
 - "aADCxConvertedData": ADC group regular conversion data (array of data)

Connection needed:
None.
Note: Optionally, a voltage can be supplied to the analog input pin (cf pin below),
      between 0V and Vdda=3.3V, to perform a ADC conversion on a determined
      voltage level.
      Otherwise, this pin can be let floating (in this case ADC conversion data
      will be undetermined).

Other peripherals used:
  1 GPIO for LED
  1 GPIO for analog input: PA4 ( connector CN10 pin 6)
  1 GPIO for push button
  DMA

Board settings:
 - ADC is configured to convert one external channel ADC_CHANNEL_4
   ( connector CN10 pin 6) and the two internal ones ADC_CHANNEL_VREFINT,
   ADC_CHANNEL_TEMPSENSOR.
 - The voltage input on the ADC external channel can be provided by an external source
   connected to  connector CN10 pin 6.



STM32G081B-EVAL board LED is be used to monitor the program execution status:
 - Normal operation: LED1 is turned-on/off in function of ADC conversion
   result.
    - Toggling: "On" upon conversion completion (full DMA buffer filled)
                "Off" upon half conversion completion (half DMA buffer filled)
 - Error: In case of error, LED1 is toggling twice at a frequency of 1Hz.

@par Keywords

Analog, ADC, Analog to Digital, Single conversion, Multi channel, Software trigger

@par Directory contents 

  - ADC/ADC_MultiChannelSingleConversion/Inc/stm32g0xx_it.h          Interrupt handlers header file
  - ADC/ADC_MultiChannelSingleConversion/Inc/main.h                        Header for main.c module  
  - ADC/ADC_MultiChannelSingleConversion/Src/stm32g0xx_it.c          Interrupt handlers
  - ADC/ADC_MultiChannelSingleConversion/Src/stm32g0xx_hal_msp.c     HAL MSP module
  - ADC/ADC_MultiChannelSingleConversion/Src/main.c                        Main program
  - ADC/ADC_MultiChannelSingleConversion/Src/system_stm32g0xx.c      STM32G0xx system source file


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
	在非持续模式下通过定序器用ADC转换几个通道，转换数据通过DMA总线持续地传送至一个数组，（循环模式）。
	
	配置实例：
	ADC被配置成按序转换模式，通过SW按键触发依次转换三个通道（一个外部模拟，两个内部）
	DMA被配置成循环模式向数组内传送转换数据。
	
运行实例：
	开始，ADC在每次按键单击下按顺序转换所选通道（非持续模式），DMA将转换数据传送至数组，转换完成后产生中断。
	结果数组被无限更新（DMA工作在循环模式）。
	当DMA传送完成时，LED1点亮（结果数组存满），并且在下一个DMA缓冲区传送一半（结果数组更新了一半）时熄灭。
	注意：当用户单击Tamper按键时，如果DMA缓冲区满则将被重置（方便用户观察）。
	
对于调试：
		观察窗下的监控变量：
		“aADCxConvertedData”：ADC定期编组的转换数据（数据数组）
	
必要连接：无
	注意：可在模拟输入脚（下面的cf脚）提供0-3V的任意电压，在确定的电压下执行ADC转换。
		也可以使该脚悬空（在这种情况下ADC转换数据将不确定）
	
	其他使用到的外围器件：
	一个对应LED的GPIO
	一个对应模拟输入的GPIO（CN10插座的PIN_6）
	一个对应按键的GPIO
	DMA总线
	
开发板设置：
		-ADC被配置成转换一个外部通道ADC_CHANNEL_4（CN10插座的PIN_6）和两个内部通道ADC_CHANNEL_VREFINT,ADC_CHANNEL_TEMPSENSOR.
		-外部通道的电压输入可以通过外部电源连接到CN10插座pin_6.

STM32G081B-EVAL开发板的LED被用来监控程序运行状态：
	-标准操作：LED1闪烁对应ADC采样结果
		-关联：转换完成时亮（DMA缓冲区满）；转换至一半时灭（缓冲区填充至一半）。
	-报错：故障状态下，LED1	在1Hz的频率下切换两次（2Hz）

关键字：ADC，模数转换，单转换，多通道，软件触发

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
	