# Práctica 6: BUSES DE COMUNICACIÓN II (SPI)
## Introducción parte práctica
En la anterior práctica trabajamos con los buses de comunicación, en esta práctica seguiremos trabajando con estos, pero especializándonos en el bus SPI.

La práctica constará de 3 partes 
 - Lectura i escritura de memoria SD
 -
 -

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
myFile = SD.open("archivo.txt");//abrimos el archivo
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
El principal objetivo del código 




### Salida por el puerto serie
```
DESCRBIR SALIDA
```
## EJERCICIO PRÁCTICO 2- LECTURA DE ETIQUETA RFID
```c++
#include <SPI.h>
#include <MFRC522.h>
#define RST_PIN 9 //Pin 9 para el reset del RC522
#define SS_PIN 10 //Pin 10 para el SS (SDA) del RC522
MFRC522 mfrc522(SS_PIN, RST_PIN); //Creamos el objeto para el RC522
void setup() {
Serial.begin(9600); //Iniciamos la comunicación serial
SPI.begin(); //Iniciamos el Bus SPI
mfrc522.PCD_Init(); // Iniciamos el MFRC522
Serial.println("Lectura del UID");
}
void loop() {
// Revisamos si hay nuevas tarjetas presentes
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
El código proporcionado

### Salida por el puerto serie
```
DESCRBIR SALIDA
```




