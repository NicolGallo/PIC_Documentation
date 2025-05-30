# Constrained Device Application (Connected Devices)

## Lab Module 09

Be sure to implement all the PIOT-CDA-* issues (requirements) listed.

### Description

NOTE: Include two full paragraphs describing your implementation approach by answering the questions listed below.

What does your implementation do? 

La implementación desarrolla un cliente CoAP completo en el módulo CoapClientConnector, que extiende la interfaz 
IRequestResponseClient. Se integran y completan los métodos de envío de peticiones (GET, POST, PUT, DELETE) y de 
observación (startObserver, stopObserver), cada uno con su respectiva lógica de manejo y callbacks asincrónicos 
(_handleRequest, _onResponse). Además, se crea un generador de URIs y se habilita el cliente desde el 
DeviceDataManager.

How does your implementation work?

A continuación, se detalla el procedimiento seguido para implementar los requisitos establecidos en el Lab Module 09:

PIOT-CDA-09-000 -> Se ha procedido a crear una nueva rama labmodule09 para empezar la elaboración de la práctica 09.

PIOT-CDA-09-001 -> Se ha añadido parte de la implementación de la lógica del módulo "CoapClientConnector", en que dicha 
clase hereda de la clase "IRequestResponseClient". Dentro de la clase "CoapClientConnector" se ha modificado el 
constructor para poder utilizar o recuperar la información del puerto y del host del CoAP Gateway. Por otro lado, se ha 
modificado el constructor del cliente (_initClient_) para añadir la lógica de la creación de la instancia del propio 
cliente a partir de un método asíncrono (_initClientContext) que pueda invocarse dentro del constructor a través del 
bucle de eventos de asyncio.

Para la resta de métodos como sendDiscoveryRequest, sendDeleteRequest, sendGetRequest, sendPostRequest, sendPutRequest, 
startObserver y stopObserver, por el momento solo se ha añadido un log informativo de acuerdo a que el método ha sido 
llamado. El método "setDataMessageListener" simplemente cuenta por ahora con una pequeña implementación donde se 
instancia un listener y se proporciona un log informativo.

Por último, se ha creado un nuevo método, "_createResourcePath", para generar una URI a partir de un ResourceNameEnum y 
cualquier otra posible cadena final que sea pasada a alguno de los métodos de petición.

El DeviceDataManager también ha sido actualizado incorporando en el constructor si el CoAP Client está habilitado 
recuperando el valor desde configUtil.

PIOT-CDA-09-002 -> Se ha procedido a añadir una lógica más completa sobre el método "sendGetRequest", mediante el cual 
se han implementado dos métodos nuevos: "_handleGetRequest" y "_onGetResponse" (el primero para encapsular la respuesta 
de la petición GET y el segundo para funcionar como callback de la encapsulación de las respuestas de las peticiones 
GET). Seguidamente, se ha implementado una modificación en el método "sendDiscoveryRequest", el cual emitirá una 
petición de descubrimiento al servidor, proporcionando la lista de recursos que están registrados en el servidor.

En esta sección, se ha ejecutado el test de integración "CoapClientConnectorTest", en que se ha skippeado todos menos 
los tests "testConnectAndDiscover", "testGetActuatorCommandCon", y "testGetActuatorCommandNon".

PIOT-CDA-09-003 -> Se ha procedido a implementar de forma completa la lógica del método "sendPutRequest" de forma 
similar que anteriormente con el GET. También, al igual que con el GET antes, se han implementado dos nuevos métodos 
asociados al "sendPutRequest": "_handlePutRequest" y "_onPutResponse".

En esta sección, se ha ejecutado nuevamente el test de integración de "CoapClientConnectorTest", en que se han mantenido
skippeados la mayoría y se han habilitado los tests "testPutSensorMessageCon" y "testPutSensorMessageNon".

PIOT-CDA-09-004 -> Se ha procedido a implementar de forma completa la lógica del método "sendPostRequest" de forma 
similar. También, al igual que con el GET y el PUT anteriormente, se han implementado dos nuevos métodos asociados al 
"sendPostRequest": "_handlePostRequest" y "_onPostResponse".

En esta sección, se ha ejecutado nuevamente el test de integración de "CoapClientConnectorTest", en que se han mantenido
skippeados la mayoría y se han habilitado los tests "testPostSensorMessageCon" y "testPostSensorMessageNon".

PIOT-CDA-09-005 -> Se ha procedido a implementar de forma completa la lógica del método "sendDeleteRequest" 
de forma similar. También, al igual que anteriormente, se han implementado dos nuevos métodos asociados al 
"sendDeleteRequest": "_handleDeleteRequest" y "_onDeleteResponse".

En esta sección, se ha ejecutado nuevamente el test de integración de "CoapClientConnectorTest", en que se han mantenido
skippeados la mayoría y se han habilitado los tests "testDeleteSensorMessageCon" y "testDeleteSensorMessageNon".

PIOT-CDA-09-006 -> Se ha procedido a implementar de forma completa la lógica del método "startObserver" y "stopObserver"
de forma similar. También, al igual que anteriormente, se han implementado dos nuevos métodos asociados a cada método 
implementado: "_handleStartObserveRequest" y "_handleStopObserveRequest".

En esta sección, se ha ejecutado nuevamente el test de integración de "CoapClientConnectorTest", en que se han mantenido
skippeados la mayoría y se ha habilitado el test "testActuatorCommandObserve".

### Code Repository and Branch

NOTE: Be sure to include the branch.

URL: https://github.com/NicolGallo/PIC_Python_Components/tree/labmodule9


### Unit Tests Executed

NOTE: The instructor will execute your unit tests. You only need to list each test case below
(e.g. ConfigUtilTest, DataUtilTest, etc). Be sure to include all previous tests, too,
since you need to ensure you haven't introduced regressions.

- Todos los tests unitarios de la parte1.
- Todos los tests unitarios de la parte2.


### Integration Tests Executed

NOTE: The instructor will execute most of your integration tests using their own environment, with
some exceptions (such as your cloud connectivity tests). In such cases, they'll review
your code to ensure it's correct. As for the tests you execute, you only need to list each
test case below (e.g. SensorSimAdapterManagerTest, DeviceDataManagerTest, etc.)

- Todos los tests de integración de la parte1.
- Todos los tests de integración de la parte2.
- CoapClientConnectorTest
- MqttClientConnectorTest
- MqttClientControlPacketTest

EOF.
