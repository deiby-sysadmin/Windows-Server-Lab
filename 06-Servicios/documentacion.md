## Servicio DNS en el dominio

El servicio DNS es fundamental para el funcionamiento del dominio, ya que permite resolver nombres de equipos, servicios y recursos dentro de la red. Sin DNS, los equipos no podrían localizar el controlador de dominio ni otros servicios esenciales.

### Pasos realizados

1. Se abre el Administrador del servidor en el controlador de dominio.
2. Se verifica que el rol **DNS** esté instalado junto con el rol de **Servicios de dominio de Active Directory (AD DS)**.
3. Se accede a la consola **DNS** para revisar la configuración inicial.
4. Se comprueba la existencia de las zonas principales:
   - Zona de búsqueda directa del dominio.
   - Zona de búsqueda inversa (si se configuró).
5. Se validan los registros esenciales:
   - Registros **A** de los equipos del dominio.
   - Registros **SRV** utilizados por Active Directory.
6. Se comprueba que el controlador de dominio actúa como servidor DNS principal.
7. Se verifica que los equipos del dominio utilizan la IP del controlador de dominio como servidor DNS.
8. Se realiza una prueba de resolución con:
  nslookup (nombre_equipo)

9. Se confirma que la resolución funciona correctamente.

### Objetivo de este paso

Garantizar que el servicio DNS está correctamente configurado y operativo, permitiendo que el dominio funcione de manera estable y que los equipos puedan localizar recursos internos sin problemas.

## Servicio DHCP en el dominio

El servicio DHCP permite asignar direcciones IP automáticamente a los equipos del dominio, garantizando una configuración de red coherente y centralizada. Su correcta implementación evita conflictos de IP y facilita la administración del entorno.

### Pasos realizados

1. Se abre el **Administrador del servidor** en el controlador de dominio.
2. Se verifica que el rol **DHCP** esté instalado.
3. Se accede a la consola **DHCP** para revisar la configuración inicial.
4. Se crea un nuevo ámbito (scope) definiendo:
   - Rango de direcciones IP.
   - Máscara de subred.
   - Puerta de enlace predeterminada.
   - Servidores DNS (normalmente la IP del controlador de dominio).
5. Se configuran las opciones del ámbito:
   - Duración del alquiler (lease).
   - Exclusiones de IP para evitar conflictos con servidores u otros equipos estáticos.
6. Se activa el ámbito para que comience a asignar direcciones IP.
7. Se autoriza el servidor DHCP dentro del dominio para que pueda operar correctamente.
8. En un equipo cliente, se ejecuta:
  ipconfig /renew

para obtener una IP desde el servidor DHCP.
9. Se verifica que la IP asignada pertenece al ámbito configurado.
10. Se comprueba la conectividad y resolución DNS para confirmar que la configuración es correcta.

### Objetivo de este paso

Proveer una asignación automática y centralizada de direcciones IP dentro del dominio, asegurando una red organizada, sin conflictos y fácil de administrar.

## Servicio NTP (sincronización horaria)

El servicio NTP garantiza que todos los equipos del dominio mantengan la misma hora. Esto es fundamental para la autenticación Kerberos, la auditoría y el funcionamiento correcto de Active Directory. Una diferencia de tiempo superior a 5 minutos puede causar fallos de inicio de sesión y errores de comunicación.

### Pasos realizados

1. Se verifica que el controlador de dominio actúa como servidor NTP principal del entorno.
2. En el controlador de dominio, se comprueba la configuración del servicio de tiempo con:
  w32tm /query /status

3. Se configura el controlador de dominio para sincronizarse con servidores NTP externos fiables, por ejemplo:
- `time.windows.com`
- `pool.ntp.org`
4. Se establece la configuración con:
  w32tm /config /manualpeerlist:"time.windows.com" /syncfromflags:manual /reliable:yes /update

5. Se reinicia el servicio de tiempo:
  net stop w32time
  net start w32time

6. En los equipos del dominio, se verifica que utilizan al controlador de dominio como fuente de tiempo:
  w32tm /query /source

7. Se fuerza la sincronización si es necesario:
  w32tm /resync

8. Se comprueba que todos los equipos mantienen una hora coherente dentro del dominio.

### Objetivo de este paso

Garantizar que todos los equipos del dominio comparten la misma hora, evitando errores de autenticación y asegurando la coherencia en auditorías y registros del sistema.

## Servicio de archivos (Comparticiones SMB)

El servicio de archivos permite centralizar documentos y recursos dentro del dominio, ofreciendo acceso controlado mediante permisos NTFS y de compartición. Este servicio es fundamental para la colaboración y la administración de datos dentro del entorno.

### Pasos realizados

