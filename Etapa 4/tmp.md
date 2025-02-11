# main.c

```c
/* USER CODE BEGIN Header */
/**
  ******************************************************************************
  * @file           : main.c
  * @brief          : Main program body
  ******************************************************************************
  * @attention
  *
  * Copyright (c) 2025 STMicroelectronics.
  * All rights reserved.
  *
  * This software is licensed under terms that can be found in the LICENSE file
  * in the root directory of this software component.
  * If no LICENSE file comes with this software, it is provided AS-IS.
  *
  ******************************************************************************
  */
/* USER CODE END Header */
/* Includes ------------------------------------------------------------------*/
#include "main.h"

/* Private includes ----------------------------------------------------------*/
/* USER CODE BEGIN Includes */

/* USER CODE END Includes */

/* Private typedef -----------------------------------------------------------*/
/* USER CODE BEGIN PTD */

/* USER CODE END PTD */

/* Private define ------------------------------------------------------------*/
/* USER CODE BEGIN PD */

/* USER CODE END PD */

/* Private macro -------------------------------------------------------------*/
/* USER CODE BEGIN PM */

/* USER CODE END PM */

/* Private variables ---------------------------------------------------------*/
ADC_HandleTypeDef hadc;

TIM_HandleTypeDef htim1;
TIM_HandleTypeDef htim3;
DMA_HandleTypeDef hdma_tim1_ch3_up;
DMA_HandleTypeDef hdma_tim3_ch1_trig;

UART_HandleTypeDef huart1;

/* USER CODE BEGIN PV */
uint8_t	rx_buffer[2] = {0};
/* USER CODE END PV */

/* Private function prototypes -----------------------------------------------*/
void SystemClock_Config(void);
static void MX_GPIO_Init(void);
static void MX_DMA_Init(void);
static void MX_TIM1_Init(void);
static void MX_USART1_UART_Init(void);
static void MX_ADC_Init(void);
static void MX_TIM3_Init(void);
/* USER CODE BEGIN PFP */

/* USER CODE END PFP */

/* Private user code ---------------------------------------------------------*/
/* USER CODE BEGIN 0 */

/* USER CODE END 0 */

/**
  * @brief  The application entry point.
  * @retval int
  */
int main(void)
{

  /* USER CODE BEGIN 1 */

  /* USER CODE END 1 */

  /* MCU Configuration--------------------------------------------------------*/

  /* Reset of all peripherals, Initializes the Flash interface and the Systick. */
  HAL_Init();

  /* USER CODE BEGIN Init */

  /* USER CODE END Init */

  /* Configure the system clock */
  SystemClock_Config();

  /* USER CODE BEGIN SysInit */

  /* USER CODE END SysInit */

  /* Initialize all configured peripherals */
  MX_GPIO_Init();
  MX_DMA_Init();
  MX_TIM1_Init();
  MX_USART1_UART_Init();
  MX_ADC_Init();
  MX_TIM3_Init();
  /* USER CODE BEGIN 2 */
  HAL_TIM_Base_Start_IT(&htim1);
  HAL_TIM_Base_Start(&htim3);
  HAL_UART_Receive_IT(&huart1, rx_buffer, 2);
  HAL_TIM_PWM_Start(&htim1, TIM_CHANNEL_3);
  TIM1->CCR3 = (TIM1->ARR);

  EVSE_Parametros params = {
		  .corrente = 16,
		  .canal_timer_led = TIM_CHANNEL_1,
		  .timer_pwm = &htim1,
		  .timer_led = &htim3
  };
  /* USER CODE END 2 */

  /* Infinite loop */
  /* USER CODE BEGIN WHILE */
  while (1)
  {
	EVSE_ExecutarEstado(&params);
	HAL_Delay(100);

    /* USER CODE END WHILE */

    /* USER CODE BEGIN 3 */
  }
  /* USER CODE END 3 */
}

/**
  * @brief System Clock Configuration
  * @retval None
  */
void SystemClock_Config(void)
{
  RCC_OscInitTypeDef RCC_OscInitStruct = {0};
  RCC_ClkInitTypeDef RCC_ClkInitStruct = {0};
  RCC_PeriphCLKInitTypeDef PeriphClkInit = {0};

  /** Initializes the RCC Oscillators according to the specified parameters
  * in the RCC_OscInitTypeDef structure.
  */
  RCC_OscInitStruct.OscillatorType = RCC_OSCILLATORTYPE_HSI|RCC_OSCILLATORTYPE_HSI14;
  RCC_OscInitStruct.HSIState = RCC_HSI_ON;
  RCC_OscInitStruct.HSI14State = RCC_HSI14_ON;
  RCC_OscInitStruct.HSICalibrationValue = RCC_HSICALIBRATION_DEFAULT;
  RCC_OscInitStruct.HSI14CalibrationValue = 16;
  RCC_OscInitStruct.PLL.PLLState = RCC_PLL_ON;
  RCC_OscInitStruct.PLL.PLLSource = RCC_PLLSOURCE_HSI;
  RCC_OscInitStruct.PLL.PLLMUL = RCC_PLL_MUL12;
  RCC_OscInitStruct.PLL.PREDIV = RCC_PREDIV_DIV1;
  if (HAL_RCC_OscConfig(&RCC_OscInitStruct) != HAL_OK)
  {
    Error_Handler();
  }

  /** Initializes the CPU, AHB and APB buses clocks
  */
  RCC_ClkInitStruct.ClockType = RCC_CLOCKTYPE_HCLK|RCC_CLOCKTYPE_SYSCLK
                              |RCC_CLOCKTYPE_PCLK1;
  RCC_ClkInitStruct.SYSCLKSource = RCC_SYSCLKSOURCE_PLLCLK;
  RCC_ClkInitStruct.AHBCLKDivider = RCC_SYSCLK_DIV1;
  RCC_ClkInitStruct.APB1CLKDivider = RCC_HCLK_DIV1;

  if (HAL_RCC_ClockConfig(&RCC_ClkInitStruct, FLASH_LATENCY_1) != HAL_OK)
  {
    Error_Handler();
  }
  PeriphClkInit.PeriphClockSelection = RCC_PERIPHCLK_USART1;
  PeriphClkInit.Usart1ClockSelection = RCC_USART1CLKSOURCE_PCLK1;
  if (HAL_RCCEx_PeriphCLKConfig(&PeriphClkInit) != HAL_OK)
  {
    Error_Handler();
  }
}

/**
  * @brief TIM1 Initialization Function
  * @param None
  * @retval None
  */
static void MX_TIM1_Init(void)
{

  /* USER CODE BEGIN TIM1_Init 0 */

  /* USER CODE END TIM1_Init 0 */

  TIM_ClockConfigTypeDef sClockSourceConfig = {0};
  TIM_MasterConfigTypeDef sMasterConfig = {0};
  TIM_OC_InitTypeDef sConfigOC = {0};
  TIM_BreakDeadTimeConfigTypeDef sBreakDeadTimeConfig = {0};

  /* USER CODE BEGIN TIM1_Init 1 */

  /* USER CODE END TIM1_Init 1 */
  htim1.Instance = TIM1;
  htim1.Init.Prescaler = 48-1;
  htim1.Init.CounterMode = TIM_COUNTERMODE_UP;
  htim1.Init.Period = 1000-1;
  htim1.Init.ClockDivision = TIM_CLOCKDIVISION_DIV1;
  htim1.Init.RepetitionCounter = 0;
  htim1.Init.AutoReloadPreload = TIM_AUTORELOAD_PRELOAD_DISABLE;
  if (HAL_TIM_Base_Init(&htim1) != HAL_OK)
  {
    Error_Handler();
  }
  sClockSourceConfig.ClockSource = TIM_CLOCKSOURCE_INTERNAL;
  if (HAL_TIM_ConfigClockSource(&htim1, &sClockSourceConfig) != HAL_OK)
  {
    Error_Handler();
  }
  if (HAL_TIM_PWM_Init(&htim1) != HAL_OK)
  {
    Error_Handler();
  }
  sMasterConfig.MasterOutputTrigger = TIM_TRGO_RESET;
  sMasterConfig.MasterSlaveMode = TIM_MASTERSLAVEMODE_DISABLE;
  if (HAL_TIMEx_MasterConfigSynchronization(&htim1, &sMasterConfig) != HAL_OK)
  {
    Error_Handler();
  }
  sConfigOC.OCMode = TIM_OCMODE_PWM1;
  sConfigOC.Pulse = 0;
  sConfigOC.OCPolarity = TIM_OCPOLARITY_HIGH;
  sConfigOC.OCNPolarity = TIM_OCNPOLARITY_HIGH;
  sConfigOC.OCFastMode = TIM_OCFAST_DISABLE;
  sConfigOC.OCIdleState = TIM_OCIDLESTATE_RESET;
  sConfigOC.OCNIdleState = TIM_OCNIDLESTATE_RESET;
  if (HAL_TIM_PWM_ConfigChannel(&htim1, &sConfigOC, TIM_CHANNEL_3) != HAL_OK)
  {
    Error_Handler();
  }
  sBreakDeadTimeConfig.OffStateRunMode = TIM_OSSR_DISABLE;
  sBreakDeadTimeConfig.OffStateIDLEMode = TIM_OSSI_DISABLE;
  sBreakDeadTimeConfig.LockLevel = TIM_LOCKLEVEL_OFF;
  sBreakDeadTimeConfig.DeadTime = 0;
  sBreakDeadTimeConfig.BreakState = TIM_BREAK_DISABLE;
  sBreakDeadTimeConfig.BreakPolarity = TIM_BREAKPOLARITY_HIGH;
  sBreakDeadTimeConfig.AutomaticOutput = TIM_AUTOMATICOUTPUT_DISABLE;
  if (HAL_TIMEx_ConfigBreakDeadTime(&htim1, &sBreakDeadTimeConfig) != HAL_OK)
  {
    Error_Handler();
  }
  /* USER CODE BEGIN TIM1_Init 2 */

  /* USER CODE END TIM1_Init 2 */
  HAL_TIM_MspPostInit(&htim1);

}

/**
  * @brief TIM3 Initialization Function
  * @param None
  * @retval None
  */
static void MX_TIM3_Init(void)
{

  /* USER CODE BEGIN TIM3_Init 0 */

  /* USER CODE END TIM3_Init 0 */

  TIM_ClockConfigTypeDef sClockSourceConfig = {0};
  TIM_MasterConfigTypeDef sMasterConfig = {0};
  TIM_OC_InitTypeDef sConfigOC = {0};

  /* USER CODE BEGIN TIM3_Init 1 */

  /* USER CODE END TIM3_Init 1 */
  htim3.Instance = TIM3;
  htim3.Init.Prescaler = 0;
  htim3.Init.CounterMode = TIM_COUNTERMODE_UP;
  htim3.Init.Period = 60-1;
  htim3.Init.ClockDivision = TIM_CLOCKDIVISION_DIV1;
  htim3.Init.AutoReloadPreload = TIM_AUTORELOAD_PRELOAD_DISABLE;
  if (HAL_TIM_Base_Init(&htim3) != HAL_OK)
  {
    Error_Handler();
  }
  sClockSourceConfig.ClockSource = TIM_CLOCKSOURCE_INTERNAL;
  if (HAL_TIM_ConfigClockSource(&htim3, &sClockSourceConfig) != HAL_OK)
  {
    Error_Handler();
  }
  if (HAL_TIM_PWM_Init(&htim3) != HAL_OK)
  {
    Error_Handler();
  }
  sMasterConfig.MasterOutputTrigger = TIM_TRGO_RESET;
  sMasterConfig.MasterSlaveMode = TIM_MASTERSLAVEMODE_DISABLE;
  if (HAL_TIMEx_MasterConfigSynchronization(&htim3, &sMasterConfig) != HAL_OK)
  {
    Error_Handler();
  }
  sConfigOC.OCMode = TIM_OCMODE_PWM1;
  sConfigOC.Pulse = 0;
  sConfigOC.OCPolarity = TIM_OCPOLARITY_HIGH;
  sConfigOC.OCFastMode = TIM_OCFAST_DISABLE;
  if (HAL_TIM_PWM_ConfigChannel(&htim3, &sConfigOC, TIM_CHANNEL_1) != HAL_OK)
  {
    Error_Handler();
  }
  /* USER CODE BEGIN TIM3_Init 2 */

  /* USER CODE END TIM3_Init 2 */
  HAL_TIM_MspPostInit(&htim3);

}

/**
  * @brief USART1 Initialization Function
  * @param None
  * @retval None
  */
static void MX_USART1_UART_Init(void)
{

  /* USER CODE BEGIN USART1_Init 0 */

  /* USER CODE END USART1_Init 0 */

  /* USER CODE BEGIN USART1_Init 1 */

  /* USER CODE END USART1_Init 1 */
  huart1.Instance = USART1;
  huart1.Init.BaudRate = 115200;
  huart1.Init.WordLength = UART_WORDLENGTH_8B;
  huart1.Init.StopBits = UART_STOPBITS_1;
  huart1.Init.Parity = UART_PARITY_NONE;
  huart1.Init.Mode = UART_MODE_TX_RX;
  huart1.Init.HwFlowCtl = UART_HWCONTROL_NONE;
  huart1.Init.OverSampling = UART_OVERSAMPLING_16;
  huart1.Init.OneBitSampling = UART_ONE_BIT_SAMPLE_DISABLE;
  huart1.AdvancedInit.AdvFeatureInit = UART_ADVFEATURE_NO_INIT;
  if (HAL_UART_Init(&huart1) != HAL_OK)
  {
    Error_Handler();
  }
  /* USER CODE BEGIN USART1_Init 2 */

  /* USER CODE END USART1_Init 2 */

}

/**
  * Enable DMA controller clock
  */
static void MX_DMA_Init(void)
{

  /* DMA controller clock enable */
  __HAL_RCC_DMA1_CLK_ENABLE();

  /* DMA interrupt init */
  /* DMA1_Channel4_5_IRQn interrupt configuration */
  HAL_NVIC_SetPriority(DMA1_Channel4_5_IRQn, 1, 0);
  HAL_NVIC_EnableIRQ(DMA1_Channel4_5_IRQn);

}

/**
  * @brief GPIO Initialization Function
  * @param None
  * @retval None
  */
static void MX_GPIO_Init(void)
{
  GPIO_InitTypeDef GPIO_InitStruct = {0};
/* USER CODE BEGIN MX_GPIO_Init_1 */
/* USER CODE END MX_GPIO_Init_1 */

  /* GPIO Ports Clock Enable */
  __HAL_RCC_GPIOF_CLK_ENABLE();
  __HAL_RCC_GPIOA_CLK_ENABLE();
  __HAL_RCC_GPIOB_CLK_ENABLE();

  /*Configure GPIO pin Output Level */
  HAL_GPIO_WritePin(GPIOA, RELAY_Pin|GPIO_PIN_12, GPIO_PIN_RESET);

  /*Configure GPIO pins : RELAY_Pin PA12 */
  GPIO_InitStruct.Pin = RELAY_Pin|GPIO_PIN_12;
  GPIO_InitStruct.Mode = GPIO_MODE_OUTPUT_PP;
  GPIO_InitStruct.Pull = GPIO_NOPULL;
  GPIO_InitStruct.Speed = GPIO_SPEED_FREQ_LOW;
  HAL_GPIO_Init(GPIOA, &GPIO_InitStruct);

/* USER CODE BEGIN MX_GPIO_Init_2 */
/* USER CODE END MX_GPIO_Init_2 */
}

/**
  * @brief This function handles USART2 global interrupt.
  */
void USART2_IRQHandler(void)
{
  /* USER CODE BEGIN USART2_IRQn 0 */

  /* USER CODE END USART2_IRQn 0 */
  HAL_UART_IRQHandler(&huart1);
  /* USER CODE BEGIN USART2_IRQn 1 */

  /* USER CODE END USART2_IRQn 1 */
}

void HAL_UART_RxCpltCallback(UART_HandleTypeDef *huart){
#ifdef debug
	printf("   test rx callback!   " "\r\n");
#endif
	HAL_UART_Receive_IT(&huart1, rx_buffer, 2);
}

void HAL_UART_TxHalfCpltCallback(UART_HandleTypeDef *huart){

}

/* USER CODE END 4 */

/**
  * @brief  This function is executed in case of error occurrence.
  * @retval None
  */
void Error_Handler(void)
{
  /* USER CODE BEGIN Error_Handler_Debug */
  /* User can add his own implementation to report the HAL error return state */
  __disable_irq();
  while (1)
  {
  }
  /* USER CODE END Error_Handler_Debug */
}

#ifdef  USE_FULL_ASSERT
/**
  * @brief  Reports the name of the source file and the source line number
  *         where the assert_param error has occurred.
  * @param  file: pointer to the source file name
  * @param  line: assert_param error line source number
  * @retval None
  */
void assert_failed(uint8_t *file, uint32_t line)
{
  /* USER CODE BEGIN 6 */
  /* User can add his own implementation to report the file name and line number,
     ex: printf("Wrong parameters value: file %s on line %d\r\n", file, line) */
  /* USER CODE END 6 */
}
#endif /* USE_FULL_ASSERT */

```

