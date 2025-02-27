# Constrained Device Application (Connected Devices)

## Lab Module 05

Be sure to implement all the PIOT-CDA-* issues (requirements).

### Description

NOTE: Include two full paragraphs describing your implementation approach by answering the questions listed below.

What does your implementation do? 

How does your implementation work?

A continuación, se detalla el procedimiento seguido para implementar los requisitos establecidos en el Lab Module 05:

PIOT-CDA-05-000 -> Se ha creado una nueva rama denominada labmodule05 para comenzar la realización de la presente sección.

PIOT-CDA-05-001 -> Se ha editado el módulo "SystemPerformanceManagerpara poder implementar el almacenamiento de los 
datos recopilados por el sistema de rendimiento. Para ello, dentro de la clase del módulo, se ha editado el método 
"handleTelemetry" incluyendo la inicialización de una instancia de tipo SystemPerformanceData, la cual permitirá 
obtener los datos de uso de CPU y memoria.

Opcionalmente, se ha añadido dentro del método "handleTelemetry" dentro de la clase SystemPerformanceManager para que, 
en adición. a parte de la recopilación del uso de CPU y memoria, se recopile el uso de disco. Para ello, también se ha 
implementado un nuevo módulo denominado SystemDiskUtilTask para llevar a cabo dicha tarea (implementando su constructor
y el método "getTelemetryValue" dentro de su clase. La estructura es muy similar a los módulos ya implementados como 
"SystemCpuUtilTask" y "SystemMemUtilTask").

En esta sección, se ha ejecutado el test de integración "SystemPerformanceManagerTest", donde se puede observar en el 
output como se ofrecen los valores de uso de cpu, memoria y disco (muy similar al output ofrecido cuando se ejecutó el 
test en la implementación de PIOT-CDA-02-007).

PIOT-CDA-05-002 ->

PIOT-CDA-05-003 -> Requisito opcional, no implementado en la realización de la práctica.

PIOT-CDA-05-004 -> Requisito opcional, no implementado en la realización de la práctica.

PIOT-CDA-05-005 -> 

### Code Repository and Branch

NOTE: Be sure to include the branch.

URL: 


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

- SystemPerformanceManagerTest
- 
- 

EOF.
