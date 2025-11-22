# Reporte-3-Pantalla-LCD
## Introduccion
### En esta practica se trato de usar la tarjeta de adquisicion de datos ´´´Esp 22´´´  junto con el sensor antes usado ´´´ DHT-11´´´  pero esta vez se incorporrar una pantala LCD (Liquid crystal display) para poder revisar los datos de temperatura y humedad que arroja el sensor pero para poder vizulizarlo de forma fisica y no necesariamente por el monitor serial.
## Materiales y equipo a utilizar
- Tarjeta ´´´ Esp 22´´´
- Sensor de temperatura DHT11
- Plataforma Wokwi
- Tarjeta LCD 16X2

## Procedimiento
### 1. Entrar y abrir la plataforma Wokwi donde seleccionaremos la siguiente tarjeta de adquisicion ´´´ ESP 22´´´
![](https://github.com/raul7ops-sketch/Reporte-3-Pantalla-LCD/blob/main/Reporte%201%20esp%2022.png?raw=true)
### 2. Una vez ahi agregaremos las librerias correspondientes para el funcionamiento de nuestra practica:
- DHT sensor library for ESPx
- LiquidCrystal I2C
![](https://github.com/raul7ops-sketch/Reporte-3-Pantalla-LCD/blob/main/Imagen%20de%20librerias%20reporte%203.png?raw=true)
### 3. Seleccionamos el sensor ´´´DHT-11´´´ y el ´´´Liquid Crystal Display IC2´´´ y lo conectamos de la siguiente manera:
![](https://github.com/raul7ops-sketch/Reporte-3-Pantalla-LCD/blob/main/Conexion%20del%20reporte%203.png?raw=true)
### 4. Copiamos el siguiente codigo y lo pegamos en Wokwi:
´´´#include "DHTesp.h"
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

const int DHT_PIN = 15;

DHTesp dhtSensor;

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {

  Serial.begin(115200);
  dhtSensor.setup(DHT_PIN, DHTesp::DHT22);
  lcd.init();
  lcd.backlight();

}

void loop() {

  TempAndHumidity  data = dhtSensor.getTempAndHumidity();
  Serial.println("Temp: " + String(data.temperature, 1) + "°C");
  Serial.println("Humidity: " + String(data.humidity, 1) + "%");
  Serial.println("---");
  
  lcd.setCursor(0, 0);
  lcd.print("  Temp: " + String(data.temperature, 1) + "\xDF"+"C  ");
  lcd.setCursor(0, 1);
  lcd.print(" Humidity: " + String(data.humidity, 1) + "% ");
  lcd.print("Wokwi Online IoT");

  delay(1000);
  lcd.clear();
  lcd.setCursor(2, 0);
  lcd.print("Bienvenidos");
  lcd.setCursor(2, 1);
  lcd.print("al curso");
  delay(1000);
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Raul Aguilar L.");
  lcd.setCursor(0, 1);
  lcd.print("Ing. Mecanico");
  delay(1000);
}´´´

Donde en este codigo hace que en la pantalla LCD muestre los valores de temperatura y humedad ademas de que se le agrego un para oraciones como "Bienvenidos al curso" y "Raul Aguilar L. Ing. Mecanico"
### 5. Damos al boton de correr simulacion
