# Constrained Device Application (Connected Devices)

## Lab Module 03

Be sure to implement all the PIOT-CDA-* issues (requirements).

### Description

NOTE: Include two full paragraphs describing your implementation approach by answering the questions listed below.

What does your implementation do?

La implementación permite gestionar datos de sensores y actuadores mediante clases específicas que heredan 
funcionalidades básicas, manejando información acerca de la humedad, temperatura y presión. Además, incorpora 
emuladores que simulan el comportamiento del hardware real (simulando captación de datos), 
y el módulo DeviceDataManager coordina todo el procesamiento, gestionando la comunicación y ejecución. 
Finalmente, se procede a modificar la aplicación principal para facilitar la gestión y visualización de los datos 
desde la misma.

How does your implementation work?

A continuación, se detalla el procedimiento seguido para implementar los requisitos establecidos en el Lab Module 03:

PIOT-CDA-03-000 -> Creada una nueva rama denominada labmodule03 para proceder a implementar los requisitos necesarios 
de esta sección.

PIOT-CDA-03-001 -> Se ha editado el módulo ActuatorData (el cual funciona como un actuador de datos resultando útil su 
función para enviar mensajes de texto al display de un dispositivo). Primero, se ha modificado el constructor de la 
clase añadiendo 3 variables (value, command y stateData). Los getters y setters también han sido implementados para 
cada variable así como el método privado "_handleUpdateData" (el cual es un método abstracto definido en la clase 
BaseIotData) que contendrá la instancia de ActuatorData que definirá los datos de value, command y stateData. 
Por último, se ha implementado el método __str__(self) para ofrecer una mejor representación de los 
parámetros de ActuatorData.

Seguidamente, se ha editado el módulo SensorData, el cual también hereda de BaseIotData y actúa como un simple sensor o 
recopilador de datos. En dicho módulo también se ha editado el constructor de la clase añadiendo la variable "value" 
así como su método get y set, la implementación del método "_handleUpdateData" y del método __str__(self) para ofrecer 
una representación detallada del sensorData.

Posteriormente, se ha efectuado el mismo procedimiento en el módulo SystemPerformanceData editando el constructor con 
las de cpuUtil, memUtil y diskUtil, para evaluar la cantidad de CPU, memoria y disco utilizado. Se han implementado los 
getters y setters correspondientes, el método "_handleUpdateData"y el método __str__(self).

Por último, se han ejecutado los tests unitarios "ActuatorDataTest", "SensorDataTest" y "SystemPerformanceDataTest", 
los cuales todos pasan correctamente imprimiendo los datos establecidos en el método __str__ de la clase BaseIotData y 
de las subclases anteriores.

PIOT-CDA-03-002 -> Se ha editado el módulo BaseSensorSimTask, añadiendo al constructor de la clase las variables 
dataSet, name, typeID, dataSetIndex y useRandomizer. A continuación, se ha implementado los métodos getName y getTypeID.
Por otro lado, se ha implementado el método generateTelemetry y getTelemetry, con los cuales se podrá obtener el 
valor actual del sensorData. No se ha ejecutado ningún test en esta sección.

PIOT-CDA-03-003 -> Se ha editado los módulos HumiditySensorSimTAsk, PressureSensorSimTAsk y TemperatureSensorSimTAsk 
(en que todos heredan de BaseSensorSimTask). En todos los módulos, se ha implementado el constructor correspondiente 
para cada clase añadiendo las variables name, typeID, dataSet, minVAl y maxVal.
También, se han ejecutado los tests unitarios "HumiditySensorSimTaskTest", "PressureSensorSimTaskTest" y 
"TemperatureSensorSimTaskTest". Estos se ejecutan correctamente ofreciendo en cada output los parámetros propios de 
cada tipo de sensor así el valor de medición dado para probar el test.

