ICM20689 DMP Driver
===

# update: Too many people ask me for the source code... I'm usualy more physical and the source code is released directly.

Invensense new generation gyroscope ICM20689 has only one online driver, the official ICM20789 version on the G55 board demo, but its very complex and difficult to use, I based on this version to delete and modify out a convenient driver code on the STM32.

## Platform parameters

Chip ： STM32F405RGT6  
IDE :  Keil  
ST lib ： HAL  

## File introduction

* **Porting file**:It is the gyroscope driver file on STM32, you only need 3 files in it to port to your own project.
* **icm20689 ported version demo**: is a ported demo, you can refer to this demo to configure spi parameters and program structure.  

[Here I have wrapped the dmp configuration related code inside the lib, if you need the original version please contact me by email.](adayimaxiga@hotmail.com)

## Notes on use
 
The only functions that really need the user's attention are the following :   

| Function | Function  | Attention |
| :------------ |:---------------:| :-----|
|  `icm20689_dmp_setup()`  | Initialize DMP (including gyroscope) | The function calls HAL_Delay internally, so it needs to be placed after the SPI and system clock |
|  `get_dmp_data()`   |Get the attitude angle solved by DMP, 0 means success, 1 means failure  |  This function (DMP updates the attitude angle frequency to 200Hz, so there is a failure when reading too fast.) |
|  `MPU_Get_Accelerometer(short *ax,short *ay,short *az)` | Obtain acceleration information        |   Note the units, using DMP mode initialization, the range must be +/- 4g |
| `MPU_Get_Gyroscope(short *gx,short *gy,short *gz)` | Obtain angular velocity        |   Note the units, using DMP mode initialization, the range must be +/- 2000dps |
