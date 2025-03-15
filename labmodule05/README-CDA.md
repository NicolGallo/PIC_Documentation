# Constrained Device Application (Connected Devices)

## Lab Module 05

Be sure to implement all the PIOT-CDA-* issues (requirements).

### Description

NOTE: Include two full paragraphs describing your implementation approach by answering the questions listed below.

What does your implementation do?

La implementación permite recopilar y almacenar datos de rendimiento del sistema, incluyendo el uso de CPU, memoria y 
disco. También facilita la conversión de estos datos a formato JSON y viceversa, asegurando su correcta gestión y 
transmisión. Además, se han incorporado pruebas para verificar el funcionamiento del sistema.

How does your implementation work?

A continuación, se detalla el procedimiento seguido para implementar los requisitos establecidos en el Lab Module 05:

PIOT-CDA-05-000 -> Se ha creado una nueva rama denominada labmodule05 para comenzar la realización de la presente sección.

PIOT-CDA-05-001 -> Se ha editado el módulo "SystemPerformanceManager" para poder implementar el almacenamiento de los 
datos recopilados por el sistema de rendimiento. Para ello, dentro de la clase del módulo, se ha editado el método 
"handleTelemetry" incluyendo la inicialización de una instancia de tipo SystemPerformanceData, la cual permitirá 
obtener los datos de uso de CPU y memoria.

Opcionalmente, se ha añadido dentro del método "handleTelemetry" dentro de la clase SystemPerformanceManager para que, 
en adición, aparte de la recopilación del uso de CPU y memoria, se recopile el uso de disco. Para ello, también se ha 
implementado un nuevo módulo denominado SystemDiskUtilTask para llevar a cabo dicha tarea (implementando su constructor
y el método "getTelemetryValue" dentro de su clase. La estructura es muy similar a los módulos ya implementados como 
"SystemCpuUtilTask" y "SystemMemUtilTask").

En esta sección, se ha ejecutado el test de integración "SystemPerformanceManagerTest", donde se puede observar en el 
output como se ofrecen los valores de uso de cpu, memoria y disco (muy similar al output ofrecido cuando se ejecutó el 
test en la implementación de PIOT-CDA-02-007).

PIOT-CDA-05-002 -> Se ha editado el módulo "DataUtil", modificando los métodos establecidos en la clase del módulo para 
poder convertir cualquier ActuatorData, SensorData y SystemPerformanceData en formato JSON y el proceso inverso. 
Por otro lado, también se han implementado un seguido de métodos privados de la clase denominados 
"_formatDataAndLoadDictionary", "_generateJsonData" y "_updateIotData", para utilizar métodos propios de la librería 
json para crear un JsonData, podder formatearlo y cargarlo el json y, por último, actualizar los valores presentes en 
el json.

En esta sección, se ha ejecutado el test unitario "DataUtilTest" y el test de integración "DataIntegrationTest", los 
cuales pasan correctamente pero en el de integración se ha tenido que skippear los tests que se tratan de leer desde 
un JSON (ESTO SE DEBERÁ VER POR QUÉ SE DEBE HACER ASÍ, PORQUE LA EJECUCIÓN DE ESTOS TESTS ESTÁN LIGADOS CON EL GDA, 
QUIZÁS AL ACABAR ESTA SECCIÓN CON EL GDA SE EJECUTEN CON TODA NORMALIDAD).

PIOT-CDA-05-003 -> Requisito opcional, no implementado en la realización de la práctica.

PIOT-CDA-05-004 -> Requisito opcional, no implementado en la realización de la práctica.

PIOT-CDA-05-100 -> Se ha llevado a cabo el merge de la rama labmodule05 a la rama main o default para comenzar la 
siguiente sección.

### Code Repository and Branch

NOTE: Be sure to include the branch.

URL: https://github.com/NicolGallo/PIC_Python_Components/tree/labmodule05


### Unit Tests Executed

NOTE: The instructor will execute your unit tests. You only need to list each test case below
(e.g. ConfigUtilTest, DataUtilTest, etc). Be sure to include all previous tests, too,
since you need to ensure you haven't introduced regressions.

- DataUtilTest
- 
- 

### Integration Tests Executed

NOTE: The instructor will execute most of your integration tests using their own environment, with
some exceptions (such as your cloud connectivity tests). In such cases, they'll review
your code to ensure it's correct. As for the tests you execute, you only need to list each
test case below (e.g. SensorSimAdapterManagerTest, DeviceDataManagerTest, etc.)

- SystemPerformanceManagerTest
- DataIntegrationTest
- 

EOF.
