# On/Off LED Project using Push Button on NUCLEO-L476RG Development Kit through STM32CubeIDE

There are two push buttons in NUCLEO-L476RG one is User (PA13) and other is Reset. In NUCLEO-L476RG Push Button will be connected to ground when it is pressed. When the push Button is pressed it will be in the Reset state. Thus, in the project we will toggle the LED when the push button is pressed.

The latest version of the STM32CubeIDE installer can be downloaded from the STMicroelectronics website at www.st.com.
Or https://www.st.com/en/development-tools/stm32cubeide.html

The official documentation regarding STM32CubeIDE is:  
https://www.st.com/resource/en/user_manual/dm00629856-stm32cubeide-user-guide-stmicroelectronics.pdf

## Tips for Running

1. Configure NUCLEO-L476RG Board as in folder Push_Button.ioc

2. Save the project

3. Make changes in main.c file. Use HAL library fuctions.
![HAL_Function_LED_Blink](https://github.com/SinghKarminder/IoT-STM32CubeIDE/blob/main/0.Blink-LED/Images/101.png)
![Push_Button_Algorithm](

        //CODE FOR PUSH BUTTON
       if(HAL_GPIO_ReadPin(GPIOC,GPIO_PIN_13)==GPIO_PIN_RESET) //Reading Input Button PA13
        {
        HAL_GPIO_TogglePin(GPIOA,GPIO_PIN_5); //Toggle LED when input is reset
        HAL_Delay(300); // Add some delay
	}

4. Complete code given in directory Core>Src>main.c

5. Save the project and Debug the project

6. Run the project

7. Output: LED2 will be toggled when button PA13 will be pressed


 
