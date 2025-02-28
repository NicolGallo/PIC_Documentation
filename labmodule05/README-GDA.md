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

PIOT-GDA-05-002 -> 
PIOT-GDA-05-003 -> 
PIOT-GDA-05-004 -> 
PIOT-GDA-05-005 ->
PIOT-GDA-05-006 ->
PIOT-GDA-05-007 ->
PIOT-GDA-05-008 -> 
PIOT-GDA-05-100 -> 

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

### Integration Tests Executed

NOTE: The instructor will execute most of your integration tests using their own environment, with
some exceptions (such as your cloud connectivity tests). In such cases, they'll review
your code to ensure it's correct. As for the tests you execute, you only need to list each
test case below (e.g. SensorSimAdapterManagerTest, DeviceDataManagerTest, etc.)

- 
- 
- 

EOF.
