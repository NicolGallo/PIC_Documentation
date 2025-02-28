# Gateway Device Application (Connected Devices)

## Lab Module 05

Be sure to implement all the PIOT-GDA-* issues (requirements) listed.

### Description

NOTE: Include two full paragraphs describing your implementation approach by answering the questions listed below.

What does your implementation do? 

How does your implementation work?

A continuación, se detalla el procedimiento seguido para implementar los requisitos establecidos en el Lab Module 05:


PIOT-GDA-05-000 -> Se ha creado una nueva rama denominada labmodule05 para comenzar la realización de la presente 
sección.


PIOT-GDA-05-001 -> Se han editado los módulos "SensorData", "ActuatorData", "SystemPerformanceData" y "SystemStateData",
los cuales contendrán los datos procedentes de los sensores y los actuadores. De todos los módulos editados, se ha 
procedido a implementar los respectivos setters y getters de las clases para obtener y definir los valores de los 
diferentes paramétros correspondientes a los sensores o los actuadores. El último módulo, el "SystemStateData", se ha 
intentado implementar de forma opcional (aunque falta confirmar la correcta implementación). Este módulo proporciona un
único espacio para contener todos los datos que eventualmente se enviarán a la nube en una estructura fácilmente 
convertible a/desde JSON.

En esta sección, se han ejecutado los tests unitarios "ActuatorDataTest", "SensorDataTest", "SystemPerformanceDataTest" 
y "SystemStateDataTest", los cuales todos pasan correctamente proporcionando información acerca de los diferentes 
parámetros establecidos para los sensores y actuadores.


PIOT-GDA-05-002 -> Se ha editado el módulo "SystemPerformanceManager" para poder almacenar los datos recopilados del 
rendimiento del sistema. Para ello, se han introducido nuevas variables como locationID y una instancia del 
IDataMessageListener, en que este último si está configurado permite invocar el correspondiente método de callback. 
Con el método "handleTelemetry" se obtienen los valores de memoria y CPU utilizados por la aplicación mediante los 
métodos definidos en la issue anterior en la clase SystemPerformaceData.

En esta sección, se ha ejecutado el test de integración "SystemPerformanceManagerTest" proporcionando información sobre
cuando comienza y termina el SystremPerformanceManager así como los valores de memoria y CPU utilizados 
durante la prueba.

Nota: Falta implementar el método getTelemetryValue dentro del módulo nuevo creado "SystemDiskUtilTask". Hay que 
averiguar si JAVA permite en alguna de sus librerias algun método para el cálculo al igual que para la memoria y la CPU.


PIOT-GDA-05-003 -> Del mismo modo que se realizó en la issue PIOT-CDA-05-002, en este caso se ha editado el módulo 
"DataUtil" implementando los métodos ya definidos en la clase que permiten convertir los datos característicos de cada 
actuador, sensor y del gestor de rendimiento del sistema a un JSON, y el proceso inverso (convertir un JSON en una 
instancia del tipo ActuatorData, SensorData o SystemPerformanceManager).

En esta sección, se ha ejecutado el test unitario "DataUtilTest" y el test de integración "DataIntegrationTest", 
ambos pasando correctamente observando se producen las diferentes conversiones en ambas direcciones (instancia a JSON 
y JSON a instancia). Es importante recalcar, que el test de integración funciona correctamente cuando lo ejecutamos por
segunda vez habiendo ejecutado previamente el "DataIntegrationTest" del CDA implementado (ambos tests necesitan 
ejecutarse a la par para obtener el output correcto).

NOTA: En el caso de poder implementar correctamente el módulo "SystemStateData", se puede añadir opcionalmente los 
mismos métodos pero para convertir en JSON los datos de dicha clase y al inrevés.