1. Se crea una carpeta en el controlador de dominio o en un servidor dedicado para almacenamiento.
2. Se accede a las propiedades de la carpeta y se configura como **recurso compartido**.
3. Se asigna un nombre de compartición que identifique claramente su propósito.
4. Se configuran los permisos de compartición:
   - Lectura
   - Cambio
   - Control total  
   según las necesidades del grupo o usuarios.
5. Se configuran los permisos NTFS para un control más granular:
   - Permisos heredados
   - Permisos explícitos
   - Grupos con acceso específico
6. Se valida que los usuarios del dominio puedan acceder al recurso mediante:
  \\nombre_servidor\nombre_comparticion

7. Se prueba el acceso desde diferentes cuentas para confirmar que los permisos funcionan correctamente.
8. Si es necesario, se crean carpetas personales o departamentales con permisos diferenciados.
9. Se habilita la auditoría en la carpeta si se requiere registrar accesos o modificaciones.

### Objetivo de este paso

Proporcionar un sistema centralizado de almacenamiento dentro del dominio, con permisos controlados y acceso seguro para los usuarios y grupos del entorno.

## Servicio de impresión (Print Server)

El servicio de impresión permite centralizar la gestión de impresoras dentro del dominio, facilitando su despliegue, control y administración. Con un servidor de impresión, los usuarios pueden instalar impresoras automáticamente y los administradores pueden aplicar permisos y políticas de uso.

### Pasos realizados

1. Se abre el **Administrador del servidor** en el controlador de dominio o en un servidor dedicado.
2. Se instala el rol **Servicios de impresión y documentos**.
3. Se accede a la consola **Administración de impresión**.
4. Se agrega una impresora al servidor mediante:
   - Detección automática.
   - Instalación manual del controlador.
   - Puerto TCP/IP si la impresora es de red.
5. Se asigna un nombre descriptivo a la impresora para facilitar su identificación.
6. Se configuran los permisos de impresión:
   - Imprimir
   - Administrar documentos
   - Administrar impresora
7. Se comparte la impresora para que los usuarios del dominio puedan instalarla automáticamente.
8. Si se desea automatizar la instalación, se vincula la impresora a una GPO mediante:
   - **Configuración del usuario → Preferencias → Configuración del Panel de control → Impresoras**
9. Se prueba la instalación desde un equipo cliente accediendo a:
  \\nombre_servidor

10. Se valida que los usuarios pueden imprimir correctamente y que los permisos funcionan según lo configurado.

### Objetivo de este paso

Centralizar la gestión de impresoras dentro del dominio, facilitando su despliegue y control, y garantizando un uso eficiente y administrado de los recursos de impresión.

## Servicio WSUS (actualizaciones centralizadas)

WSUS permite centralizar la descarga y distribución de actualizaciones de Windows dentro del dominio. Con este servicio, los equipos no necesitan conectarse directamente a Internet para recibir actualizaciones, lo que mejora la seguridad, reduce el consumo de ancho de banda y permite un control total sobre qué actualizaciones se instalan.

### Pasos realizados

1. Se abre el **Administrador del servidor** en el controlador de dominio o en un servidor dedicado.
2. Se instala el rol **Windows Server Update Services (WSUS)**.
3. Durante la instalación, se selecciona:
   - La ubicación donde se almacenarán las actualizaciones.
   - El servidor SQL o la base de datos interna (WID).
4. Una vez instalado, se abre la consola **WSUS**.
5. Se configura el origen de sincronización:
   - Servidores de Microsoft Update.
   - Idiomas y productos que se desean actualizar.
6. Se define la programación de sincronización automática.
7. Se crean grupos de equipos, por ejemplo:
   - `Equipos de prueba`
   - `Equipos de producción`
8. Se vinculan los equipos del dominio a estos grupos mediante GPO:
   - **Configuración del equipo → Plantillas administrativas → Componentes de Windows → Windows Update → Especificar la ubicación del servidor WSUS**
9. Se sincronizan las actualizaciones y se revisan las disponibles.
10. Se aprueban las actualizaciones para cada grupo según la política del laboratorio.
11. En los equipos cliente, se ejecuta:
  wuauclt /detectnow
    
    para forzar la detección de actualizaciones.
    
13. Se valida que los equipos reciben las actualizaciones desde WSUS y no desde Internet.

### Objetivo de este paso

Centralizar la gestión de actualizaciones dentro del dominio, garantizando que todos los equipos reciban parches de seguridad de forma controlada, organizada y alineada con las políticas del entorno.

## Estado de la configuración de servicios

La configuración de los servicios del dominio queda completada con la implementación de DNS, DHCP, NTP, comparticiones SMB, servidor de impresión y WSUS.  
Estos servicios proporcionan una infraestructura estable, centralizada y administrada, permitiendo que el entorno funcione de manera eficiente y segura.

Con esta base, el laboratorio está preparado para continuar con la siguiente fase: la monitorización del sistema y de los servicios críticos del dominio.



