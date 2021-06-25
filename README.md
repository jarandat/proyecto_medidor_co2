# Medidor CO2 para prevención de la transmisión del Covid19 en ambientes interiores

Al respirar, absorbemos oxígeno del aire y al exhalar expulsamos dióxido de carbono (CO2). En ambientes interiores, con el correr de los minutos, si no se ventila, la respiración de las personas allí presentes hace que suba la concentración de CO2. Se ha demostrado que hay correlación entre esa concentración y el riesgo de contagio de enfermedades respiratorias en general. En realidad, hay una antigua prescripción médica sobre ventilar para prevenir el contagio de enfermedades respiratorias. En este tiempo de pandemia de COVID-19, esa recomendación se transformó en la principal para minimizar el riesgo de contagio. En resumen, es importante medir la concentración de CO2 para saber si un ambiente interior está suficientemente ventilado dada una cierta cantidad de gente que realiza actividad en ese espacio. 

Se propone el diseño de un dispositivo medidor de CO2, de uso orientativo, para espacios interiores, como medida de prevención de enfermedades infecciosas que se contagian mediante aerosoles (particularmente, COVID-19). 

El objetivo es que el dispositivo propuesto sea de uso sencillo, lo más económico posible, y de diseño libre. El dispositivo solamente tiene cuatro componentes. Además del sensor y la computadora, hay un LED RGB para indicar, mediante colores, el nivel de concentración de CO2 en el ambiente interior donde se use. El cuarto componente, es simplemente un pulsador. 

El diseño cuenta con una computadora de placa reducida, también llamado de placa única, de placa simple (SBC), o sistema en un chip (SoC), de bajo costo. En este caso, el sistema propuesto es de la familia ESP32 con tecnología Bluetooth y WiFi integrada. Por eso último, el instrumento no va a necesitar una pantalla, en su lugar, una app para Android o una aplicación web, van a mostrar los valores de CO2 actuales, las series de tiempo, y otros análisis para estudio y toma de decisiones (por ejemplo, ventilar más, reducir el aforo, etc.).

La situación sanitaria evidencia la necesidad de usar este tipo de dispositivos, no solo en esta coyuntura, sino post-pandemia, como elemento que apunta a asegurar un nivel de calidad de aire desde el punto de vista sanitario. En otras palabras, sería un elemento más de seguridad e higiene en espacios donde se realicen diferentes tipos de actividades humanas, incluida la educación en todos sus niveles.

## Lista de materiales

Son cuatro componentes más los cables de conexión y el gabinete.
1. ESP32: Hay diversos modelos y versiones del SoC ESP32.
2. Sensor MH-Z19b
3. Pulsador
4. LED RGB más 3 resistencias 220 ohm (por simplicidad, se recoienda que sea en un solo módulo).

En esta aplicación, el significado de los colores es el siguiente:
- Verde significa baja concentración de CO2, bajo riesgo de contagio por aerosoles.
- Amarillo es acercándose a riesgo alto.
- Rojo es riesgo alto, debe ventilarse el ambiente.
- Violeta es riesgo alto, debería evacuarse momentáneamente el ambiente.

El LED en azul significa que el sensor se está calentando o que el aparato está en modo de calibración.

## Conexión de componentes

![Diagrama de conexiones](https://github.com/medicionco2/proyecto_medidor_co2/blob/main/diagramas_conexion/diagrama_esp32.png)

La alimentación del dispositivo se hace mediante un cargador USB estándar.

El sensor puede venir con un cable armado con una ficha que no es compatible con los conectores del ESP32. Por eso, una alternativa es cortar el cable y  empalmar cables dupont.

Para más ayuda, ese video muestra en detalle cómo se conecta el sensor MH-Z19b al ESP32 https://www.youtube.com/watch?v=vmDCqNXVZKQ

En resumen, conectar el sensor requiere de 4 cables: Alimentación (5V), tierra (GND), y los dos cables de la conexión serie (Tx y Rx). 

## Programación

1. Instalar IDE Arduino en una PC. 
2. Instalar soporte para ESP32.
Las instrucciones para estos dos primeros pasos se pueden ver en https://randomnerdtutorials.com/installing-the-esp32-board-in-arduino-ide-windows-instructions/ 
	
3. Instalar librería para el sensor MH-Z19b.
	https://github.com/piot-jp-Team/mhz19_uart 
4. Copiar y compilar el código fuente seleccionado usando Arduino IDE.
5. Descargar el código ejecutable en el ESP32 de manera que quede programado con la aplicación seleccionada.

## Funcionamiento

Una vez conectado el cable USB, el dispositivo se pone en funcionamiento. No hay botón de encendido. El sensor tarda tres minutos para iniciar sus medidas, eso se indica con el LED encendido en color azul. Pasado ese tiempo, el LED indica la concentración de CO2 mediante colores: verde (poca concentracón de CO2, más seguro), amarillo, rojo y violeta (muy alta concentración de CO2, menos seguro). A su vez, se envían las medidas de CO2 y temperatura por WiFi o Bluetooth, según cuál programa se haya cargado en el dispositivo. 

Si se seleccionó la versión Bluetooth, se pueden ver las medidas en un teléfono inteligente. Una posibilidad es usar la app "Serial Bluetooth Terminal" que se pude descargar en el teléfono desde https://play.google.com/store/apps/details?id=de.kai_morich.serial_bluetooth_terminal&hl=en&gl=US

### Calibración

Al aire libre, la concentración de CO2 es cercana a las 400 ppm. Por eso, el dispositivo se calibra al aire libre y de esa manera se establece una referencia.

Para la calibración, hay que poner el dispositivo al aire libre, oprimir el pulsador por al menos un segundo y esperar al menos 20 minutos. En ese estado, el LED está encendido en color azul con intensidades variables que se repiten cíclicamente. Se recomienda repetir la calibración mensualmente y realizarla al menos una vez cada 6 meses.  

## Más Información

- Importancia de la ventilación para la prevención de la COVID-19.  Canal del Ministerio de Ciencia, Tecnología e Innovación, 26 marzo de 2021. https://youtu.be/fpMb1TzraGw  

- Natalia Rubinstein, Ciclo Ciencia para ventilar: Yo ventilo, ella ventila, vos ventilás. ¿Pero lo hacemos bien? https://youtu.be/4q3odycwvYs

- Sandra Cordo, Ciclo Ciencia para ventilar: Transmisión de Covid-19 por aire. Principales medidas de prevención. https://youtu.be/4AUWS4Dpn0A

- Alejandro Nadra, Juan Fernández Zaragoza, Ciclo Ciencia para ventilar: ¿Qué son las tecnologías libres y qué aportan en el contexto de pandemia? https://youtu.be/301sSYFhCg8

- Página de Jorge Aliaga (Medición de CO2) http://www.jorgealiaga.com.ar/?page_id=2864 
      Sw: https://github.com/jlaliaga/Medidor-de-CO2/releases/tag/V2 

- Comparativa de sensores, https://soloelectronicos.com/2020/11/01/monitor-de-co2-con-sensor-mh-z19/
      Recomiendan el MH-Z19, lo mismo que Jorge Aliaga. La ventaja adicional, que no mencionan, es que al tener medida de temperatura junto con CO2, se puede controlar la habitabilidad de un espacio con un criterio CO2 y temperatura combinado.