PIOT-GDA-05-004 -> Se ha editado el módulo "DeviceDataManager", el cual resulta ser el núcleo principal del GDA 
implementado debido a que se encarga de todo el procesamiento de datos que tiene lugar en la aplicación y, a la vez, 
direcciona o dirige todas las solicitudes al destino apropiado. Para ello, se han añadido una serie de banderas o flags
en el constructor de la clase, en relación a la disponibilidad de la comunicación de la conexión.

Posteriormente, se ha implementado el método privado "initConnections", en la que se analizan las distintas flags 
aunque de momento no se ha establecido la lógica correspondiente (eso se efectuará en etapas más adelante del proyecto).
También, se ha implementado los métodos "startManager" y "stopManager" en que por el momento solo permiten visualizar 
un mensaje de depuración conforme el DeviceDataManager comienza y termina.

Por último, se ha implementado de forma básica la lógica de los métodos públicos de la clase como 
"handleActuatorCommandResponse", "handleIncomingMessage", "handleSensorMessage" y "handleSystemPerformanceMessage" 
(los cuales serán empleados más adelante como métodos callback) en que de momento solo incorporan un mensaje de 
depuración conforme se ha llamado al método), y también el método setActuatorDataListener.

En esta sección, se ha ejecutado el test de integración "DeviceDataManagerNoCommsTest", el cual pasa correctamente 
ofreciendo un simple output indicando cuando comienza y cuando termina el DeviceDataManager (debido a que aún no se ha 
procedido a realizar la lógica de conexión).

NOTA: Los métodos privados añadidos al final del módulo falta chequear que hacen exactamente y se estan bien como estan
actualmente (ya que en principio simplemente son declararlos y dejarlos vacíos por ahora).


PIOT-GDA-05-005 -> Se ha editado el módulo "GatewayDeviceApp" en que se ha modificado el contenido del main para 
eliminar a las llamadas sobre SystemPerformanceManager y cambiarlas por llamadas a DeviceDataManager dentro de los 
métodos, principalemente, de "startManager" y "stopManager", ya que la instancia del DeviceDataManager llama a su vez 
al SystemPerformanceManager. 

En esta sección, se ha ejecutado el test de integración "GatewayDeviceAppTest", el cual se observa que pasa correctamente ya 
que en el output se puede visualizar como se inicializa y comienza el GDA, el DeviceDataManager, el 
SystemPerformanceManager y se ofrecen valores de uso de memoria y CPU, y también como se detienen los mismos elementos 
(estas inicializaciones y detenciones se realizan en orden, indicando que todos los pasos seguidos hasta el momento se 
han correlacionado adecuadamente). 


PIOT-GDA-05-006 ->Requisito opcional, no implementado en la realización de la práctica.


PIOT-GDA-05-007 ->Requisito opcional, no implementado en la realización de la práctica.


PIOT-GDA-05-008 -> Requisito opcional, no implementado en la realización de la práctica.

PIOT-GDA-05-100 -> Se ha llevado a cabo el merge de la rama labmodule05 a la rama main o default para comenzar la 
siguiente sección.

### Code Repository and Branch

NOTE: Be sure to include the branch.

URL: https://github.com/NicolGallo/PIC_Java_Components/tree/labmodule05


### Unit Tests Executed

NOTE: The instructor will execute your unit tests. You only need to list each test case below
(e.g. ConfigUtilTest, DataUtilTest, etc). Be sure to include all previous tests, too,
since you need to ensure you haven't introduced regressions.

- ActuatorDataTest
- SensorDataTest
- SystemPerformanceDataTest
- SystemStateDataTest
- DataUtilTest

### Integration Tests Executed

NOTE: The instructor will execute most of your integration tests using their own environment, with
some exceptions (such as your cloud connectivity tests). In such cases, they'll review
your code to ensure it's correct. As for the tests you execute, you only need to list each
test case below (e.g. SensorSimAdapterManagerTest, DeviceDataManagerTest, etc.)

- SystemPerformanceManagerTest
- DataIntegrationTest
- DeviceDataManagerNoCommsTest
- GatewayDeviceAppTest

EOF.
