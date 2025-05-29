# Constrained Device Application (Connected Devices)

## Lab Module 10

Be sure to implement all the PIOT-CDA-* issues (requirements) listed.

### Description

NOTE: Include two full paragraphs describing your implementation approach by answering the questions listed below.

What does your implementation do? 

How does your implementation work?

A continuación, se detalla el procedimiento seguido para implementar los requisitos establecidos en el Lab Module 10:

PIOT-CDA-10-000 -> Se ha procedido a crear una nueva rama labmodule10 para empezar la elaboración de la práctica 10.

PIOT-CDA-10-001 -> Se ha procedido a modificar el módulo "MqttClientConnector" incorporando dos en el constructor de la 
clase dos nuevas variables para poder detectar si la encriptación de mqtt está habilitada o no y encontrar la ruta de la
llava del certificado creado para la práctica en cuestión. Seguidamente, se ha modificado el método "connectClient" para
incorporar el chequeo de la encriptación habilitada y, en caso afirmativo, se deberá proceder a actualizar el puerto del
cliente y cargar el certificado (ya que se estaría trabajando en modo conexión segura con TLS) para conectarlo 
correctamente al broker.

En esta sección, se ha ejecutado el test de integración "MqttClientConnectorTest" en que se ha efectuado con la 
configuración por defecto, es decir, sin la habilitación de TLS.

PIOT-CDA-10-002 -> En esta sección no se ha modificado nada debido a que en PIOTS anteriores ya se efectuó la lógica 
(como recomendaban pasos previos) del método "handleActuatorCommandMessage". Para la ejecución del test correspondiente 
con esta sección, se ha desactivado de forma temporal los comandos enableMqttClient, enableCoapServer y enableCoapClient
(puestos a False) dentro del PiotConfig.props, y se ha ejecutado el test de integración "testActuatorDataCallbackTest".

PIOT-CDA-10-003 -> Se ha procedido a modificar nuevamente el módulo "MqttClientConnector" para poder llevar a cabo la 
suscripción a los mensajes de comando de ActuatorData desde el GDA y enviar los mensajes recibidos. Para ello, se ha 
implementado el método "onActuatorCommandMessage" el cual se trata de un método callback para gestionar o procesar los 
mensajes de suscripción entrantes para los mensajes de comando del actuador dado. También, se ha implementado la lógica 
de la función callbak "onConnect" para poder añadir suscripciones al comando del actuador.

Por último, se ha modificado el método "publishMessage" comentando la línea que se había introducido en PIOTS anteriores
correspondiente a la llamada wait_for_publish(), debido a que puede ocasionar una condición deadlock o un wait infinito 
ocasionando un bloqueo peligroso.

En esta sección, se ha ejecutado el test de integración "MqttClientConnectorTest", en que se han skippeado todos los 
tests menos el testNewActuatorCmdPubSub que es el propiamente ejecutado dentro del módulo.

PIOT-CDA-10-004 -> Se ha procedido a implementar la lógica del método "_handleUpstreamTransmission" dentro del módulo 
DeviceDataManager, en que este método se encargará de gestionar el envío de los datos del sensor al GDA utilizando MQTT.
Este método privado debe estar o ser llamado a su vez desde los métodos "handleSensorMessage" y 
"handleSystemPerformanceMessage" para realizar el cometido requerido en el PIOT (ya realizado dado que en PIOTS 
anteriores se estableció la llamada al método como manera de avanzar posible trabajo antes de llegar a este PIOT en 
cuestión). 

En esta sección, se ha ejecutado el test de integración "DeviceDataManagerIntegrationTest", en que simplemente se 
ejecuta el único test presente (testDeviceDataMgrTimedIntegration) que crea una instancia del DeviceDataManager y 
realiza un start del mismo (también se ha tenido que establecer a True el valor de enableEmulator y enableSenseHAT 
para observar en el display del emulador los mensajes correspondientes al paso del test establecido).

### Code Repository and Branch

NOTE: Be sure to include the branch.

URL: https://github.com/NicolGallo/PIC_Python_Components/tree/labmodule10


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

- DeviceDataManagerIntegrationTest
- MqttClientConnectorTest
- testActuatorDataCallbackTest

EOF.
