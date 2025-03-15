# Gateway Device Application (Connected Devices)

## Lab Module 02

Be sure to implement all the PIOT-GDA-* issues.

### Description

NOTE: Include two full paragraphs describing your implementation approach by answering the questions listed below.

What does your implementation do?

Permite recopilar y gestionar datos sobre rendimiento del sistema, obteniendo métricas como la carga de CPU y memoria. 
Define tareas específicas, conectando dichas tareas con un gestor centralizado (SystemPerformanceManager) que programa 
su ejecución periódica, y genera registros de información.

How does your implementation work?

Los siguientes apartados detallan en medida lo efectuado en cada paso del GDA para cumplir los requisitos establecidos 
en el Lab Module 02:

PIOT-GDA-02-000 -> Se ha creado una nueva rama denominada labmodule02.

PIOT-GDA-02-001 -> Para crear el nuevo módulo GatewayDeviceApp se ha mantenido la arquitectura proporcionada por el 
código fuente de la práctica.

En esta sección, se han ejecutado todos los tests unitarios del módulo "ConfigUtilTest" observando que todos pasan 
correctamente. Del mismo modo, se ha ejecutado el test de integración del módulo "GatewayDeviceAppTest" y pasa 
correctamente obteniendo un output al indicado en las notas.

PIOT-GDA-02-002 -> Se ha editado el módulo "SystemPerformanceManager" que será responsable de programar tareas de recopilación 
de datos sobre el rendimiento del sistema. En el módulo, se ha añadido la variable estática "pollRate" y una variable 
de logging. Por otro lado, se ha implementado los métodos startManager y stopManager para enseñar información o logs 
sobre si el SystemPerformanceManager se ha iniciado o se ha detenido. Se ha implementado el constructor de la clase 
obteniendo el valor de pollRate mediante el valor de la propiedad ConfigConst.POLL_CYCLES_KEY desde la sección 
ConfigConst.GATEWAY_DEVICE del módulo de configuración de la aplicación, utilizando ConfigUtil. Si la propiedad no 
está definida, se usa ConfigConst.DEFAULT_POLL_CYCLES como valor predeterminado.

En esta sección, se ha ejecutado el test de integración "SystemPerformanceManagerTest" el cual pasa correctamente 
obteniendo un output como el indicado en las notas.

PIOT-GDA-02-003 -> Se ha conectado el SystemPerformanceManager con el GatewayDeviceApp para proceder a arrancarlo y pararlo 
con la aplicación. Para ello, se ha implementado en el constructor del GatewatDeviceApp una instancia del 
SystemPerformanceManager y se ha editado los métodos startApp y stopAdd para visualizar nuevos logs de información 
al lanzar la aplicación llamando a los métodos startManager y stopManager. 

En esta sección, se ha ejecutado el test de integración "GatewayDeviceAppTest" obteniendo un output como el indicado en 
las notas.

PIOT-GDA-02-004 -> Se ha editado el módulo BaseSystemUtilTask en que será la clase base que contendrá la funcionalidad 
central que heredarán todas las demás tareas de rendimiento del sistema. Se han añadido dos variables privadas 
(name y typeID), las cuales se pasaran como parámetros al constructor de la clase.

Por otro lado, en el módulo se han implementado dos métodos get (getName y getTypeID) y un método abstracto 
"getTelemetryValue", en que este último será implementado y definido por las diferentes tareas que hereden del módulo 
creado. 

En esta sección, no se ha procedido ejecutar ningún test.

PIOT-GDA-02-005 -> Se ha editado el módulo SystemCpuUtilTask en que recolectará las métricas empleadas sobre la CPU del 
sistema local. Para ello, se ha implementado el método abstracto getTelemetryValue definido en BaseSystemUtilTask. 
Para acceder a información sobre el sistema operativo y el rendimiento del sistema se crea una instancia del tipo 
OperatingSystemMXBean, en que con aplicarle el método "getSystemLoadAverage" se obtiene el valor promedio de carga 
del sistema en el último minuto.

En esta sección, se ha ejecutado el test unitario "SystemCpuUtilTaskTest", el cual pasa correctamente visualizando el 
valor de CPU utilizada por el sistema.

PIOT-GDA-02-006 -> Editado el módulo SystemMemUtilTask en que recolectará las métricas empleadas sobre la memoria del 
sistema local. Para ello, se ha implementado el método abstracto getTelemetryValue definido en BaseSystemUtilTask. 
Para acceder a los detalles sobre el uso de la memoria heap se obtiene una instancia del tipo MemoryUsage, con el cual 
se obtendrá el valor de memoria utilizada por el sistema y el valor de cantidad máxima de memoria asignada a la heap de 
la máquina virtual de Java (JVM), y con ellos se calcula el porcentaje de uso de memoria. 

En esta sección, se ha ejecutado el test unitario "SystemMemUtilTaskTest", el cual pasa correctamente visualizando 
el valor de memoria utilizada por el sistema.

PIOT-GDA-02-007 -> Conectados los módulos SystemCpuUtilTask y SystemMemUtilTask con el SystemPerformanceManager para 
permitir a este último poder arrancar y detener el monitoreo de las diferentes tareas de rendimiento. Para ello, se ha 
editado el módulo SystemPerformanceManager implementando un seguido de variables privadas a la clase. Por otro lado, 
también se ha implementado el método "handleTelemetry", el cual incluye llamadas para recuperar las métricas de 
utilización de CPU y memoria.

Posteriormente, se ha editado el constructor de la clase creando instancias de los módulos de tareas editados en los pasos
anteriores. Por último, se ha editado los métodos startManager y stopManager invocando el método "scheduleAtFixedRate" 
para comenzar y detener el planificador de tareas.

En esta sección, se ha ejecutado el test de integración "GatewayDeviceAppTest", el cual se ejecuta correctamente 
proporcionando un output de acorde al especificado en las notas.

PIOT-GDA-02-100 -> Se ha efectuado el merge de la rama labmodule2 a la rama default o main.

### Code Repository and Branch

NOTE: Be sure to include the branch.

URL: https://github.com/NicolGallo/PIC_Java_Components/tree/labmodule2


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

- GatewayDeviceAppTest
- SystemPerformanceManagerTest
- 

EOF.
