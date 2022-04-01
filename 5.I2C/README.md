# I2C Measurement of temperature Project on NUCLEO-L476RG Development Kit through STM32CubeIDE using STTS751 Sensor

The project demonstrates how to use the STM32CubeIDE tool to configure peripherals, develop,and produce your beginning projects using initialization C code and HAL libraries using the STM32CubeIDE tool tto measure temperature from STTS751 Sensor.
Inter-Integrated Circuit (I2C) is a communication bus protocol developed by Philips Semiconductor (now NXP Semiconductors) in 1982. It is a relatively slow protocol but has seen widespread use due to its simplicity and robustness. Most microcontrollers have at least 1 I2C peripheral controller built in to the silicon.

If you would like to learn more about the I2C protocol, this tutorial from SparkFun is recommended (https://learn.sparkfun.com/tutorials/i2c/all).

By looking at the STTS751 datasheet (https://www.st.com/resource/en/datasheet/stts751.pdf), we can determine that retrieving temperature data from the temperature register would require a set of I2C write/read commands as follows in the code section.

The latest version of the STM32CubeIDE installer can be downloaded from the STMicroelectronics website at www.st.com.
Or https://www.st.com/en/development-tools/stm32cubeide.html

The official documentation regarding STM32CubeIDE is:  
https://www.st.com/resource/en/user_manual/dm00629856-stm32cubeide-user-guide-stmicroelectronics.pdf


## Tips for Running

1. Configure NUCLEO-L476RG Board as in folder I2C.ioc

2. Save the project

3. Make changes in main.c file. Use HAL library fuctions.


        //CODE FOR LED BLINK
        /* USER CODE BEGIN Includes */
        #include <string.h>
        #include <stdio.h>
        /* USER CODE END Includes */
        
        /* USER CODE BEGIN PV */
        static const uint8_t STTS751_ADDR = 0x48 << 1; // Use 8-bit address
        static const uint8_t REG_TEMP = 0x00;
        /* USER CODE END PV */
        
        /* USER CODE BEGIN 1 */
        HAL_StatusTypeDef ret;
        uint8_t buf[12];
        int16_t val;
        float temp_c;
        /* USER CODE END 1 */
        
        /* USER CODE BEGIN WHILE */
        while (1)
        {
        // Tell STTS751 that we want to read from the temperature register
        buf[0] = REG_TEMP;
        ret = HAL_I2C_Master_Transmit(&hi2c1, STTS751_ADDR, buf, 1, HAL_MAX_DELAY);
        if ( ret != HAL_OK ) {
        strcpy((char*)buf, "Error Tx\r\n");
        } else {
        
        // Read 2 bytes from the temperature register
        ret = HAL_I2C_Master_Receive(&hi2c1, STTS751_ADDR, buf, 2, HAL_MAX_DELAY);
        if ( ret != HAL_OK ) {
        strcpy((char*)buf, "Error Rx\r\n");
        } else {
        
        //Combine the bytes
        val = ((int16_t)buf[0] << 4) | (buf[1] >> 4);
        
        // Convert to 2's complement, since temperature can be negative
        if ( val > 0x7FF ) {
        val |= 0xF000;
        }
        
        // Convert to float temperature value (Celsius)
        temp_c = val * 0.0625;
        
        // Convert temperature to decimal format
        temp_c *= 100;
        sprintf((char*)buf,
        "%u.%02u C\r\n",
        ((unsigned int)temp_c / 100),
        ((unsigned int)temp_c % 100));
        }
        }
        
        // Send out buffer (temperature or error message)
        HAL_UART_Transmit(&huart2, buf, strlen((char*)buf), HAL_MAX_DELAY);
        
        // Wait
        HAL_Delay(500);
        /* USER CODE END WHILE */
        
4. Complete code given in directory Core>Src>main.c

5. Save the project and Debug the project

6. Run the project

7. Output: Temperature in Celsius being displayed on serial terminal

Refer video: https://www.youtube.com/watch?v=isOekyygpR8
 
