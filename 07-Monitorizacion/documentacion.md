# Monitorización del dominio

Esta sección documenta los mecanismos y herramientas utilizados para supervisar el estado del dominio, sus servicios y los equipos que forman parte del entorno. La monitorización permite detectar problemas, anticipar fallos y mantener la estabilidad del sistema.

## Objetivo de esta sección

Establecer un sistema de supervisión que permita controlar el rendimiento, disponibilidad y seguridad del dominio, asegurando que los servicios críticos funcionan correctamente y que cualquier incidencia pueda ser detectada y atendida a tiempo.

## Monitorización básica con el Visor de eventos

El Visor de eventos es la herramienta principal para revisar el estado del sistema, detectar errores, advertencias y eventos críticos dentro del dominio. Permite supervisar tanto el controlador de dominio como los equipos cliente, ofreciendo información detallada sobre el funcionamiento del entorno.

### Pasos realizados

1. Se abre el **Visor de eventos** desde el controlador de dominio.
2. Se revisan los registros principales:
   - **Aplicación**
   - **Seguridad**
   - **Sistema**
   - **DNS Server**
   - **Directory Service**
   - **File Replication Service**
3. Se identifican eventos relevantes como:
   - Errores de autenticación.
   - Fallos de servicios.
   - Problemas de replicación.
   - Advertencias relacionadas con DNS o Active Directory.
4. Se filtran los eventos para facilitar la búsqueda de incidencias específicas.
5. Se exportan eventos importantes cuando es necesario documentar fallos o incidencias.
6. Se revisa periódicamente el estado del controlador de dominio para asegurar que no existan errores críticos.
7. Se comprueba también el Visor de eventos en equipos cliente para detectar:
   - Problemas de políticas de grupo.
   - Fallos de red.
   - Errores de inicio de sesión.
8. Se utiliza esta información para anticipar problemas y mantener la estabilidad del entorno.

### Objetivo de este paso

Supervisar el estado del dominio mediante la revisión de eventos del sistema, permitiendo detectar fallos, advertencias y comportamientos anómalos antes de que afecten al funcionamiento general del entorno.

## Monitorización de servicios con PowerShell

PowerShell permite supervisar el estado de los servicios del dominio de forma rápida y automatizada. Con comandos como `Get-Service`, es posible comprobar si los servicios críticos están en ejecución y detectar fallos antes de que afecten al funcionamiento del entorno.

### Pasos realizados

1. Se abre una consola de **PowerShell** en el controlador de dominio.
2. Se revisa el estado de los servicios principales del sistema:
  Get-Service

3. Se comprueba específicamente el estado de servicios críticos como:
- Active Directory Domain Services (`NTDS`)
- DNS Server (`DNS`)
- DHCP Server (`DHCPServer`)
- Servicio de tiempo (`W32Time`)
- Servicio de replicación (`NTFRS` o `DFSR`)
4. Para verificar un servicio concreto, se utiliza:
  Get-Service -Name nombre_servicio

5. Si un servicio aparece detenido, se intenta iniciar:
  Start-Service -Name nombre_servicio

6. Para detener un servicio (solo en pruebas controladas):
  Stop-Service -Name nombre_servicio

7. Se crea un pequeño script para revisar automáticamente los servicios críticos:
$servicios = "DNS","DHCPServer","W32Time","NTDS"
  Get-Service -Name $servicios

8. Se ejecuta periódicamente para asegurar que todos los servicios están funcionando correctamente.
9. Si se detecta un fallo recurrente, se revisa el Visor de eventos para obtener más información.

### Objetivo de este paso

Supervisar el estado de los servicios esenciales del dominio mediante PowerShell, permitiendo detectar fallos rápidamente y mantener la estabilidad del entorno.

## Monitorización del rendimiento con el Monitor de recursos

El Monitor de recursos permite supervisar en tiempo real el rendimiento del sistema, mostrando información detallada sobre CPU, memoria, disco y red. Es una herramienta esencial para detectar cuellos de botella, procesos problemáticos y comportamientos anómalos en el controlador de dominio o en cualquier equipo del entorno.

### Pasos realizados

1. Se abre el **Monitor de recursos** desde el menú de herramientas administrativas o mediante:
  resmon.exe

2. Se revisa el estado de los cuatro componentes principales:
- **CPU**: procesos que consumen demasiados recursos.
- **Memoria**: uso de RAM y posibles fugas de memoria.
- **Disco**: actividad de lectura/escritura y procesos que generan carga excesiva.
- **Red**: conexiones activas, latencia y tráfico generado por servicios.
3. Se identifican procesos que afectan negativamente al rendimiento del controlador de dominio.
4. Se comprueba que los servicios críticos (DNS, AD DS, DHCP, etc.) no generan carga anormal.
5. Se revisan los gráficos en tiempo real para detectar picos de actividad.
6. Se utiliza la pestaña **CPU → Servicios** para correlacionar procesos con servicios específicos.
7. Se monitoriza la actividad de disco para detectar:
- Problemas con la base de datos de Active Directory.
- Cargas excesivas en WSUS.
8. Se analiza el tráfico de red para identificar:
- Equipos que generan demasiadas solicitudes.
- Problemas de comunicación con otros controladores de dominio.
9. Se utiliza esta información para anticipar problemas de rendimiento y planificar mejoras.

### Objetivo de este paso

Supervisar el rendimiento del sistema en tiempo real, detectando procesos o servicios que puedan afectar la estabilidad del dominio y permitiendo actuar antes de que se produzcan fallos.

## Monitorización avanzada con Performance Monitor

Performance Monitor permite crear conjuntos de recopiladores de datos y analizar métricas detalladas del sistema a largo plazo. Es una herramienta avanzada para detectar problemas de rendimiento, analizar tendencias y evaluar la salud del controlador de dominio y otros equipos del entorno.

### Pasos realizados

1. Se abre **Performance Monitor** desde las herramientas administrativas o ejecutando:
  perfmon.exe

2. Se revisa la vista en tiempo real de contadores como:
- Uso de CPU
- Memoria disponible
- Actividad de disco
- Latencia de red
3. Se agregan contadores específicos para servicios críticos:
- Active Directory: `NTDS`
- DNS Server: consultas por segundo
- Disco: `Avg. Disk Queue Length`
- Memoria: `Pages/sec`
4. Se crea un **Conjunto de recopiladores de datos**:
- Se selecciona *Conjuntos de recopiladores de datos → Definidos por el usuario*.
- Se crea un nuevo conjunto basado en plantillas o personalizado.
5. Se configuran los intervalos de muestreo (por ejemplo, cada 15 segundos).
6. Se define la ubicación donde se guardarán los registros.
7. Se inicia el recopilador para comenzar a registrar datos.
8. Tras un periodo de monitorización, se revisan los informes generados:
- Gráficos de rendimiento
- Tendencias de uso
- Picos de carga
9. Se analizan los resultados para identificar:
- Saturación de CPU
- Falta de memoria
- Problemas de disco
- Latencia en servicios del dominio
10. Se utiliza esta información para planificar mejoras o resolver incidencias de rendimiento.

### Objetivo de este paso

Obtener una monitorización avanzada y detallada del rendimiento del sistema, permitiendo analizar tendencias, detectar problemas complejos y optimizar la infraestructura del dominio.

## Estado de la monitorización del dominio

La monitorización del dominio queda establecida mediante el uso del Visor de eventos, PowerShell, el Monitor de recursos y Performance Monitor.  
Estas herramientas permiten supervisar el estado del sistema, detectar incidencias, analizar el rendimiento y anticipar problemas antes de que afecten a los servicios críticos del entorno.






