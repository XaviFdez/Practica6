# Práctica 6: BUSES DE COMUNICACIÓN II (SPI)
## Introducción parte práctica
En la anterior práctica trabajamos con los buses de comunicación, en esta práctica seguiremos trabajando con estos, pero especializándonos en el bus SPI.

La práctica constará de 3 partes 
 - Lectura i escritura de memoria SD
 - Lectura de etiqueta RFID

## EJERCICIO PRÁCTICO 1 - LECTURA/ESCRITURA DE MEMORIA SD
```c++
#include <SPI.h>
#include <SD.h>
File myFile;
void setup()
{
Serial.begin(9600);
Serial.print("Iniciando SD ...");
if (!SD.begin(4)) {
Serial.println("No se pudo inicializar");
return;
}
Serial.println("inicializacion exitosa");
myFile = SD.open("archivo.txt");
if (myFile) {
Serial.println("archivo.txt:");
while (myFile.available()) {
Serial.write(myFile.read());
}
myFile.close(); //cerramos el archivo
} else {
Serial.println("Error al abrir el archivo");
}
}
void loop()
{
}
```
### Funcionamiento del código
En este código inicializa una targeta de SD, despues abre un archivo ("archivo.txt"), una vez abierto, se lee el archivo y se envía lo que contiene por el puerto serie, y finalmente cierra el archivo.

#### Funcionalidades del código:
- ##### * Función: void setup():*
   Este subprograma configura la comunicación serial, se intenta inicializar la tarjeta SD en el pin 4, se abre el archivo "archivo.txt" si la inicialización es exitosa, y se lee su contenido para enviarlo a través de la comunicación serial.
 
 - ##### * Función: void loop():*
   Esta función está vacía y no contiene ninguna instrucción

### Salida por el puerto serie
Supongamos que el archivo contiene lo siguiente:

**Este es un archivo de prueba.** 
**1234567890**

La salida por puerto serie es la siguiente:
```
Iniciando SD ... inicializacion exitosa
archivo.txt:
Este es un archivo de prueba.
1234567890
```

## EJERCICIO PRÁCTICO 2- LECTURA DE ETIQUETA RFID
```c++
#include <SPI.h>
#include <MFRC522.h>
#define RST_PIN 9 
#define SS_PIN 10 
MFRC522 mfrc522(SS_PIN, RST_PIN); 
void setup() {
Serial.begin(9600); 
SPI.begin(); 
mfrc522.PCD_Init(); 
Serial.println("Lectura del UID");
}
void loop() {

if ( mfrc522.PICC_IsNewCardPresent())
{
//Seleccionamos una tarjeta
if ( mfrc522.PICC_ReadCardSerial())
{
// Enviamos serialemente su UID
Serial.print("Card UID:");
for (byte i = 0; i < mfrc522.uid.size; i++) {
Serial.print(mfrc522.uid.uidByte[i] < 0x10 ? " 0"
: " ");
Serial.print(mfrc522.uid.uidByte[i], HEX);
}
Serial.println();
// Terminamos la lectura de la tarjeta actual
mfrc522.PICC_HaltA();
}
}
}
```
### Funcionamiento del código
En este código se establece la comunicación con el módulo lector de tarjetas RFID MFRC522, entonces lo que hace es que escanea en busca de tarjetas RFID y, cuando detecta una, lee su UID y lo muestra en el monitor serial. Esto permite identificar de forma única cada tarjeta presente en el área de alcance del lector RFID.

#### Funciones específicas del código:

### Salida por el puerto serie
```
DESCRBIR SALIDA
```




