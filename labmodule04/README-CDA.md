# Constrained Device Application (Connected Devices)

## Lab Module 04

Be sure to implement all the PIOT-CDA-* issues (requirements).

### Description

NOTE: Include two full paragraphs describing your implementation approach by answering the questions listed below.

What does your implementation do? 

How does your implementation work?

A continuación, se detalla el procedimiento seguido para implementar los requisitos establecidos en el Lab Module 04:

PIOT-CFG-04-001 -> Primeramente, se ha precisado instalar las dependencias GTK y PyGObject, en que la primera consiste 
en una biblioteca empleada para poder crear interfaces gráficas de usuario (por ejemplo, apps con botones, windows, 
menús...) mientras que PyGObject permite emplear GTK desde Python pudiendo aprovechar la potencia y versatilidad de las
librerías en lenguaje C. Para la instalación de estas dependencias se han empleado los siguientes comandos:

-> sudo apt install gcc libcairo2-dev pkg-config python3-dev libgirepository1.0 dev gir1.2-gtk-4.0 meson cmake
-> pip install pycairo
-> pip install pygobject

Segundamente, se ha procedido a instalar el emulador que se empleará en el desarrollo de la práctica (Sense-Emu Sense 
HAT) así como la librería "pisense". Para la instalación, se han empleado los siguientes comandos:

-> pip install sense-emu
-> pip install pisense

Instaladas todas las dependencias y el emulador, se ha actualizado el requirements del entorno virtual de trabajo 
mediante el siguiente comando:

-> pip freeze > requirements.txt

Al ejecutar el test de integración "SenseHatEmulatorQuickTest" se ha observado un error acerca de la función "textsize" 
y esto se puede deber a que la librería ImageDraw en la versión 3.10 de Python la ha deprecado. PAra solucionar este 
problema, se ha accedido al módulo anim.py de la librería pisense y se han hecho las siguientes modificaciones:

- Comentada la línea 167
- Modificada la línea 168 por el siguiente código:

--> x, y, width, height = draw.textbbox((0,0), text, f)

Seguidamente, se ejecuta nuevamente el test de integración y se observa como en el emulador Sense Hat se observa el 
hardware emulado con mensajes corriendo por el display así como un output similar al proporcionado en las notas de 
Notion.

PIOT-CDA-04-000 -> Se ha procedido a crear una nueva rama denominada labmodule04.

PIOT-CDA-04-001 -> Primeramente, se ha modificado el archivo de configuración cambiando a True los parámetros 
"enableEmulator" y "enableSenseHat" para poder operar el Sense Hat en modo emulador.

Seguidamente, se ha editado el módulo "HumiditySensorEmulatorTask", modificando el constructor de la clase añadiendo 
el name y el typeID del emulador de la tarea del sensor de humedad en cuestión y definiendo el método abstracto 
"generateTelemetry" implementado previamente en la clase BaseSensorSimTask. Este procedimiento se sigue de la misma 
forma para los módulos "TemperatureSensorEmulatorTask" y "PressureSensorEmulatorTask".

En esta seccion, se han ejecutado los tests de integración "HumidityEmulatorTaskTest", "PressureEmulatorTaskTest" y 
"TemperatureEmulatorTaskTest", pasando todos ellos correctamente proporcionando información acerca del dato tomado por
el sensor, el nombre y ID del sensor, entre otros parámetros. Si se cambian valores del respectivo sensor en la GUI del 
Sense HAT mientras se ejecutan los tests se puede observar como el valor mostrado corresponde al establecido.

PIOT-CDA-04-002 -> Se han editado los módulos "HumidifierEmulatorTask", "HvacEmulatorTask" y "LedDisplayEmulatorTask", 
los cuales heredan de la clase BaseActuatorSimTask. En ellos, se ha procedido a implementar el constructor de la clase 
añadiendo el name y el typeID de la tarea emulada del actuador así como la definición de los métodos abstractos 
"_activateActuator" y "_deactivateActuator".

