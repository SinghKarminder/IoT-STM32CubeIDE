#Blink LED Project on NUCLEO-L476RG Development Kit through STM32CubeIDE

The project demonstrates how to use the STM32CubeIDE tool to configure peripherals, develop,and produce your beginning projects using initialization C code and HAL libraries using the STM32CubeIDE tool.

The latest version of the STM32CubeIDE installer can be downloaded from the STMicroelectronics website at www.st.com.
Or https://www.st.com/en/development-tools/stm32cubeide.html

The official documentation regarding STM32CubeIDE is:  
https://www.st.com/resource/en/user_manual/dm00629856-stm32cubeide-user-guide-stmicroelectronics.pdf

##Tips for Running

1. Configure NUCLEO-L476RG Board as in folder LED_Blinky.ioc

2. Save the project

3. Make changes in main.c file. Use HAL library fuctions.

          //CODE FOR LED BLINK
	  //HAL_GPIO_TogglePin (GPIOA, GPIO_PIN_5); //Toggle Pin PA5 to blink LED2
	  //HAL_Delay (500);   /* Insert delay 500 ms */

4. Complete code given in Core>Src>main.c

5. Save the project and Debug the project

6. Run the project

7. Output: LED2 blink after every 500 ms

Refer video: https://www.youtube.com/watch?v=hyZS2p1tW-g
 