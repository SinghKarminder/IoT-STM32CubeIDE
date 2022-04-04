# Print message through UART Project of NUCLEO-L476RG Development Kit through STM32CubeIDE on serial terminal

The project demonstrates how to use the STM32CubeIDE tool to configure peripherals, develop,and produce your beginning projects using initialization C code and HAL libraries using the STM32CubeIDE tool to print message on the serial terminal PuTTY.

The latest version of the STM32CubeIDE installer can be downloaded from the STMicroelectronics website at www.st.com.
Or https://www.st.com/en/development-tools/stm32cubeide.html

The official documentation regarding STM32CubeIDE is:  
https://www.st.com/resource/en/user_manual/dm00629856-stm32cubeide-user-guide-stmicroelectronics.pdf

## Tips for Running

1. Configure NUCLEO-L476RG Board as in folder UART_Print.ioc

2. Save the project

3. Make changes in main.c file. Use HAL library fuctions.


        //CODE FOR LED BLINK
        
        /* USER CODE BEGIN Includes */
        #include <string.h>
        /* USER CODE END Includes */
        
        /* USER CODE BEGIN 1 */
        uint8_t buf[15];
        /* USER CODE END 1 */
        
        while (1)
        {
        //User code for printing message to UART terminal
        strcpy((char*)buf, "Hello World!\r\n");
        HAL_UART_Transmit(&huart2, buf, strlen((char*)buf), HAL_MAX_DELAY);
        HAL_Delay(500);
        /* USER CODE END WHILE */
4. Complete code given in directory Core>Src>main.c

5. Save the project and Debug the project

6. Run the project

7. Output: Message "Hello World" will be being printed to the serial terminal


