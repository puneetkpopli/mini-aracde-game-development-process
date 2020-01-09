# mini-aracde-game-development-process
a mini project of 3rd sem designing game with adafruit LED and arduino game engine code is in LPC1769 
• Pseudo code for game engine
Game.h
#ifndef GAMETASKS_H_
#define GAMETASKS_H_
#include <stdio.h>
#include <stdlib.h>
#include "FreeRTOS.h"
#include "task.h"
#include "KYPD.h"
#include "uart.h"
#include <time.h>
#define sWidth 128
#define sHight 64
#define BuferSize 12
void vGameInit();
void vTaskRunGame(void *pvParameters);
void vTaskSendData(void *pvParameters);
void vbutton(void *pvParameters);
void vstar(void *pvParameters);
Page 2
void vcharacter(void *pvParameters);
void vTaskCollision();
#endif
Game engine
#include "game.h"
go_character *pcharacter = NULL; //Head for the linked list character
go_character *pstar = NULL; //Head for the linked list character
bool gameOver;
xTaskHandle handle = NULL;
uint8_t numstar = 0;
const dimension dimstar =
{
.height = 16,
.width = 16
};
const dimension dimcharacter =
{
.height = 16,
.width = 16
};
xTaskCreate(vLEDTask1, (signed char *) "vTaskLed1",
configMINIMAL_STACK_SIZE, NULL, (tskIDLE_PRIORITY + 1UL),
(xTaskHandle *) NULL);
xTaskCreate(vTaskUART,(signed char *) "CommunicationTask",
configMINIMAL_STACK_SIZE, NULL, (tskIDLE_PRIORITY + 1UL),
(xTaskHandle *) NULL);
Page 3
xTaskCreate(vKeyPadTask,(signed char *) "CommunicationTask",
configMINIMAL_STACK_SIZE, NULL, (tskIDLE_PRIORITY + 1UL),
(xTaskHandle *) NULL);
xTaskCreate(vTaskSendData, (signed char *) "TaskSendData",
configMINIMAL_STACK_SIZE, NULL,(tskIDLE_PRIORITY + 1UL),
(xTaskHandle *) NULL);
xTaskCreate(vcharacter, (signed char *) "PlayerTask",
configMINIMAL_STACK_SIZE, NULL,(tskIDLE_PRIORITY + 1UL),
&pHeadPlayer->handle);
xTaskCreate(vTaskCollision,"Collisions",configMINIMAL_STACK_SIZE,NULL,2,NULL);
//*************************************************************************//
Player tasks still not complete
//**************************************************************************/
vTaskStartScheduler();
}
vTaskDelay(configTICK_RATE_HZ/10);
}
}
Note-
We are still under development process of work with main code for game
By doing this project we are now able to work with RTOS hardware and able understand basic RTOS programming concepts.
Page 4
