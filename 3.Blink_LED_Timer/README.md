# Blink LED through Timer 16 Project on NUCLEO-L476RG Development Kit through STM32CubeIDE

A timer (sometimes known as a counter) is a unique piece of hardware found in many microcontrollers. Their purpose is straightforward: they count (up or down, depending on the configuration—for now, we'll assume up). An 8-bit timer, for example, will count from 0 to 255. When a timer reaches its maximum value, most of them will "rollover." As a result, once our 8-bit timer hits 255, it will reset to 0.
Most timers include a range of options that you may use to customize how they work. Other specific function registers in the microcontroller are frequently used to apply these adjustments. You might, for example, set the timer to roll over at 100 instead of counting to the maximum of 255. You may also use the timer to control other hardware or peripherals inside the microcontroller, such as activating a certain pin when the timer rolls over.

Calculation:

![equation](http://latex.codecogs.com/gif.latex?ToggleDelay%3D%5Cfrac%7BTimerCount*Prescaler%7D%7BMCUClock%7D)

Timer Count=10,000
Prescaler=8,000
MCU Clock=80MHz

![equation](http://latex.codecogs.com/gif.latex?ToggleDelay%3D%5Cfrac%7B10,000*8,000%7D%7B80*10^6%7D)

Toggle Delay = 1 sec

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
        uint16_t timer_val;        
        /* USER CODE END 1 
        
        /* USER CODE BEGIN 2 */        
        // Say something
        uart_buf_len = sprintf(uart_buf, "Timer Test\r\n");
        HAL_UART_Transmit(&huart2, (uint8_t *)uart_buf, uart_buf_len, 100);
        
        // Start timer
        HAL_TIM_Base_Start(&htim16);       
        
       // Get current time (microseconds)
       timer_val = __HAL_TIM_GET_COUNTER(&htim16);
       /* USER CODE END 2 */
        
        while (1)
        {
        // If enough time has passed (1 second), toggle LED and get new timestamp
        if (__HAL_TIM_GET_COUNTER(&htim16) - timer_val >= 10000)
        {
        HAL_GPIO_TogglePin(GPIOA, GPIO_PIN_5);
        timer_val = __HAL_TIM_GET_COUNTER(&htim16);
        }
        /* USER CODE END WHILE */

        
4. Complete code given in directory Core>Src>main.c

5. Save the project and Debug the project

6. Run the project

7. Output: LED will blink when the timer roll over i.e. after 1 second

Refer video: https://www.youtube.com/watch?v=VfbW6nfG4kw
 