# EVSE.c

```c
/*
 * EVSE.c
 *
 *  Created on: Jan 23, 2025
 *      Author: Pedro Henrique Harenza
 */
#include "EVSE.h"

estado_t estado_atual = ESTADO_A;
estado_t estado_anterior = ESTADO_B;
uint8_t  carregado_flag = 0;

void (*tabela_estados[])(uint8_t, TIM_HandleTypeDef *, uint8_t) = {estado_a, estado_b, estado_c, estado_e, estado_f};

void EVSE_ExecutarEstado(EVSE_Parametros *params) {
	tabela_estados[estado_atual](params->corrente, params->timer_led, params->canal_timer_led);
}

void estado_a(uint8_t corrente, TIM_HandleTypeDef *htim_led, uint8_t LED_TIM_CHANNEL){
	if(estado_atual != estado_anterior){
		TIM1->CCR3 = (TIM1->ARR);
		HAL_GPIO_WritePin(RELAY_GPIO_Port, RELAY_Pin, 0);
	}
	estado_anterior = estado_atual;
#ifdef debug
	printf(BOLD "ESTADO A" ANSI_RESET "\r\n");
#endif
	setAllLEDsToColor(255, 255, 255);
	WS2812_Send(htim_led, LED_TIM_CHANNEL);
	evse_state_logic_transition();
}

void estado_b(uint8_t corrente, TIM_HandleTypeDef *htim_led, uint8_t LED_TIM_CHANNEL){
	if(estado_atual != estado_anterior){
		TIM1->CCR3 = (TIM1->ARR)*27/100;
		HAL_GPIO_WritePin(RELAY_GPIO_Port, RELAY_Pin, 0);
	}
	estado_anterior = estado_atual;
#ifdef debug
	printf(BOLD YELLOW "ESTADO B" ANSI_RESET "\r\n");
#endif
	if(carregado_flag){
		setAllLEDsToColor(0, 255, 0);
		WS2812_Send(htim_led, LED_TIM_CHANNEL);
	} else {
		setAllLEDsToColor(255, 255, 0);
		WS2812_Send(htim_led, LED_TIM_CHANNEL);
	}
	evse_state_logic_transition();
}

void estado_c(uint8_t corrente, TIM_HandleTypeDef *htim_led, uint8_t LED_TIM_CHANNEL){
	if(estado_atual != estado_anterior){
		TIM1->CCR3 = (TIM1->ARR)*27/100;
		HAL_GPIO_WritePin(RELAY_GPIO_Port, RELAY_Pin, 1);
	}
	estado_anterior = estado_atual;
#ifdef debug
	printf(BOLD GREEN "ESTADO C" ANSI_RESET "\r\n");
#endif

	green_effect(htim_led, LED_TIM_CHANNEL);
	evse_state_logic_transition();
}

void estado_e(uint8_t corrente, TIM_HandleTypeDef *htim_led, uint8_t LED_TIM_CHANNEL){
	if(estado_atual != estado_anterior){
		TIM1->CCR3 = 0;
		HAL_GPIO_WritePin(RELAY_GPIO_Port, RELAY_Pin, 0);
	}
	estado_anterior = estado_atual;
#ifdef debug
	printf(BOLD RED "ESTADO E" ANSI_RESET "\r\n");
#endif
}

void estado_f(uint8_t corrente, TIM_HandleTypeDef *htim_led, uint8_t LED_TIM_CHANNEL){
	if(estado_atual != estado_anterior){
#ifndef debug
		TIM1->CCR3 = 0;
#endif
		HAL_GPIO_WritePin(RELAY_GPIO_Port, RELAY_Pin, 0);
	}
	estado_anterior = estado_atual;
#ifdef debug
	printf(BOLD RED "ESTADO F" ANSI_RESET "\r\n");
#endif
	setAllLEDsToColor(255, 0, 0);
	WS2812_Send(htim_led, LED_TIM_CHANNEL);
#ifdef debug
	evse_state_logic_transition();
#endif
}


void evse_state_logic_transition() {
    int medida = read_pilot(); // Lê o valor do piloto (em mV)
#ifdef debug
    printf("%d""\r\n", medida);
#endif

    switch (estado_atual) {
        case ESTADO_A:
            if (medida >= 3070 && medida <= 3390) { // 3230 ± 160
                // Permanece no ESTADO_A
            } else if (medida >= 2671 && medida <= 2991) { // 2831 ± 160
                estado_atual = ESTADO_B;
            } else if (medida >= 2272 && medida <= 2592) { // 2432 ± 160
                estado_atual = ESTADO_B;
            } else {
                estado_atual = ESTADO_F;
            }
            break;

        case ESTADO_B:
            if (medida >= 2671 && medida <= 2991) { // 2831 ± 160
                // Permanece no ESTADO_B
            } else if (medida >= 3070 && medida <= 3390) { // 3230 ± 160
                estado_atual = ESTADO_A;
                carregado_flag = 0;
            } else if (medida >= 2272 && medida <= 2592) { // 2432 ± 160
                estado_atual = ESTADO_C;
                carregado_flag = 0;
            } else {
                estado_atual = ESTADO_F;
                carregado_flag = 0;
            }
            break;

        case ESTADO_C:
            if (medida >= 2272 && medida <= 2592) { // 2432 ± 160
                // Permanece no ESTADO_C
            } else if (medida >= 3070 && medida <= 3390) { // 3230 ± 160
                estado_atual = ESTADO_A;
            } else if (medida >= 2671 && medida <= 2991) { // 2831 ± 160
                estado_atual = ESTADO_B;
                carregado_flag = 1;
            } else {
            	estado_atual = ESTADO_F;
            }
            break;

        case ESTADO_E:
            if (medida >= 1476 && medida <= 1796) { // 1636 ± 160
                // Permanece no ESTADO_E
            }
            break;

        case ESTADO_F:
#ifdef debug
            if (medida >= 3070 && medida <= 3390) { // 3230 ± 160
                estado_atual = ESTADO_A;
            } else if (medida >= 2671 && medida <= 2991) { // 2831 ± 160
                estado_atual = ESTADO_B;
            } else if (medida >= 2272 && medida <= 2592) { // 2432 ± 160
                estado_atual = ESTADO_C;
            }
#endif
            break;
    }
}


uint16_t read_pilot(){
	uint16_t adc_sample[100] = {0};
	int average = 0;
	int sum = 0;
	int n = 0;
	//HAL_GPIO_WritePin(GPIOA, GPIO_PIN_12, 1);
	for(int i=0; i <= 100; i++){
		adc_sample[i] = (adc_get_value() * 3300)/4095;
		if(adc_sample[i] > 1000){
			sum += adc_sample[i];
			n++;
		}
	}
	//HAL_GPIO_WritePin(GPIOA, GPIO_PIN_12, 0);
	if(n > 0){
		average = sum/n;
	} else {
		average = 0;
	}
	
	return average;
}

```

