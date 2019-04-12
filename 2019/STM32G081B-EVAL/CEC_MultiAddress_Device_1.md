/**
  @page CEC CEC_MultiAddress_Device_1 example
  
  @verbatim
  ******************************************************************************
  * @file    CEC/CEC_MultiAddress_Device_1/readme.txt 
  * @author  MCD Application Team
  * @brief   Description of the CEC Multiple Address communication example.
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

This example shows how to configure and use the CEC peripheral to receive and 
transmit messages in the case where one device supports two distinct logical
addresses at the same time.


- Hardware Description

To use this example, two STM32G081B-EVAL boards (called Device_1 and 
Device_2) are loaded with the matching software then connected through CEC lines
PB10 and GND.


@verbatim
Development board = STM32G081B-EVAL 
*------------------------------------------------------------------------------*
|         Device Address :0x01                    Device Address :0x03         |
|                                                 Device Address :0x05         |
|         ____________________                   ____________________          |
|        |                    |                 |                    |         |
|        |                    |                 |                    |         | 
|        |     __________     |                 |     __________     |         |
|        |    |   CEC    |____|____CECLine______|____|   CEC    |    |         |
|        |    | Device_1 |    |                 |    | Device_2 |    |         |
|        |    |__________|    |                 |    |__________|    |         |
|        |                    |                 |                    |         |
|        |  O LD1             |                 |  O LD1             |         |
|        |  O LD2    Joystick |                 |  O LD2    Joystick |         |
|        |  O LD3        _    |                 |  O LD3        _    |         |
|        |  O LD4       |_|   |                 |  O LD4       |_|   |         |
|        |                    |                 |                    |         |
|        |             GND O--|-----------------|--O GND             |         |
|        |____________________|                 |____________________|         |
|                                                                              |
|                                                                              |
*------------------------------------------------------------------------------*
@endverbatim


- Software Description

The test unrolls as follows.

On Device_1 TX side, three possible messages can be transmitted and are 
indicated as below on the transmitting board:
 - when Tamper push-button is pressed, a ping message (no payload) is addressed
  to Device_2 first logical address; LED1 toggles
 - when Joystick DOWN push-button is pressed, a ping message (no payload) is addressed
  to Device_2 second logical address; LED4 toggles  
 - when Joystick Selection push-button is pressed, a broadcast message (with empty
 payload) is sent by Device_1; LED2 toggles
 
When Joystick UP push-button is pressed, LED3 toggles (no message sent)  


Accordingly, the following happens on Device_2 RX side in case of successful
reception:
 - when Tamper push-button is pressed on TX side, 
     * LED1 is turned on
     * LED3 and LED4 are turned off 
 - when Joystick DOWN push-button is pressed on TX side, 
     * LED4 is turned on
     * LED1 and LED3 are turned off      
 - when Joystick Selection push-button is pressed on TX side, all LEDs are turned off 


Conversely, on Device_2 TX side, only ping messages addressed to the 
single Device_1 logical address or broadcast messages are sent:
 - when Tamper push-button is pressed, a ping message (no payload) is addressed
  to Device_1; LED1 toggles
 - when Joystick DOWN push-button is pressed, a ping message (no payload) is addressed
  to Device_1; LED4 toggles  
 - when Joystick Selection push-button is pressed, a broadcast message (with empty
 payload) is sent; LED2 toggles


Accordingly, the following happens on Device_1 RX side in case of successful
transmission:
 - when Tamper or Joystick DOWN push-button are pressed on TX side, 
      * LED1 and LED4 are turned on
      * LED3 is turned off     
 - when Joystick Selection push-button is pressed on TX side, all LEDs are turned off 


For Device_1 and _2, in case of transmission or reception error, 
LED3 is turned on.


Practically, 2 EXTI lines (EXTI_Line0_1 and EXTI_Line2_3) are configured to 
generate an interrupt on each falling or rising edge. 
A specific message is then transmitted by the CEC IP
and a LED connected to a specific GPIO pin is toggled.
    - EXTI_Line0_1 is mapped to PA.00
    - EXTI_Line2_3 is mapped to PC.13, PC.02 and PC.03 

Then, on TX side,
  - when rising edge is detected on EXTI_Line0_1, LED2 toggles
  - when falling edge is detected on EXTI_Line4_15 and EXTI line interrupt is detected
    on PC.13, LED1 toggles
  - when falling edge is detected on EXTI_Line2_3 and EXTI line interrupt is detected
    on PC.02, LED3 toggles
  - when falling edge is detected on EXTI_Line2_3 and EXTI line interrupt is detected
    on PC.03, LED4 toggles

In this example, HCLK is configured at 56 MHz.

@par Keywords

Connectivity, CEC, Transmission, Reception, joystick, Data exchange

@par Directory contents 

  - CEC/CEC_MultiAddress_Device_1/Inc/stm32g0xx_hal_conf.h    HAL configuration file
  - CEC/CEC_MultiAddress_Device_1/Inc/stm32g0xx_it.h          Interrupt handlers header file
  - CEC/CEC_MultiAddress_Device_1/Inc/main.h                  Header for main.c module  
  - CEC/CEC_MultiAddress_Device_1/Src/stm32g0xx_it.c          Interrupt handlers
  - CEC/CEC_MultiAddress_Device_1/Src/system_stm32g0xx.c      STM32G0xx system source file
  - CEC/CEC_MultiAddress_Device_1/Src/main.c                  Main program
  - CEC/CEC_MultiAddress_Device_1/Src/stm32g0xx_hal_msp.c     IP hardware resources initialization
  
@par Hardware and Software environment

  - This example runs on STM32G081RBTx Devices.
    
  - This example has been tested with STM32G081B-EVAL board and can be
    easily tailored to any other supported device and development board.      


@par How to use it ? 

In order to make the program work, you must do the following :
 - Open your preferred toolchain 
 - Rebuild all files (CEC_DataExchange_Device_1 project) and load your image into target memory
    o Load the project in Device_1 Board
 - Rebuild all files (CEC_DataExchange_Device_2 project) and load your image into target memory
    o Load the project in Device_2 Board
 - Be aware that PB10 pin is missing but PB10 is connected directly to it (SB23 is closed).
 - With a wire, connect PB10-PB10 between the 2 boards
 - Add a pull-up resistor of 27kohm between PB10 and V3.3
 - Connect the ground of the 2 boards
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
这个例程展示如何配置并使用外部CEC在一个设备同时支持两个不同逻辑地址收发报文的情形
	
	-硬件描述
	为了使用这个例程，两个STM32G081B-EVAL评估板（device_1/device_2）被装载匹配软件然后通过CEC线（PB10或者HDMI连接器）连接。
*------------------------------------------------------------------------------*
|         Device Address :0x01                    Device Address :0x03         |
|                                                 Device Address :0x05         |
|         ____________________                   ____________________          |
|        |                    |                 |                    |         |
|        |                    |                 |                    |         | 
|        |     __________     |                 |     __________     |         |
|        |    |   CEC    |____|____CECLine______|____|   CEC    |    |         |
|        |    | Device_1 |    |                 |    | Device_2 |    |         |
|        |    |__________|    |                 |    |__________|    |         |
|        |                    |                 |                    |         |
|        |  O LD1             |                 |  O LD1             |         |
|        |  O LD2    Joystick |                 |  O LD2    Joystick |         |
|        |  O LD3        _    |                 |  O LD3        _    |         |
|        |  O LD4       |_|   |                 |  O LD4       |_|   |         |
|        |                    |                 |                    |         |
|        |             GND O--|-----------------|--O GND             |         |
|        |____________________|                 |____________________|         |
|                                                                              |
|                                                                              |
*------------------------------------------------------------------------------*
	-软件描述
	测试展开如下
	1板TX端，下列三个可用报文可以被传送并显示：
		-当按下tamper时，一个ping报文（无内容）被发送到2板第一逻辑地址；LED1闪烁
		-当操纵杆下方向按下时，一个ping报文（无内容）被发送到2板第二逻辑地址；LED4闪烁
		-当操纵杆选择键按下时，一个广播消息（空内容）通过1板发送；LED2闪烁
		-当操纵杆上方向按下时，LED3闪烁（无消息发出）
		
	因此，下列结果表明2板RX端接收成功：
	1板按下tamper：LED1亮；LED3和LED4都灭
	1板操纵杆下方向按下时：LED4亮，LED1和LED3都灭
	1板当操纵杆选择键按下时：所有灯均灭
	
	反过来，在2板TX端，只有发送到1板逻辑地址的PING消息和广播报文才会发送：
		-当按下tamper时，ping报文（无内容）发送至1板；LED1闪烁
		-当操纵杆下方向按下时，ping报文（无内容）发送至1板；LED4闪烁
		-当操纵杆选择键按下时，一个广播消息（空内容）被发送；LED2闪烁
		
	因此，下列结果表明1板RX端接收成功：
		-当按下tamper或者操纵杆下方向按下时，LED1和LED4点亮，LED3熄灭
		-当操纵杆选择键按下时，所有LED都熄灭
	
	对于1、2板，传输与接收出错时，LED3点亮
	
	事实上，2个EXTI线（EXTI_Line0_1 and EXTI_Line2_3）被配置成在每个上升沿和下降沿产生中断。
	随后一个特定的信息通过CEC的IP传送出来，与特定的GPIO连接的LED将会闪烁。
		-EXTI_Line0_1被映射至PA.00
		-EXTI_Line2_3被映射至PC.13, PC.02 and PC.03 
	
	那么在TX端，
		-当上升沿被EXTI_Line0_1检测到之后，LED2闪烁
		-当下降沿被EXTI_Line4_15检测到且EXTI线中断被PC.13检测到，LED1闪烁
		-当下降沿被EXTI_Line2_3检测到且EXTI线中断被PC.02检测到，LED3闪烁
		-当下降沿被EXTI_Line2_3检测到且EXTI线中断被PC.03检测到，LED4闪烁

	在这个实例中，HCLK被配置为56MHz。

关键字：连通性，CEC，传送，接收，控制杆，数据交换

目录内容：
  - CEC/CEC_MultiAddress_Device_1/Inc/stm32g0xx_hal_conf.h    HAL 配置文件
  - CEC/CEC_MultiAddress_Device_1/Inc/stm32g0xx_it.h          中断处理程序头文件
  - CEC/CEC_MultiAddress_Device_1/Inc/main.h                  主程序头文件 
  - CEC/CEC_MultiAddress_Device_1/Src/stm32g0xx_it.c          中断处理程序
  - CEC/CEC_MultiAddress_Device_1/Src/system_stm32g0xx.c      STM32G0xx系统源文件（配置时钟）
  - CEC/CEC_MultiAddress_Device_1/Src/main.c                  主程序
  - CEC/CEC_MultiAddress_Device_1/Src/stm32g0xx_hal_msp.c     IP硬件资源初始化

软硬件环境：
	-这个例程运行在STM32G081xx系列器件上
	-这个例程已经在STM32G081B-EVAL开发板上经过测试，可以轻松地裁剪至其他支持的硬件或者开发板上
	
如何使用？
	为了让程序运行，你必须按如下操作：
	-打开常用的工具链（toolchain）
	-重编译所有文件(CEC_DataExchange_Device_1 project、CEC_DataExchange_Device_2 project)并在目标内存中加载
	-留意PB10管脚消失但是被直接接在上面（SB23关闭了）
	-用线连接三个板子的PB10
	-在V3.3与PB10之间增加一个27k上拉电阻
	-三个板子共地连接
	-运行实例
 * <h3><center>&copy; COPYRIGHT STMicroelectronics</center></h3>
 */
	