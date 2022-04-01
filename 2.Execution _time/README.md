# Print Execution timer of timer Project on serial terminal on NUCLEO-L476RG Development Kit through STM32CubeIDE

In this demo, we will be using an STM32 Nucleo-L476RG, which has a default main clock (HCLK) of 80 MHz. We could have a timer tick at 80 MHz, but that might be too fast for many of our applications. A 16-bit timer can count to 65,535 before rolling over, which means we can measure events no longer than about 819 microseconds.
If we wish to measure longer events, we need to use a prescaler, which is a piece of hardware that divides the clock source. For example, a prescaler of 80 would turn an 80 MHz clock into a 1 MHz clock.
Now, our timer would tick once every 1 microsecond and, assuming a 16-bit timer, be able to time events up to a maximum of about 65.5 milliseconds.

The latest version of the STM32CubeIDE installer can be downloaded from the STMicroelectronics website at www.st.com.
Or https://www.st.com/en/development-tools/stm32cubeide.html

The official documentation regarding STM32CubeIDE is:  
https://www.st.com/resource/en/user_manual/dm00629856-stm32cubeide-user-guide-stmicroelectronics.pdf

## Tips for Running

1. Configure NUCLEO-L476RG Board as in folder Execution_time.ioc

2. Save the project

3. Make changes in main.c file. Use HAL library fuctions.


        //CODE FOR PRINTING ELASPED TIME
        
        /* USER CODE BEGIN 1 */
        char uart_buf[50];
        int uart_buf_len;
        uint16_t timer_val;        
        /* USER CODE END 1 
        
        /* USER CODE BEGIN 2 */        
        // Say something
        uart_buf_len = sprintf(uart_buf, "Timer Test\r\n");
        HAL_UART_Transmit(&huart2, (uint8_t *)uart_buf, uart_buf_len, 100);
        
        // Start timer
        HAL_TIM_Base_Start(&htim16);
        /* USER CODE END 2 */
        
        while (1)
        {
        //Defining variables size and type
        char uart_buf[50];
        int uart_buf_len;
        uint16_t timer_val;
        
        // Get current time (microseconds)
        timer_val = __HAL_TIM_GET_COUNTER(&htim16);
        
        // Wait for 50 ms
        HAL_GPIO_WritePin(GPIOA, GPIO_PIN_5, GPIO_PIN_SET);
        HAL_Delay(50);
        HAL_GPIO_WritePin(GPIOA, GPIO_PIN_5, GPIO_PIN_RESET);
        
        // Get time elapsed
        timer_val = __HAL_TIM_GET_COUNTER(&htim16) - timer_val;
        
        // Show elapsed time
        uart_buf_len = sprintf(uart_buf, "%u us\r\n", timer_val);
        HAL_UART_Transmit(&huart2, (uint8_t *)uart_buf, uart_buf_len, 100);
        
        // Wait again so we don't flood the Serial terminal
        HAL_Delay(1000);
        /* USER CODE END WHILE */

        
4. Complete code given in directory Core>Src>main.c

5. Save the project and Debug the project

6. Run the project

7. Output: Elasped time being printed on the serial terminal

Refer video: https://www.youtube.com/watch?v=VfbW6nfG4kw
 