PIOT-CDA-03-004 -> Se ha editado el módulo BaseActuatorSimTask, añadiendo en primera instancia, las variables name, 
typeID, simpleName (utilizado solamente para realizar el logging), lastknownCommand (utilizado para almacenar el 
último comando ejecutado) y lastKnownValue (utilizado para almacenar el último valor aplicado).
Seguidamente, se ha implementado el método privado "_ActivateActuator" y "_deactivateActuator" para proporcionar un 
log informativo acerca de la puesta en ON y OFF del actuador, respectivamente.

Por último, se ha implementado el método "updateActuator", el cual procesa los comandos para el actuador devolviendo 
una respuesta con su estado actualizado. Si el comando resulta ser ON u OFF (un comando válido), procederá a activar 
o desactivar el actuador. Si el comando resulta ser inválido, se registrará el error asignando el código de error por 
defecto. En una última instancia, se crea un objeto de tipo ActuadorData, copiando los datos originales y actualizando 
el estado (permitiendo a la aplicación gestionar el actuador y confirmar así la ejecución del comando).

En esta sección, no se ha ejecutado ningún tipo de test.

PIOT-CDA-03-005 -> Se han editado los módulos "HumidifierActuatorSimTask" y "HvacActuatorSimTask", en que ambos heredan
de la clase BaseActuatorSimTAsk. En ambos módulos, se ha implementado el constructor de las respectivas clases, 
añadiendo las variables name, typeID y simpleName.

En esta sección, se han ejecutado los tests unitarios "HumidifierActuatorSimTaskTest" y "HvacActuatorSimTaskTest", 
pasando correctamente obteniendo en la consola los valores de los actuadores, los parámetros característicos detallados
de estos y la visualización de ON u OFF en caso de si se activa o se desactiva el actuador.

PIOT-CDA-03-006 -> Se ha editado el módulo "SensorAdapterManager, la cual está enfocada en la gestión de simuladores 
(o con los emuladores que se implementarán más adelante). Para ello, se ha implementado un constructor con las 
variables useEmulator, pollRate y locationID para poder recuperar ciertas propiedades del archivo de configuración del 
sistema. En adición, se han implementado los métodos "setDataMessageListener", "startManager" y "stopManager", para 
poder mostrar diferentes logs informativos acerca del estado del SensorAdapterManager.
Por otro lado, se ha implementado el método "handleTelemetry", el cual se ejecutará según la frecuencia de muestreo 
establecido (pollRate). En cada una de las tareas de los sensores se generan datos de telemetría, se asigna el ID de 
ubicación a cada instancia de SensorData generada y luego se pasa la referencia al escuchador de mensajes (listener) de
datos para su procesamiento.

Por último, se ha implementado un nuevo método "_initEnvironmentalSensorTasks", con el cual se procede a crear la tarea 
del simulador de los sensores.

En esta sección, se ha ejecutado todos los tests unitarios de la part02 en que todos pasan correctamente imprimiendo 
por consola todos los datos pertinentes a los sensores implementados en pasos anteriores (se ejecutan todos 
correctamente menos el test "DataUtilTest" que será implementado en etapas posteriores) y el test de integración 
"SensorAdapterManagerTest", en que se ejecuta correctamente observando datos generados por los sensores simulados en 
sus diferentes jobs.

PIOT-CDA-03-007 -> Se ha editado el módulo "ActuatorAdapterManager", el cual es muy similar al anterior pero se 
implementan propiedades características de actuadores en vez de sensores. Se ha implementado el constructor de la clase
así como los métodos "sendActuatorCommand" (encargado de activar acciones validando el valor de la respuesta del 
actuador y que locationID sea igual a la configurada en la aplicación. En caso de fallar la validación o chequeo, no 
se ejecutará la acción indicándose mediante un log informativo), "setDataMessageListener" y 
"_initEnvironmentalActuationTasks" (encargado de cargar el entorno de las tareas de un actuador simulado y de crear 
el actuador HVAC).