# WS2812.c

```c
/*
 * WS2812.c
 *
 *  Created on: Jan 24, 2025
 *      Author: Pedro
 */


#include "WS2812.h"

uint16_t LED_Data[NUM_LEDS][4];
uint16_t pwmData[24*NUM_LEDS+52];
uint16_t effStep = 0;

int datasentflag;

void HAL_TIM_PWM_PulseFinishedCallback(TIM_HandleTypeDef *htim){
	HAL_TIM_PWM_Stop_DMA(htim, TIM_CHANNEL_ALL);
	datasentflag = 1;
}

void set_led(uint16_t LEDnum, uint16_t red, uint16_t green, uint16_t blue){
	LED_Data[LEDnum][0] = LEDnum;
	LED_Data[LEDnum][1] = green;
	LED_Data[LEDnum][2] = red;
	LED_Data[LEDnum][3] = blue;
}

void WS2812_Send(TIM_HandleTypeDef *htim, uint8_t TIM_CHANNEL) {
    uint32_t color;
    uint16_t indx = 2;

    pwmData[0] = 0;
    pwmData[1] = 0;

    for (int i = 0; i < NUM_LEDS; i++) {
        color = ((LED_Data[i][1] << 16) | (LED_Data[i][2] << 8) | (LED_Data[i][3]));

        for (int bit = 23; bit >= 0; bit--) {
            pwmData[indx++] = (color & (1 << bit)) ? 34 : 17;
        }
    }

    for (int i = 0; i < 50; i++) {
        pwmData[indx++] = 0;
    }

    HAL_TIM_PWM_Start_DMA(htim, TIM_CHANNEL, (uint32_t *)pwmData, indx);

    while (!datasentflag) {}
    datasentflag = 0;
}

void setAllLEDsToColor(uint16_t red, uint16_t green, uint16_t blue){
	for(int i=0;i < NUM_LEDS; i++){
		set_led(i, red, green, blue);
	}
}

void green_effect(TIM_HandleTypeDef *htim, uint8_t TIM_CHANNEL) {
    static const uint8_t green_values[3] = {255, 255, 15};  // Valores de verde

    uint16_t ind;
    uint8_t color_index;
    uint8_t factor1, factor2;

    for (uint16_t j = 0; j < 9; j++) {
        ind = effStep + j;
        color_index = (ind % 9) / 3;  // Determina o índice da cor (0, 1 ou 2)

        // Calcula os fatores de interpolação (0 a 255, em vez de 0.0 a 1.0)
        factor1 = 255 - ((ind % 3) * 85);  // 85 = 255 / 3
        factor2 = (ind % 3) * 85;

        // Interpolação apenas para o canal verde
        uint8_t green = (green_values[color_index] * factor1 + green_values[(color_index + 1) % 3] * factor2) >> 8;

        // Define a cor do LED (red e blue sempre 0)
        set_led(j, 0, green, 0);
    }

    // Envia os dados para a fita de LED
    WS2812_Send(htim, TIM_CHANNEL);

    // Atualiza o passo do efeito
    if (effStep >= 62) {
        effStep = 0;
    } else {
        effStep++;
    }
}


```

