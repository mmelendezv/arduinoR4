# Tarjeta Arduino R4 con Wifi
![arduino r4](https://github.com/user-attachments/assets/d39a095f-f1df-4fdc-9f00-d9669de79b78)

La placa Arduino Uno R4 WiFi es la última incorporación a la familia Arduino, ofreciendo un conjunto de características avanzadas mientras mantiene la robustez y versatilidad que esperas. Esta placa trae un aumento significativo en la potencia de procesamiento gracias a su microcontrolador Arm® Cortex®-M4 de 32 bits.

Esta nueva versión de Arduino Uno R4 ofrece características notables que no existían en las versiones posteriores a las versiones precedentes, incluyendo conectividad Wi-Fi y Bluetooth BLE  en la misma placa gracias a un módulo ESP32-S3 integrado (anteriormente teníamos dos módulos extras), abriendo un abanico de posibilidades para proyectos IoT y comunicación remota. . Otra funcionalidad nueva, aunque pareciera solo algo estético, una matriz LED de 12x8 para visualizaciones graficas de manera amigable. Un conector Qwiic facilitar la conexión de sensores I2C y soporte para alimentación de hasta 24V, además de compatibilidad con el estándar HID para actuar como teclado o ratón;  con ello, se tiene una expansión y características destacadas del Arduino Uno R4 WiFi.

Características
Matriz LED (la versión con Wifi):
Una matriz de 12x8 LEDs rojos integrados facilita la creación de interfaces visuales y la visualización de datos de sensores sin necesidad de componentes externos adicionales. 
Conector Qwiic:
El conector I2C Qwiic permite la conexión rápida y sencilla de sensores, pantallas y otros módulos I2C sin necesidad de soldar, simplificando el proceso de expansión. 
Amplio rango de voltaje:
El Uno R4 WiFi soporta voltajes de entrada de hasta 24V, lo que lo hace adecuado para entornos industriales o proyectos que requieran mayor potencia. 
Compatibilidad con HID:
La placa puede emular un ratón o teclado USB, lo que permite interactuar con computadoras de manera sencilla. 
Diagnóstico de errores:
Cuenta con un mecanismo de detección de errores en tiempo real que ayuda a identificar y solucionar problemas en el código. 
Memoria y velocidad:
El microcontrolador principal, Renesas RA4M1, ofrece una velocidad de reloj de 48 MHz y 256 kB de memoria flash y 32 kB de SRAM, mientras que el ESP32-S3 tiene 384 kB de ROM y 512 kB de SRAM. 
Compatibilidad con shields:
La placa es compatible con los shields diseñados para el Arduino Uno R3, lo que facilita la migración de proyectos existentes. 
Nuevo conector USB-C:
El puerto USB-C reemplaza el antiguo USB tipo B, ofreciendo una conexión más moderna y resistente. 

# Capitulo 1. Inicio en Arduino R4.
El primer punto con la tarjeta es instalar el software el IDE de Arduino, se recomienda usar una vesion reciente. Al momento es tiene la version 2.3.6:
<img width="863" height="582" alt="AcercaDe" src="https://github.com/user-attachments/assets/ab6ff512-6a90-4902-9a30-5873e09a9a49" />


Enlaces utiles:

https://docs.arduino.cc/hardware/uno-r4-wifi/ 

https://github.com/arduino/uno-r4-library-compatibility

https://docs.arduino.cc/tutorials/uno-r4-wifi/cheat-sheet/

https://docs.arduino.cc/tutorials/uno-r4-wifi/led-matrix/
