# Constrained Device Application (Connected Devices)

## Lab Module 02

Be sure to implement all the PIOT-CDA-* issues (requirements).

### Description

NOTE: Include two full paragraphs describing your implementation approach by answering the questions listed below.

What does your implementation do?

Permite gestionar y monitorizar el rendimiento del sistema mediante la definición de módulos que obtienen 
métricas como el uso de CPU y memoria. Estos módulos se integran, posteriormente, al SystemPerformanceManager, que 
ejecuta las tareas regularmente usando la librería apscheduler. El módulo principal (ConstrainedDeviceApp) controla el 
arranque y finalización del manager.

How does your implementation work?

Los siguientes apartados detallan en medida lo efectuado en cada paso para cumplir los requisitos establecidos en el 
Lab Module 02:

PIOT-CDA-02-000 -> Creada la nueva rama denominada labmodule02.

PIOT-CDA-02-001 -> Para crear el nuevo módulo ConstrainedDeviceApp se ha mantenido la arquitectura proporcionada por el 
código fuente. 

En esta sección, se han ejecutado el test unitario 'ConfigUtilTest' y el test de integración "ConstrainedDeviceAppTest" 
los cuales pasan correctamente.

PIOT-CDA-02-002 -> Para crear el nuevo módulo SystemPerformanceManager se ha aprovechado la arquitectura ya 
proporcionada y se ha implementado el constructor de la clase así como la implementación de los métodos startManager y 
stopManager para visualizar los prints de información.

En esta sección, se ha ejecutado el test de integración 'SystemPerformanceManagerTest' el cual pasa correctamente.

PIOT-CDA-02-003 -> Dentro del CDA, se implementa una instancia del SystemPerformanceManager para conectar ambos módulos 
de la arquitectura y se ha editado los métodos de startApp y stopApp con la información de los logs correspondientes 
para visualizar el momento en que el CDA arranca y finaliza, así como el arranque y la finalización del 
SystemPerformanceManager. 

En esta sección, se ha ejecutado el test de integración 'ConstrainedDeviceAppTest' el cual pasa correctamente generando 
el output esperado a partir del observado en las notas del Notion.

PIOT-CDA-02-004 -> Se ha añadido dos parámetros al constructor de la clase BaseSystemUtilTask, así como dos métodos get 
para cada parámetro establecido (name y typeID). Por otro lado, el método 'getTelemetryValue' se ha dejado tal y como 
ha sido proporcionado en el código fuente debido a que se implementará en fases posteriores.

También, en esta sección ningún test ha sido requerido ejecutar.

PIOT-CDA-02-005 -> Se ha implementado la clase SystemCpuUtilTask, la cual nos permitirá recolectar métricas 
correspondientes al uso de CPU del sistema local. Para ello, se ha definido el método 'getTelemetryValue' 
que en el anterior paso se dejó sin implementar.

En esta sección, se ha ejecutado el test unitario "SystemCpuUtilTaskTest" para comprobar el correcto funcionamiento 
de la clase editada, el cual pasa con éxito indicando el porcentaje de CPU que se ha utilizado.

PIOT-CDA-02-006 -> Se ha implementado la clase SystemMemUtilTask, la cual nos permitirá recolectar métricas 
correspondientes al uso de la memoria del sistema local. Para ello, se ha definido el método 'getTelemetryValue' para 
que devuelva el porcentaje de memoria virtual.

En esta sección, se ha ejecutado el test unitario "SystemMemUtilTaskTest" para comprobar el correcto funcionamiento
de la clase editada, el cual pasa con éxito indicando el uso de memoria empleada.

PIOT-CDA-02-007 -> Se ha conectado tanto el task asociado a la CPU y la memoria al SystemPerformanceManager. A su vez, 
se ha utilizado en la implementación de dicha clase la librería 'apscheduler', que permite ejecutar las dos tasks 
implementadas en PIOT-CDA-02-005 y PIOT-CDA-02-006 en intervalos regulares de tiempo. El SystemPerformanceManager 
permite también poder arrancar y finalizar el monitoreo de las tareas que estarán recolectando los datos o métricas 
pertinentes.

En esta sección, se ha ejecutado el test de integración 'SystemPerformanceManagerTest' el cual pasa correctamente 
generando un output donde se visualiza los diferentes jobs (o trabajos) en diferentes intervalos de tiempo de las 
medidas de las métricas de CPU y memoria utilizada por el sistema local.

PIOT-CDA-02-100 -> Se ha realizado el merge a la rama master o principal lo implementado en la rama labmodule2. 
Por otro lado, se ha comprobado que todos los tests de integración y unitarios de la part01 se ejecutan y pasan 
correctamente.

### Code Repository and Branch

NOTE: Be sure to include the branch.

URL: https://github.com/NicolGallo/PIC_Python_Components/tree/labmodule02

### Unit Tests Executed

NOTE: The instructor will execute your unit tests. You only need to list each test case below
(e.g. ConfigUtilTest, DataUtilTest, etc). Be sure to include all previous tests, too,
since you need to ensure you haven't introduced regressions.

- ConfigUtilTest
- SystemCpuUtilTaskTest
- SystemMemUtilTaskTest

### Integration Tests Executed

NOTE: The instructor will execute most of your integration tests using their own environment, with
some exceptions (such as your cloud connectivity tests). In such cases, they'll review
your code to ensure it's correct. As for the tests you execute, you only need to list each
test case below (e.g. SensorSimAdapterManagerTest, DeviceDataManagerTest, etc.)

- ConstrainedDeviceAppTest
- SystemPerformanceManagerTest
- 

EOF.