En esta sección, se han ejecutado los tests de integración "HumidifierEmulatorTaskTest", "HvacEmulatorTaskTest" y 
"LedDisplayEmulatorTaskTest", pasando todos ellos correctamente proporcionando información acerca de cuando se activa 
el actuador, el ID del actuador, el valor ofrecido, entre otros parámetros (el output es muy similar al proporcionado 
en las notas del Notion). También, en el momento que se activa el actuador correspondiente, en la pantalla del emulador
Sense HAT se visualiza que el tipo de actuador esta en modo ON y el valor aplicado.

PIOT-CDA-04-003 -> Se ha editado el módulo "SensorAdapterManager" para añadir la funcionalidad del emulador. En la 
issue PIOT-CDA-03-006, ya se implementó el método "_initEnvironmentalSensorTasks" el cual permite instanciar las tareas 
de los sensores sin definirlos en el constructor de la clase. En esta ocasión, se le ha añadido al método un else donde 
si enableEmulator es True se cargan dinámicamente las tareas del emulador (la carga dináimica se emplea para asegurar 
que solo se carguen las tareas en tiempo de ejecución si el emulador está habilitado, ya que podrían estar configurados
para comunicarse directamente con el hardware del Sense HAT).

En esta sección, se ha ejecutado el test de integración "SensorEmulatorManagerTest", pasando correctamente pudiendo 
observar los datos generados y el mensaje de cada sensor (humedad, temperatura y presión). También, si se procede a 
cambiar algún valor desde la GUI del emulador, se observa dicho cambio en el output por terminal, mostrando la buena 
conexión entre el emulador y las tareas de los sensores.

PIOT-CDA-04-004 -> Se ha editado el módulo "ActuatorAdapterManager para añadir la funcionalidad del emulador. El 
procedimiento es muy similar a la issue anterior pero, en este caso, se modifica la implementación del método 
"_initEnvironmentalActuationTasks" efectuada en la issue PIOT-CDA-03-007. Para ello, al método se le adiciona un else 
donde si el useEmulator es True se cargarán dinámicamente las tareas del emulador.

En esta sección, se ha ejecutado el test de integración "ActuatorEmulatorManagerTest", visualizando un output similar 
al proporcionado en las notas del Notion (en el output se observa como se activa el actuador y se actualizan los 
valores de los actuadores humidificador, HVAC y el display LED y como se desactiva el actuador correspondiente.

PIOT-CDA-04-005 -> Esta sección resulta opcional en el caso de que se quisiera tener un dispositivo físico real 
(por ello se pide instalar la librería I2c la cual permite la gestión y facilita la comunicación y el control eficiente 
de diversos dispositivos electrónicos mediante el protocolo I2C (Inter-Integrated Circuit). En este caso, como no se
dispone de un dispositivo físico real, este requisito no se ha realizado en la práctica.

PIOT-CDA-04-100 -> Se ha llevado a cabo el merge de la rama labmodule04 a la rama main o default para comenzar la
siguiente sección Lab Module 05.

### Code Repository and Branch

NOTE: Be sure to include the branch.

URL: https://github.com/NicolGallo/PIC_Python_Components/tree/labmodule04


### Unit Tests Executed

NOTE: The instructor will execute your unit tests. You only need to list each test case below
(e.g. ConfigUtilTest, DataUtilTest, etc). Be sure to include all previous tests, too,
since you need to ensure you haven't introduced regressions.

- 
- 
- 

### Integration Tests Executed

NOTE: The instructor will execute most of your integration tests using their own environment, with
some exceptions (such as your cloud connectivity tests). In such cases, they'll review
your code to ensure it's correct. As for the tests you execute, you only need to list each
test case below (e.g. SensorSimAdapterManagerTest, DeviceDataManagerTest, etc.)

- SenseHatEmulatorQuickTest
- HumidityEmulatorTaskTest
- PressureEmulatorTaskTest
- TemperatureEmulatorTaskTest
- HumidifierEmulatorTaskTest
- HvacEmulatorTaskTest
- LedDisplayEmulatorTaskTest
- SensorEmulatorManagerTest
- ActuatorEmulatorManagerTest

EOF.
