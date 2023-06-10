# Practica ESP32 con sensor ultrasónico de distancia y LCD
En este repositorio se muestra a continuación una práctica utilizando la página Wokwi para la simulación del sensor ultrasónico de distancia con LCD de 16x2.

## Introducción

### Descripción

Se recrea una simulación de un sensor ultrasónico de distancia utilizando una tarjeta ```ESP32```, donde los datos recopilados se muestran en una LCD. En esta práctica se usara un simulador llamado [WOKWI](https://wokwi.com/).


## Material Necesario

Para realizar esta práctica se ocuparon las siguientes herramientas y componentes:

- [SIMULADOR WOKWI](https://wokwi.com/)
- Tarjeta ESP32
- Sensor ultrasónico de distancia
- LCD 16x2 (I2C)



## Instrucciones

### Requisitos previos

Para poder usar este repositorio necesitas entrar a la plataforma [WOKWI](https://wokwi.com/).


### Instrucciones de preparación de entorno 

1. Al ingresar a la página de [WOKWI](https://wokwi.com/) se selecciona la tarjeta ESP32, se agrega el sensor ultrasónico de distancia y una LCD de 16x2 (I2C).

2. Una vez seleccionado la tarjeta ```Esp32```, en la parte izquierda se encuentra la pestaña de código donde se agrega lo siguiente:

```
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

const int Trigger = 13;   //Pin digital 2 para el Trigger del sensor
const int Echo = 12;   //Pin digital 3 para el Echo del sensor

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {
  Serial.begin(9600);//iniciailzamos la comunicación
  pinMode(Trigger, OUTPUT); //pin como salida
  pinMode(Echo, INPUT);  //pin como entrada
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0
  lcd.init();
  lcd.backlight();
}

void loop()
{
  long t; //timepo que demora en llegar el eco
  long d; //distancia en centimetros

  digitalWrite(Trigger, HIGH);
  delayMicroseconds(10);          //Enviamos un pulso de 10us
  digitalWrite(Trigger, LOW);
  
  t = pulseIn(Echo, HIGH); //obtenemos el ancho del pulso
  d = t/59;             //escalamos el tiempo a una distancia en cm
  
  Serial.print("Distancia: ");
  Serial.print(d);      //Enviamos serialmente el valor de la distancia
  Serial.print("cm");
  Serial.println();
  delay(1000);          //Hacemos una pausa de 100ms

  lcd.setCursor(0,0);
  lcd.print(" Diplomado AIyM ");
  lcd.setCursor(0,1);
  lcd.print(" Michelle C. G. ");
  delay(1000);

  lcd.setCursor(0,0);
  lcd.print("Distancia:      ");
  lcd.setCursor(0,1);
  lcd.print(String(d) + "  cm         ");
  delay(3000);

}

```
3. En dado caso que se muestre un error con la libería, en la pestaña **Library Manager** se instala la librería de **LiquidCrystal I2C** como se muestra en la siguiente imagen.

![](https://github.com/Michellecg/ESP32_con_sensor_ultrasonico/blob/main/Lib_Ult_LCD.PNG)

4. Hacer la conexión del **sensor ultrasónico de distancia** y **LCD 16x2 (I2C)** con la tarjeta **ESP32** como se muestra en la siguente imagen.

![](https://github.com/Michellecg/ESP32_con_sensor_ultrasonico/blob/main/Conex_Ult_LCD.PNG)

### Instrucciónes de operación

1. Iniciar simulador.
2. Visualizar los datos en el monitor serial.
3. Modificar la distancia dando *doble click* al sensor **ultrasónico de distancia**
4. Añadir un mensaje al inicio de recolección de datos en la LCD. 

## Resultados

Una vez compilado el programa y que no se hayan presentado errores, se podrán observar los datos del sensor en la LCD tal como se muestra en la siguente imagen.

![](https://github.com/Michellecg/ESP32_con_sensor_ultrasonico/blob/main/Res_Ult_LCD.PNG)

![](https://github.com/Michellecg/ESP32_con_sensor_ultrasonico/blob/main/Res_Ult_LCD2.PNG)



# Créditos

Desarrollado por Michelle Cuatlapantzi González

- [GitHub](https://github.com/Michellecg/)