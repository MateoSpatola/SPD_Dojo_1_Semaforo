# Dojo N°1 (Parte 3) Semaforo
![Tinkercad](./img/ArduinoTinkercad.jpg)


## Integrantes 
- Spatola Mateo
- Videla Ribodino Ivan
- Manzanares Patricio
- Quiroga Joaquin
- Santa Eulalia Matias


## Proyecto: Semaforo.
![Tinkercad](./img/semaforo3.png)


## Descripción
Este es el código correspondiente al Dojo 1 del Grupo C. En este código se utiliza un Arduino para controlar la iluminación de tres LEDs (Rojo, Amarillo y Verde) y un timbre. El objetivo del Dojo fue familiarizarse con la programación en Arduino y la interacción con componentes electrónicos.

Consignas Parte 3 (Nuevos requisitos):
- Agregar un botón (pull down) que al presionarlo se active la funcionalidad de luz verde con más tiempo, dándole a la persona que lo necesite más tiempo para cruzar la calle , sirve para la próxima luz verde y solo para la próxima luz verde después de presionar el botón. el tiempo se duplicará. 
-  Colocar dos semáforos de calles que se crucen  y programarlos para que funcionen en conjunto.


## Función principal
El código hace uso de varias funciones para controlar los LEDs, el timbre y el pulsador. 
Hubo muchas modificaciones del código anterior, ya que ahora son semáforos enfrentados.
Además si se presiona el pulsador añade el doble de tiempo a la LED verde para que cruce el peatón.

Se crearon las funciones loopSemaforoUno() y loopSemaforoDos(), que recorren cada semaforo individualmente.

~~~ C (lenguaje en el que esta escrito)
void loopSemaforoUno()
{
  prenderLed(LED_ROJO_DOS);
  prenderLedConSonido(LED_ROJO_UNO);
  titilarLed(LED_ROJO_UNO,200,3);
  
  prenderLedConSonido(LED_AMARILLO_UNO);
  titilarLed(LED_AMARILLO_UNO,200,3);
  
  prenderUnTiempo(LED_VERDE_UNO,5000);
  titilarLed(LED_VERDE_UNO,200,3);
  
  prenderLedConSonido(LED_AMARILLO_UNO);
  titilarLed(LED_AMARILLO_UNO,200,3);
  apagarLed(LED_ROJO_DOS);
}
~~~

~~~ C (lenguaje en el que esta escrito)
void loopSemaforoDos()
{
  prenderLed(LED_ROJO_UNO);
  prenderLedConSonido(LED_ROJO_DOS);
  titilarLed(LED_ROJO_DOS,200,3);
  
  prenderLedConSonido(LED_AMARILLO_DOS);
  titilarLed(LED_AMARILLO_DOS,200,3);
  
  prenderUnTiempo(LED_VERDE_DOS,5000);
  titilarLed(LED_VERDE_DOS,200,3);
  
  prenderLedConSonido(LED_AMARILLO_DOS);
  titilarLed(LED_AMARILLO_DOS,200,3);
}
~~~

Luego se agregaron las funciones loopSemaforoUnoConTiempoVerdeDuplicado() y loopSemaforoDosConTiempoVerdeDuplicado(), que al presionar el pulsador recorren cada semaforo individualmente duplicando el tiempo en el que la led verde esta encendida.

~~~ C (lenguaje en el que esta escrito)
void loopSemaforoUnoConTiempoVerdeDuplicado()
{
  prenderLed(LED_ROJO_DOS);
  prenderLedConSonido(LED_ROJO_UNO);
  titilarLed(LED_ROJO_UNO,200,3);
  
  prenderLedConSonido(LED_AMARILLO_UNO);
  titilarLed(LED_AMARILLO_UNO,200,3);
  
  prenderUnTiempo(LED_VERDE_UNO,10000);
  titilarLed(LED_VERDE_UNO,200,3);
  
  prenderLedConSonido(LED_AMARILLO_UNO);
  titilarLed(LED_AMARILLO_UNO,200,3);
  apagarLed(LED_ROJO_DOS);
}
~~~

~~~ C (lenguaje en el que esta escrito)
void loopSemaforoDosConTiempoVerdeDuplicado()
{
  prenderLed(LED_ROJO_UNO);
  prenderLedConSonido(LED_ROJO_DOS);
  titilarLed(LED_ROJO_DOS,200,3);
  
  prenderLedConSonido(LED_AMARILLO_DOS);
  titilarLed(LED_AMARILLO_DOS,200,3);
  
  prenderUnTiempo(LED_VERDE_DOS,10000);
  titilarLed(LED_VERDE_DOS,200,3);
  
  prenderLedConSonido(LED_AMARILLO_DOS);
  titilarLed(LED_AMARILLO_DOS,200,3);
}
~~~


En el loop principal del código, se encienden ambos semaforos, y empieza el recorrido de uno de los semaforos mientras el otro se queda con el led rojo encendido, luego cuando el primer semaforo termina el recorrido, empieza el siguiente y asi sucesivamente.
~~~ C (lenguaje en el que esta escrito)

void loop()
{
  if(digitalRead(BOTON) == 0)
  {
    loopSemaforoUno();
  }
  if(digitalRead(BOTON) == 1)
  {
    //Si el boton se encuentra pulsado, el siguiente 
    //semaforo arrancara con el tiempo de luz vede duplicado
    loopSemaforoDosConTiempoVerdeDuplicado();
  }
  
  if(digitalRead(BOTON) == 0)
  {
    loopSemaforoDos();
  }
  if(digitalRead(BOTON) == 1)
  {
    //Si el boton se encuentra pulsado, el siguiente 
    //semaforo arrancara con el tiempo de luz vede duplicado
    loopSemaforoUnoConTiempoVerdeDuplicado();
  }
}
~~~


## :robot: Link al proyecto
- [Proyecto](https://www.tinkercad.com/things/9Vku32oaMTg)

> Recomendación: Al iniciar simulación bajar volumen.
