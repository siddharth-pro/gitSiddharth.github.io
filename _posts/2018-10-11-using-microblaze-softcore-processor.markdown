---
layout: post
title: "Using Microblaze softcore processor"
date: "2018-10-11"
---

Xilinx provides its own softcore processor IP Microblaze to use in embedded systems application. In this post and a few that follow up, I will implement the Microblaze softcore processor on Spartan 3E FPGA. After that's done I will use Xilinx provided SDK(Software Development Kit) to write a C program to turn on LEDs using switches.

I found [this](http://www.techcounsellor.com/2017/06/putting-microblaze-processor-papilio-one/) article which explains the whole step involved in setting up Microblaze on Papilio one FPGA board. It gives an example of blinking LED program to demonstrate the working. But the program below shows the use of switches to turn on LEDs.


```c
/***************************** Include Files *********************************/
#include <stdio.h>
#include "xparameters.h"
#include "xgpio.h"
#include "platform.h"

/************************** Variable Defintions ******************************/
XGpio Gpio_leds;  //Gpio_leds is user defined variable
XGpio Gpio_keys;  //Also same as above

int main()
{
	 int Status;
	 int i;
	 u32 Delay;
	 u32 DataRead;

	 init_platform();

	 Status = XGpio_Initialize(&Gpio_keys, XPAR_DIP_SWITCHES_DEVICE_ID);
	 if (Status != XST_SUCCESS) {
		  return XST_FAILURE;
	 }

	 XGpio_SetDataDirection(&Gpio_keys, 1, 0xFFFFFFFF);    //set Gpio_keys is input

	 Status = XGpio_Initialize(&Gpio_leds, XPAR_LEDS_DEVICE_ID);
	 if (Status != XST_SUCCESS) {
		  return XST_FAILURE;
	 }

	 XGpio_SetDataDirection(&Gpio_leds, 1, 0x0);         //set Gpio_leds is output

 while(1)
  {
	 DataRead = XGpio_DiscreteRead(&Gpio_keys, 1);

	 if((DataRead & 0x0f)!=0x0f){                      //if key is pushed
		for (Delay = 0; Delay < 2000; Delay++);
		DataRead = XGpio_DiscreteRead(&Gpio_keys, 1);  //read again
	 	if((DataRead & 0x0f)!=0x0f)
	 	{
 	 	      XGpio_DiscreteWrite(&Gpio_leds, 1, DataRead);
	 	}
	 }
	 else{                                             //if key is not pushed
			for (Delay = 0; Delay < 2000; Delay++);
			DataRead = XGpio_DiscreteRead(&Gpio_keys, 1);  //read again
		 	if((DataRead & 0x0f)==0x0f)
		 	{
	 	 	      XGpio_DiscreteWrite(&Gpio_leds, 1, DataRead);
		 	}
	 }
  }
    return 0;
}

 ``` 

