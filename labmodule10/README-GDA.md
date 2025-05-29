# Gateway Device Application (Connected Devices)

## Lab Module 10

Be sure to implement all the PIOT-GDA-* issues (requirements) listed.

### Description

NOTE: Include two full paragraphs describing your implementation approach by answering the questions listed below.

What does your implementation do? 

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
requerida realizar la suscripción a los topics del CDA relacionados con mensajes correspondientes a SensorData, 
SystemPerformanceData y mensajes de respuesta de ActuatorData.

### Code Repository and Branch

NOTE: Be sure to include the branch.

URL: https://github.com/NicolGallo/PIC_Java_Components/tree/labmodule10



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

- MqttClientConnectorTest
- 
- 

EOF.
