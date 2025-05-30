# Gateway Device Application (Connected Devices)

## Lab Module 10

Be sure to implement all the PIOT-GDA-* issues (requirements) listed.

### Description

NOTE: Include two full paragraphs describing your implementation approach by answering the questions listed below.

What does your implementation do? 

Se han realizado modificaciones en el módulo MqttClientConnector para incluir soporte de credenciales y conexiones 
seguras mediante TLS, así como la suscripción a topics relevantes del CDA. Asimismo, se ha ampliado la lógica de gestión
en el DeviceDataManager para procesar mensajes de sensores, incluyendo condiciones específicas asociadas a sensores de 
humedad. Cada una de estas modificaciones ha sido validada mediante pruebas de integración diseñadas específicamente 
para asegurar su correcto funcionamiento.

How does your implementation work?

PIOT-GDA-10-000 -> Se ha procedido a crear una nueva rama labmodule10 para empezar la elaboración de la práctica 10.

PIOT-GDA-10-001 -> Se ha procedido a modificar el módulo "MqttClientConnector" para que haya soporte para la carga y 
configuración de valores de autorización (como usuarios y passwords) así como conexiones encriptadas mediante TLS al 
broker. Para ello, se ha implementado la lógica de los métodos privados initCredentialConnectionParameters, 
initSecureConnectionParameters y initClientParameters. También se ha modificado el constructor de la clase para llamar 
directamente a su vez a initClientParameters el cual a su vez llamará a initCredentialConnectionParameters o 
initSecureConnectionParameters en función de si la conexión se efectúa con seguridad o no.

En esta sección, se ha ejecutado el test de integración "MqttClientConnectorTest" con la configuración por defecto del 
programa y sin habilitar la seguridad TLS.

PIOT-GDA-10-002 -> Se ha procedido a modificar nuevamente el módulo "MqttClientConnector" para añadir la lógica 
requerida para realizar la suscripción a los topics del CDA relacionados con mensajes correspondientes a SensorData, 
SystemPerformanceData y mensajes de respuesta de ActuatorData. Para ello, se ha implementado los métodos "connectComplete" 
y "messageArrived" (respecto a la opción 1 que proporciona las notas del Notion), en que la primera es un callback 
necesario que se invoca una vez se ha efectuado la conexión del cliente al broker para poder asegurar que las suscripciones
de topics se efectúan a posteriori de una conexión con éxito. El messageArrived permite, una vez se ha registrado para 
todas las notificaciones de suscripción, analizar o parsear el contenido del topic para saber si está relacionado con 
ActuatorData, SystemPerformanceData o SensorData antes de proceder a su envío del escuchador o listener.

En esta sección, se ha ejecutado el test de integración "MqttClientConnectorTest", y se ha añadido un nuevo test a este 
módulo denominado testActuatorCommandResponseSubscription (elaborado para asegurar que los mensajes de Actuator Response
sean recibidos y procesados).

PIOT-GDA-10-003 -> Se ha procedido a modificar el "DeviceDataManager" para adicionar la gestión de los mensajes CDA 
entrantes sobre SystemPerformanceData, SensorData y mensajes de respuesta de ActuatorData. Para ello, primeramente se ha 
añadido en el archivo Config.props nuevos parámetros sobre valores de humedad para poder implementar la lógica posterior 
para determinar el traspaso de un threshold establecido. EStos valores se han añadido a su vez en el archivo ConfigConst
para poder ser utilizadas desde el DeviceDataManager. A continuación, se ha procedido a implementar la lógica del método 
"handleSensorMessage" el cual a su vez llama al método privado "handleIncomingDataAnalysis" que se encarga añadir el 
requisito correspondiente al traspaso del valor del threshold. Esto se efectúa dado que en el método se chequea si el 
tipo de dato es un sensor de humedad y, en caso afirmativo, se procede a llamar a un siguiente método privado 
"handleHumiditySensorAnalysis" que realiza toda la lógica implementada.

En esta sección, se ha ejecutado un nuevo módulo de test creado denominado "DeviceDataManagerSimpleCdaActuationTest", el
cual permite comprobar el buen funcionamiento del DeviceDataManager al recibir mensajes de tipo SensorData que provienen
de lecturas de humedad del CDA (lo cual se puede comprobar emulando los cambios de lectura mediante el SenseHAT).


### Code Repository and Branch

NOTE: Be sure to include the branch.

URL: https://github.com/NicolGallo/PIC_Java_Components/tree/labmodule10



### Unit Tests Executed

NOTE: The instructor will execute your unit tests. You only need to list each test case below
(e.g. ConfigUtilTest, DataUtilTest, etc). Be sure to include all previous tests, too,
since you need to ensure you haven't introduced regressions.

- Todos los tests unitarios de la parte1.
- Todos los tests unitarios de la parte2.
- Todos los tests unitarios de la parte3.

### Integration Tests Executed

NOTE: The instructor will execute most of your integration tests using their own environment, with
some exceptions (such as your cloud connectivity tests). In such cases, they'll review
your code to ensure it's correct. As for the tests you execute, you only need to list each
test case below (e.g. SensorSimAdapterManagerTest, DeviceDataManagerTest, etc.)

- Todos los tests de integración de la parte1.
- Todos los tests de integración de la parte2.
- Todos los tests de integración de la parte3.
- MqttClientConnectorTest
- DeviceDataManagerSimpleCdaActuationTest

EOF.
