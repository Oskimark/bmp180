# bmp180
reciclaje de sensor de presion compatible BMP180 sacado de un celular



cableado
1
2 scl
3 sda
4



8
7 
6 3.3v
5 gnd


codigo

#include <SFE_BMP180.h>
#include <Wire.h>

SFE_BMP180 bmp180;

void setup()
{
  Serial.begin(9600);

  if (bmp180.begin())
    Serial.println("BMP180 iniciado correctamenten");
  else
  {
    Serial.println("Error al iniciar el BMP180");
    while(1); // bucle infinito
  }
}

void loop()
{
  char status;
  double T,P;
   
  status = bmp180.startTemperature();//Inicio de lectura de temperatura
  if (status != 0)
  {   
    delay(status); //Pausa para que finalice la lectura
    status = bmp180.getTemperature(T); //Obtener la temperatura
    if (status != 0)
    {
      status = bmp180.startPressure(3); //Inicio lectura de presión
      if (status != 0)
      {        
        delay(status);//Pausa para que finalice la lectura        
        status = bmp180.getPressure(P,T); //Obtenemos la presión
        if (status != 0)
        {                  
          Serial.print("Temperatura: ");
          Serial.print(T,2);
          Serial.print(" *C , ");
          Serial.print("Presion: ");
          Serial.print(P,2);
          Serial.println(" mb");          
        }      
      }      
    }   
  } 
  delay(1000);
}![bmp180 casero](https://github.com/Oskimark/bmp180/assets/17094891/3e4d26fd-f27c-4833-b654-8d0f6b45fec1)