# adc.c

```c
/*
 * adc.c
 *
 *  Created on: Jan 23, 2025
 *      Author: Pedro Henrique Harenza
 */
 #include "adc.h"

ADC_HandleTypeDef hadc;

/**
  * @brief ADC Initialization Function
  * @param None
  * @retval None
  */
static void MX_ADC_Init(void)
{
  ADC_ChannelConfTypeDef sConfig = {0};

  hadc.Instance = ADC1;
  hadc.Init.ClockPrescaler = ADC_CLOCK_ASYNC_DIV1;
  hadc.Init.Resolution = ADC_RESOLUTION_12B;
  hadc.Init.DataAlign = ADC_DATAALIGN_RIGHT;
  hadc.Init.ScanConvMode = ADC_SCAN_DIRECTION_FORWARD;
  hadc.Init.EOCSelection = ADC_EOC_SINGLE_CONV;
  hadc.Init.LowPowerAutoWait = DISABLE;
  hadc.Init.LowPowerAutoPowerOff = DISABLE;
  hadc.Init.ContinuousConvMode = DISABLE;
  hadc.Init.DiscontinuousConvMode = DISABLE;
  hadc.Init.ExternalTrigConv = ADC_SOFTWARE_START;
  hadc.Init.ExternalTrigConvEdge = ADC_EXTERNALTRIGCONVEDGE_NONE;
  hadc.Init.DMAContinuousRequests = DISABLE;
  hadc.Init.Overrun = ADC_OVR_DATA_PRESERVED;
  if (HAL_ADC_Init(&hadc) != HAL_OK)
  {
    Error_Handler();
  }

  /** Configure for the selected ADC regular channel to be converted.
  */
  sConfig.Channel = ADC_CHANNEL_9;
  sConfig.Rank = ADC_RANK_CHANNEL_NUMBER;
  sConfig.SamplingTime = ADC_SAMPLETIME_71CYCLES_5;
  if (HAL_ADC_ConfigChannel(&hadc, &sConfig) != HAL_OK)
  {
    Error_Handler();
  }
}

uint16_t adc_get_value(){
	uint16_t sample;
	HAL_ADC_Start(&hadc);
	HAL_ADC_PollForConversion(&hadc, HAL_MAX_DELAY);
	sample = HAL_ADC_GetValue(&hadc);
	return sample;
}
```