En esta sección, se han ejecutado todos los tests unitarios como en la sección anterior (PIOT-CDA-03-006) menos el test 
"DataUtilTest" y el test de integración "ActuatorAdapterManagerTest", ejecutándose todos correctamente pudiendo 
observar por consola los valores de los actuadores así como diferentes logs informativos de los mismos.

PIOT-CDA-03-008 -> Se ha editado el módulo "DeviceDataManager", el cual corresponde al núcleo del CDA elaborado, 
procesando los datos en la aplicación y dirigiendo todas las solicitudes al destino apropiado. Primero, se han editado 
diferentes propiedades y constantes en la configuración del CDA en los módulos "PiotConfig" y "ConfigConst".

A continuación, se ha procedido a editar la clase DeviceDataManager añadiendo nuevas instancias del 
SystemPerformanceManager, del SensorAdapterManager y del ActuatorAdapterManager, así como la recuperación de las 
diferentes flags de habilitación de actuación editadas anteriormente en la configuración del CDA.

Por otro lado, se han implementado los métodos "startManager" y "stopManager" para arrancar y parar el 
SystemPerformanceManager y el SensorAdapterManager con logs informativos correspondientes de cada uno. También, se ha 
implementado la lógica de los diferentes métodos públicos ("handleActuatorCommandMessage", 
"handleActuatorCommandResponse", "handleIncomingMessage", "handleSensorMessage" y "handleSystemPerformanceMessage") de 
la clase que serán utilizados más adelante como callback methods (métodos de devolución de llamada).

En esta sección, se ha ejecutado el test de integración "DeviceDataManagerNoCommsTest" pasando correctamente y 
obteniendo información acerca de todos los sensores y actuadores del sistema.

PIOT-CDA-03-009 -> Se ha editado el módulo "ConstrainedDeviceApp" añadiendo al constructor de la clase una instancia 
del DeviceDataManager y, posteriormente, modificando los métodos startApp y stopApp para llamar a los métodos propios 
del DeviceDataManager como "startManager" y "stopManager".

En esta sección, se ha ejecutado el test de integración "ConstrainedDeviceAppTest", pasando correctamente y pudiendo 
observar los diferentes logs informativos como cuando comienza y termina el CDA, lo mismo con el DeviceDataManager, el 
SystemPerformanceManage, el SensorAdapterManager, también se observa en el momento que el scheduler o planificador está 
en búsqueda de correr nuevos jobs o trabajos y cuando no detecta más jobs se detiene el CDA.

PIOT-CDA-03-100 -> Se ha llevado a cabo el merge de la rama labmodule03 a la rama main o default para comenzar la
siguiente sección Lab Module 04.

### Code Repository and Branch

NOTE: Be sure to include the branch.

URL: https://github.com/NicolGallo/PIC_Python_Components/tree/labmodule03

### Unit Tests Executed

NOTE: The instructor will execute your unit tests. You only need to list each test case below
(e.g. ConfigUtilTest, DataUtilTest, etc). Be sure to include all previous tests, too,
since you need to ensure you haven't introduced regressions.

- ActuatorDataTest
- SensorDataTest
- SystemPerformanceDataTest
- HumiditySensorSimTaskTest
- PressureSensorSimTaskTest
- TemperatureSensorSimTaskTest
- HumidifierActuatorSimTaskTest
- HvacActuatorSimTaskTest

### Integration Tests Executed

NOTE: The instructor will execute most of your integration tests using their own environment, with
some exceptions (such as your cloud connectivity tests). In such cases, they'll review
your code to ensure it's correct. As for the tests you execute, you only need to list each
test case below (e.g. SensorSimAdapterManagerTest, DeviceDataManagerTest, etc.)

- ConstrainedDeviceAppTest
- SensorAdapterManagerTest
- ActuatorAdapterManagerTest
- DeviceDataManagerNoCommsTest

EOF.
