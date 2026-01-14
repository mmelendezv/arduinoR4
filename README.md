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
El primer punto con la tarjeta es instalar el software el IDE de Arduino, se recomienda usar una versión reciente. Al momento es tiene la version 2.3.7 (considerando una instalacion de Windows):, pero se puede instalar otra version que sea reciente.

<img width="863" height="582" alt="AcercaDe" src="https://github.com/user-attachments/assets/ab6ff512-6a90-4902-9a30-5873e09a9a49" />


Aqui esta la version actual de Arduino...
https://www.arduino.cc/en/software

Una vez instalado el software, hay que configurar dos puntos importantes; la placa, en este la placa Arduino UNO R4 WiFi y el puerto conectado en la PC como se muestran en las imagenes.
<img width="954" height="584" alt="boardR4" src="https://github.com/user-attachments/assets/67fcb500-4443-41da-9292-bc6d15f82d3f" />
<img width="948" height="583" alt="PuertoR4" src="https://github.com/user-attachments/assets/2f6de195-a4ea-4b75-a365-3ccc469463d6" />

Posteriormente sera necesario instalar las librerias correspondientes a los elementos a usar. En este ejemplo solo se requiere la placa R4 que cuenta con una patalla de matrix de LED (hay que instalar la libreria "Arduino_LED_Matrix.h")
```
/* Ejemplo con pantalla de matrix de LED
#include "Arduino_LED_Matrix.h"

#define MAX_Y 8
#define MAX_X 12

void displayGrid();

uint8_t grid[MAX_Y][MAX_X] = {
    {0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0}, 
    {0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0}, 
    {0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0}, 
    {0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0},
    {0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0}, 
    {0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0},
};

ArduinoLEDMatrix matrix;

#define   DELAY         3
#define   MAX_POINTS    1
#define   BLOCK_ROWS    3

struct point_t {
    double x, y, dx, dy;

    point_t() :
        x(0.0), y(0.0), dx(0.0), dy(0.0) {}

    point_t(int _x, int _y, int _dx, int _dy) : 
        x(_x), y(_y), dx(_dx), dy(_dy) {}

    point_t(double _x, double _y, double _dx, double _dy) :
        x(_x), y(_y), dx(_dx), dy(_dy) {}

    void set() {
        grid[(int) y][(int) x] = 1;
    }

    void reset() {
        grid[(int) y][(int) x] = 0;
    }

    void update(point_t *blocks, int &num_blocks) {
        int ox = 0;
        int oy = 0;
        int pdx = static_cast<int>(x + dx);
        int mdx = static_cast<int>(x - dx);
        int pdy = static_cast<int>(y + dy);
        int mdy = static_cast<int>(y - dy);
        int i = 0;

        for (i=0; i < num_blocks; i++) {
            ox = static_cast<int>(blocks[i].x);
            oy = static_cast<int>(blocks[i].y);

            if ((pdx == ox || mdx == ox) && (pdy == oy || mdy == oy)) {
                break;
            }
        }

        if (i < num_blocks) {
            // we hit a block
            dx *= -1.0;
            dy *= -1.0;

            grid[(int) oy][(int) ox] = 0;
            blocks[i] = blocks[num_blocks - 1];
            num_blocks--;
        }
        else {
            if (pdx < 0 || mdx < 0 || pdx >= MAX_X || mdx >= MAX_X) 
            { dx *= -1.0; }
            if (pdy < 0 || mdy < 0 || pdy >= MAX_Y || mdy >= MAX_Y) 
            { dy *= -1.0; }
        }

        x += dx;
        y += dy;
    }
};

point_t points[MAX_POINTS];
int num_blocks = BLOCK_ROWS * 12;
point_t blocks[BLOCK_ROWS * 12];
uint32_t start = 0;

void reset_blocks() {
    for (int y = 0; y < BLOCK_ROWS; y++) {
        for (int x = 0; x < 12; x++) {
            blocks[y * MAX_X + x].x = x;
            blocks[y * MAX_X + x].y = y + 1;
        }
    }
    num_blocks = BLOCK_ROWS * 12;
    start = millis();
}

void reset_ball() {
    int const min_num = 2;
    int const max_num = 6;

    auto lambda = []() -> double { 
        return (1.0 / (double) random(min_num, max_num)); 
    };

    for (point_t &pt : points) {
        pt.x = random(0, MAX_X);
        pt.y = random(0, MAX_Y);
        pt.dx = random(2) ? -lambda() : +lambda();
        pt.dy = random(2) ? -lambda() : +lambda();
    }
}

void setup() {
    delay(1000);
    Serial.begin(115200);
    delay(1000);
    
    Serial.println("Arduino LED Matrix");
    matrix.begin();

    pinMode(A0, INPUT);
    randomSeed(analogRead(A0));

    reset_ball();
    reset_blocks();
}

void loop() {
    for (int i = 0; i < num_blocks; i++) {
        blocks[i].set();
    }

    for (point_t &pt : points) { pt.set(); }
    displayGrid();

    delay(DELAY);

    for (point_t &pt : points) { pt.reset(); }
    displayGrid();

    for (point_t &pt : points) { pt.update(blocks, num_blocks); }

    if (0 == num_blocks || millis() - start >= 60000LU) {
        reset_ball();
        reset_blocks();
    }
}

void leftEye() {
	//Left eye
	frame[1][3] = 1;
	frame[1][4] = 1;
	frame[2][3] = 1;
	frame[2][4] = 1;
}

void wink() {
	//Wink with the left eye
	frame[1][3] = 0;
	frame[1][4] = 0;
	frame[2][3] = 1;
	frame[2][4] = 1;
}

void rightEye() {
	//Right eye
	frame[1][8] = 1;
	frame[1][9] = 1;
	frame[2][8] = 1;
	frame[2][9] = 1;
}

void mouth() {
	//Mouth
	frame[5][3] = 1;
	frame[5][9] = 1;
	frame[6][3] = 1;
	frame[6][4] = 1;
	frame[6][5] = 1;
	frame[6][6] = 1;
	frame[6][7] = 1;
	frame[6][8] = 1;
	frame[6][9] = 1;
}

void loop() {
	leftEye();
	rightEye();
	mouth();

	matrix.renderBitmap(frame, 8, 12);

	delay(1000);
	wink();

	matrix.renderBitmap(frame, 8, 12);
	delay(1000);
}
```
![20260113_102048](https://github.com/user-attachments/assets/4eaa8a6b-9b0a-4d61-8be4-b9e54e70ca12)


Enlaces utiles:

https://docs.arduino.cc/hardware/uno-r4-wifi/ 

https://github.com/arduino/uno-r4-library-compatibility

https://docs.arduino.cc/tutorials/uno-r4-wifi/cheat-sheet/

https://docs.arduino.cc/tutorials/uno-r4-wifi/led-matrix/
