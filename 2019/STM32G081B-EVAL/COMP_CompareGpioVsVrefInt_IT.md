/**
  @page COMP_CompareGpioVsVrefInt_IT COMP example
  
  @verbatim
  ******************************************************************************
  * @file    Examples/COMP/COMP_CompareGpioVsVrefInt_IT/readme.txt
  * @author  MCD Application Team
  * @brief   Description of the COMP_CompareGpioVsVrefInt_IT Example.
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

How to configure the COMP peripheral to compare the external
voltage applied on a specific pin with the Internal Voltage Reference. 

When the comparator input crosses (either rising or falling edges) the internal 
reference voltage VREFINT (1.22V), the comparator generates an interrupt
and exit from STOP mode.

The System enters STOP mode 5 seconds after the comparator is started and 
after any system wake-up triggered by the comparator interrupt.

In this example, the comparator input is connected on the pin PA1 (connected on pin 1 on CN4) 
the user shall apply a voltage on and each time the comparator input crosses VREFINT, LED1 toggles.
If LED1 is toggling continuously without any voltage update, it indicates that the system 
generated an error.

@note Care must be taken when using HAL_Delay(), this function provides 
      accurate delay (in milliseconds) based on variable incremented in SysTick ISR. 
      This implies that if HAL_Delay() is called from a peripheral ISR process, then 
      the SysTick interrupt must have higher priority (numerically lower) than the 
      peripheral interrupt. Otherwise the caller ISR process will be blocked. 
      To change the SysTick interrupt priority you have to use HAL_NVIC_SetPriority() function.
      
@note The application need to ensure that the SysTick time base is always set 
      to 1 millisecond to have correct HAL operation.

@par Keywords

comparator, stop mode, voltage compare, wakeup trigger, comparator interrupt.

@par Directory contents 

  - COMP/COMP_CompareGpioVsVrefInt_IT/Inc/stm32g0xx_hal_conf.h    HAL configuration file
  - COMP/COMP_CompareGpioVsVrefInt_IT/Inc/stm32g0xx_it.h          COMP interrupt handlers header file
  - COMP/COMP_CompareGpioVsVrefInt_IT/Inc/main.h                  Header for main.c module
  - COMP/COMP_CompareGpioVsVrefInt_IT/Src/stm32g0xx_it.c          COMP interrupt handlers
  - COMP/COMP_CompareGpioVsVrefInt_IT/Src/main.c                  Main program
  - COMP/COMP_CompareGpioVsVrefInt_IT/Src/stm32g0xx_hal_msp.c     HAL MSP file 
  - COMP/COMP_CompareGpioVsVrefInt_IT/Src/system_stm32g0xx.c      STM32G0xx system source file


@par Hardware and Software environment 

  - This example runs on STM32G081RBTx devices.

  - This example has been tested with STM32G081B-EVAL board and can be
    easily tailored to any other supported device and development board.

  - Apply an external variable voltage on PA1 (connected on pin 1 on CN4) with average voltage 1.22V.
    
    
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
展示如何配置外围比较器比较内部参考电压与外部特定管脚电压

当比较器输入（不管上升还是下降沿）经过参考电压比较（1.22V）,比较器产生中断并退出STOP模式。

在比较器开始运作并且通过任何比较器中断触发的系统唤醒之后系统进入STOP模式5秒。

在这个实例中，比较器输入被连接到PA1脚（CN4插座的pin_1），用户应施加电压在每次比较器输入经过VREFINT比较后，LED1闪烁。
如果LED1在没有输入电压更新的情况下不断闪烁，意味着系统产生错误。

注意：
	谨慎使用HAL_Delay()函数，其提供了基于HAL时基ISR的增变量的精确延时（毫秒级）。这意味着HAL_Delay()被调用为一个外部ISR进程，那么HAL时基中断必须相较外部中断拥有更高优先级（较小数字）。否则这个ISR调用进程将被阻塞。
	你必须用HAL_NVIC_SetPriority()函数来改变HAL时基中断优先级。
	
	这个程序需要确保HAL时基总是被设置1毫秒来产生正确的操作。	
	
关键字：比较器，停止模式，电压比较，唤醒触发，比较器中断

目录内容：
  - COMP/COMP_CompareGpioVsVrefInt_IT/Inc/stm32g0xx_hal_conf.h    HAL 配置文件
  - COMP/COMP_CompareGpioVsVrefInt_IT/Inc/stm32g0xx_it.h          比较器中断处理程序头文件
  - COMP/COMP_CompareGpioVsVrefInt_IT/Inc/main.h                  main.c 头文件模块  
  - COMP/COMP_CompareGpioVsVrefInt_IT/Src/stm32g0xx_it.c          中断处理程序
  - COMP/COMP_CompareGpioVsVrefInt_IT/Src/main.c                  主程序
  - COMP/COMP_CompareGpioVsVrefInt_IT/Src/stm32g0xx_hal_msp.c     IP硬件资源初始化
  - COMP/COMP_CompareGpioVsVrefInt_IT/Src/system_stm32g0xx.c      STM32G0xx系统源文件
软硬件环境：
	-这个例程运行在STM32G081xx系列器件上
	-这个例程已经在STM32G081B-EVAL开发板上经过测试，可以轻松地裁剪至其他支持的硬件或者开发板上
	-在PA1（CN4插座pin_1）施加一个外部可变的平均值为1.22V的电压
如何使用？
	为了让程序运行，你必须按如下操作：
	-打开常用的工具链（toolchain）
	-重编译所有文件并在目标内存中加载
	-运行实例
 * <h3><center>&copy; COPYRIGHT STMicroelectronics</center></h3>
 */
	