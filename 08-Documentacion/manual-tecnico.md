# Manual técnico del laboratorio de Windows Server

Este manual recoge toda la información técnica del laboratorio, incluyendo la infraestructura, configuración del dominio, servicios, seguridad, automatización y monitorización. Su objetivo es servir como documento profesional que describe de forma clara y detallada el entorno implementado.

## 1. Introducción

El presente manual técnico documenta la construcción completa de un laboratorio basado en Windows Server, diseñado para simular un entorno empresarial real con servicios de dominio, políticas de grupo, seguridad, automatización y monitorización.  
El objetivo principal del proyecto es demostrar la capacidad de implementar, administrar y mantener una infraestructura corporativa funcional utilizando tecnologías de Microsoft.

Este laboratorio ha sido desarrollado siguiendo buenas prácticas de administración de sistemas, permitiendo comprender de forma práctica cómo se estructura y gestiona un dominio Active Directory, cómo se configuran sus servicios esenciales y cómo se supervisa su funcionamiento para garantizar estabilidad y seguridad.

El alcance del proyecto incluye:

- Instalación y configuración de un controlador de dominio.
- Implementación de Active Directory con usuarios, grupos y OU.
- Aplicación de políticas de grupo (GPOs) para gestionar el entorno.
- Configuración de servicios críticos como DNS, DHCP, NTP, WSUS y comparticiones SMB.
- Medidas de seguridad y endurecimiento del sistema.
- Automatización mediante scripts y tareas programadas.
- Monitorización del dominio y sus servicios.
- Documentación completa del entorno y sus procedimientos.

Este manual sirve como referencia técnica para comprender el funcionamiento del laboratorio y como evidencia profesional del trabajo realizado.




## 2. Infraestructura del entorno

El laboratorio se ha construido sobre un entorno virtualizado que simula la infraestructura básica de una empresa. La arquitectura se ha diseñado para permitir la implementación de un dominio Active Directory completo, junto con servicios esenciales y equipos cliente para pruebas.

### 2.1 Plataforma de virtualización

El entorno se ejecuta sobre una plataforma de virtualización que permite crear y gestionar máquinas virtuales de forma aislada. Esta plataforma facilita la creación de redes internas, la asignación de recursos y la administración del laboratorio sin afectar al sistema anfitrión.

### 2.2 Máquinas virtuales del laboratorio

El laboratorio está compuesto por las siguientes máquinas virtuales:

- **Controlador de dominio (DC01)**  
  - Sistema operativo: Windows Server  
  - Funciones: Active Directory, DNS, DHCP, NTP, WSUS, servidor de archivos, servidor de impresión.  
  - Recursos asignados: CPU, memoria y almacenamiento suficientes para ejecutar servicios críticos.

- **Equipos cliente (PC01, PC02, etc.)**  
  - Sistema operativo: Windows  
  - Funciones: unión al dominio, pruebas de GPOs, acceso a servicios, validación de políticas y monitorización.

### 2.3 Red del laboratorio

La red del entorno se ha configurado para simular una red corporativa interna:

- **Rango de direcciones IP** asignado mediante DHCP.
- **Servidor DNS** integrado en el controlador de dominio.
- **Puerta de enlace** simulada o estática según la configuración del laboratorio.
- **Red interna** aislada del exterior para garantizar seguridad y control total del entorno.

### 2.4 Recursos y configuración base

- Asignación de CPU y memoria adaptada a cada máquina virtual.
- Almacenamiento suficiente para servicios como WSUS y comparticiones SMB.
- Configuración inicial del servidor con roles y características necesarias.
- Sincronización horaria mediante NTP para garantizar el correcto funcionamiento de Kerberos.
- Estructura organizada de carpetas y documentación dentro del proyecto.

Esta infraestructura proporciona una base sólida para la implementación del dominio y todos los servicios asociados, permitiendo realizar pruebas, configuraciones y simulaciones de un entorno empresarial real.

## 3. Implementación de Active Directory

La implementación de Active Directory constituye el núcleo del laboratorio, proporcionando autenticación centralizada, gestión de usuarios, administración de recursos y control del entorno mediante políticas de grupo. Esta sección describe el proceso completo de instalación y configuración del dominio.

### 3.1 Instalación del rol de Active Directory Domain Services

1. Se instala el rol **Active Directory Domain Services (AD DS)** desde el Administrador del servidor.
2. Una vez instalado el rol, se promueve el servidor a **controlador de dominio**.
3. Se crea un nuevo dominio dentro de un nuevo bosque.
4. Se configura el nivel funcional del bosque y del dominio.
5. Se instala y configura automáticamente el servicio DNS integrado.
6. Se reinicia el servidor para completar la promoción.

### 3.2 Configuración inicial del dominio

- Se valida el correcto funcionamiento del servicio DNS.
- Se comprueba la replicación interna del controlador de dominio.
- Se verifica la creación de las zonas DNS necesarias para Active Directory.
- Se ajusta la configuración de tiempo (NTP) para garantizar la sincronización correcta del entorno.

### 3.3 Estructura organizativa (OU)

Se crea una estructura organizada de Unidades Organizativas para separar y administrar los diferentes elementos del dominio:

- OU para usuarios.
- OU para grupos.
- OU para equipos cliente.
- OU para departamentos (si aplica).
- OU para políticas específicas.

Esta estructura permite aplicar GPOs de forma ordenada y mantener una administración clara del entorno.

### 3.4 Creación de usuarios y grupos

- Se crean usuarios estándar para pruebas y validación del dominio.
- Se crean grupos de seguridad y grupos globales para la asignación de permisos.
- Se aplican buenas prácticas como:
  - Separación entre usuarios y equipos.
  - Uso de grupos para permisos en lugar de asignarlos directamente a usuarios.
  - Nombres descriptivos y consistentes.

### 3.5 Unión de equipos al dominio

Los equipos cliente se unen al dominio para permitir:

- Autenticación centralizada.
- Aplicación de políticas de grupo.
- Acceso a recursos compartidos.
- Supervisión y administración desde el controlador de dominio.

### 3.6 Políticas iniciales del dominio

Se aplican políticas básicas para establecer control sobre el entorno:

- Configuración de contraseñas y bloqueo de cuentas.
- Redirección de carpetas (si aplica).
- Restricciones de seguridad.
- Configuración de escritorio y entorno de usuario.
- Políticas de instalación de software (si se utilizan).

Estas políticas sirven como base para el resto de configuraciones del laboratorio.

---

La implementación de Active Directory proporciona la estructura fundamental del entorno, permitiendo administrar usuarios, equipos y recursos de forma centralizada y segura.


## 4. Políticas de grupo (GPOs)

Las Políticas de Grupo (GPOs) permiten administrar de forma centralizada la configuración de usuarios y equipos dentro del dominio. En este laboratorio se han implementado diversas políticas destinadas a mejorar la seguridad, estandarizar el entorno y controlar el comportamiento de los equipos cliente.

### 4.1 Estructura de GPOs en el dominio

Las GPOs se han organizado siguiendo buenas prácticas:

- Políticas aplicadas a nivel de dominio.
- Políticas específicas vinculadas a OUs concretas.
- Separación entre políticas de usuario y políticas de equipo.
- Nombres descriptivos para facilitar su administración.

### 4.2 Políticas aplicadas en el laboratorio

A continuación se describen las políticas principales configuradas:

####  Políticas de seguridad
- Configuración de contraseñas (longitud mínima, complejidad, caducidad).
- Bloqueo de cuentas tras intentos fallidos.
- Restricciones de acceso a panel de control y configuraciones del sistema.
- Deshabilitación de ejecución de aplicaciones no autorizadas (si aplica).

####  Políticas de entorno de usuario
- Configuración del escritorio.
- Restricción de acceso a configuraciones avanzadas.
- Redirección de carpetas (si se implementó).
- Aplicación de fondos de pantalla corporativos (si se utilizó).

#### 🖧 Políticas de red
- Configuración de servidores NTP.
- Ajustes de red para clientes del dominio.
- Configuración de proxy (si aplica).

####  Políticas de software
- Instalación automática de software mediante GPO (si se utilizó).
- Restricciones de ejecución mediante AppLocker o Software Restriction Policies.

####  Políticas de impresión
- Distribución automática de impresoras del servidor de impresión.
- Configuración de permisos de impresión.

####  Políticas de actualización
- Configuración de WSUS para que los equipos reciban actualizaciones desde el servidor interno.
- Programación de instalación de actualizaciones.

### 4.3 Validación de las políticas

Para asegurar que las políticas se aplican correctamente:

- Se ejecuta `gpupdate /force` en los equipos cliente.
- Se revisa el Visor de eventos para detectar errores de GPO.
- Se utiliza `gpresult /r` para comprobar qué políticas se aplican a cada usuario y equipo.
- Se realizan pruebas prácticas en los equipos cliente para validar los cambios.

---

Las GPOs permiten controlar de forma precisa el comportamiento del entorno, garantizando seguridad, estandarización y administración centralizada del dominio.


## 5. Seguridad del dominio

La seguridad del dominio es uno de los pilares fundamentales del laboratorio. Se han implementado diversas medidas destinadas a proteger el controlador de dominio, los equipos cliente, los usuarios y los servicios críticos del entorno. Estas acciones garantizan la integridad, disponibilidad y confidencialidad del sistema.

### 5.1 Protección del controlador de dominio

El controlador de dominio es el componente más crítico del entorno, por lo que se han aplicado medidas específicas:

- Restricción de acceso físico y lógico al servidor.
- Uso de cuentas administrativas separadas para tareas de gestión.
- Deshabilitación de servicios innecesarios.
- Configuración de firewall mediante reglas específicas.
- Sincronización horaria correcta para evitar problemas con Kerberos.
- Revisión periódica del Visor de eventos para detectar anomalías.

### 5.2 Gestión de permisos y privilegios

Se han aplicado buenas prácticas de administración de permisos:

- Principio de **mínimo privilegio** para usuarios y grupos.
- Uso de grupos de seguridad para asignar permisos en lugar de hacerlo directamente a usuarios.
- Control de acceso a carpetas compartidas mediante ACLs.
- Separación entre cuentas de usuario y cuentas administrativas.
- Restricción de acceso a herramientas del sistema para usuarios estándar.

### 5.3 Auditorías y registros

Para garantizar trazabilidad y detección de incidentes:

- Activación de auditorías de inicio de sesión.
- Auditoría de acceso a objetos (carpetas y archivos sensibles).
- Registro de cambios en políticas de grupo.
- Supervisión de eventos críticos en:
  - Active Directory
  - DNS
  - Replicación
  - Seguridad del sistema

### 5.4 Políticas de seguridad mediante GPO

Se han aplicado políticas específicas para reforzar la seguridad del entorno:

- Configuración de contraseñas (complejidad, longitud, caducidad).
- Bloqueo de cuentas tras intentos fallidos.
- Restricción de acceso al Panel de control y configuraciones avanzadas.
- Deshabilitación de ejecución de software no autorizado (si aplica).
- Configuración de WSUS para actualizaciones controladas.

### 5.5 Seguridad en servicios del dominio

Cada servicio ha sido configurado siguiendo buenas prácticas:

- **DNS:** zonas seguras, actualizaciones dinámicas protegidas.
- **DHCP:** reservas, control de concesiones y protección contra servidores no autorizados.
- **NTP:** sincronización con el controlador de dominio.
- **Comparticiones SMB:** permisos NTFS y de recurso compartido correctamente configurados.
- **Impresión:** control de permisos y distribución mediante GPO.
- **WSUS:** aprobación manual de actualizaciones y control de equipos.

### 5.6 Seguridad en equipos cliente

Los equipos unidos al dominio cuentan con:

- Políticas de restricción de software.
- Configuración de firewall.
- Actualizaciones controladas mediante WSUS.
- Restricciones de acceso a configuraciones del sistema.
- Supervisión mediante Visor de eventos y herramientas de monitorización.

---

Estas medidas garantizan que el dominio funcione de forma segura, minimizando riesgos y asegurando que los servicios críticos estén protegidos frente a accesos no autorizados o fallos de configuración.

## 6. Servicios del dominio

El dominio implementado en el laboratorio incluye una serie de servicios esenciales para garantizar su funcionamiento, administración y disponibilidad. Cada servicio ha sido configurado siguiendo buenas prácticas, asegurando estabilidad, seguridad y eficiencia en el entorno.

### 6.1 Servicio DNS

El servicio DNS es fundamental para Active Directory, ya que permite la resolución de nombres dentro del dominio.

- Instalación automática durante la promoción del controlador de dominio.
- Configuración de zonas integradas en Active Directory.
- Actualizaciones dinámicas seguras.
- Registros SRV generados correctamente para los servicios del dominio.
- Validación mediante herramientas como `nslookup` y el Visor de eventos.

### 6.2 Servicio DHCP

El servidor DHCP proporciona direcciones IP y parámetros de red a los equipos cliente.

- Creación de un ámbito con el rango de direcciones del laboratorio.
- Configuración de puerta de enlace, DNS y dominio.
- Reservas para equipos específicos (si aplica).
- Supervisión de concesiones y estado del servicio.
- Integración con DNS para actualizaciones dinámicas.

### 6.3 Servicio NTP (W32Time)

La sincronización horaria es esencial para Kerberos y la autenticación del dominio.

- El controlador de dominio actúa como servidor NTP interno.
- Los equipos cliente sincronizan automáticamente con el DC.
- Validación mediante:
  w32tm /query /status


### 6.4 Comparticiones SMB

Se han configurado recursos compartidos para almacenamiento y distribución de archivos.

- Carpetas compartidas con permisos NTFS y de recurso compartido.
- Uso de grupos de seguridad para controlar el acceso.
- Acceso desde equipos cliente mediante rutas UNC.
- Auditoría de acceso a archivos sensibles (si aplica).

### 6.5 Servidor de impresión

El controlador de dominio actúa como servidor de impresión centralizado.

- Instalación del rol de impresión.
- Adición de impresoras físicas o virtuales.
- Publicación en Active Directory.
- Distribución automática mediante GPO.
- Control de permisos de impresión.

### 6.6 WSUS (Windows Server Update Services)

WSUS permite gestionar las actualizaciones de Windows dentro del dominio.

- Instalación del rol WSUS y configuración de la base de datos.
- Sincronización con Microsoft Update.
- Aprobación manual de actualizaciones.
- Configuración de GPO para que los equipos usen WSUS.
- Supervisión del estado de los equipos y actualizaciones pendientes.

---

Estos servicios forman el núcleo funcional del dominio, proporcionando resolución de nombres, direccionamiento IP, sincronización horaria, almacenamiento, impresión y gestión de actualizaciones. Su correcta configuración garantiza un entorno estable y administrado de forma centralizada.

## 7. Automatización

La automatización es una parte fundamental del laboratorio, ya que permite reducir tareas repetitivas, mejorar la eficiencia y garantizar que ciertos procesos se ejecuten de forma consistente. En este entorno se han implementado scripts y tareas programadas que facilitan la administración del dominio y sus servicios.

### 7.1 Scripts utilizados en el laboratorio

Se han creado scripts en PowerShell para automatizar diversas tareas administrativas:

- **Revisión del estado de servicios críticos**
  ```powershell
  $servicios = "DNS","DHCPServer","W32Time","NTDS"
  Get-Service -Name $servicios

Este script permite comprobar rápidamente si los servicios esenciales del dominio están en ejecución.

**Copias de seguridad básicas de carpetas
  Copy-Item -Path C:\Datos -Destination D:\Backup\Datos -Recurse
Utilizado para realizar copias de seguridad simples dentro del entorno.

**Revisión de eventos del sistema
  Get-EventLog -LogName System -Newest 20
Permite obtener los eventos más recientes del sistema para detectar problemas.

7.2 Tareas programadas
Se han configurado tareas programadas para ejecutar scripts de forma automática:

Comprobación periódica de servicios

Frecuencia: diaria.

Acción: ejecutar el script de revisión de servicios.

Objetivo: detectar fallos antes de que afecten al dominio.

Copias de seguridad automáticas

Frecuencia: semanal.

Acción: ejecutar el script de copia de seguridad.

Objetivo: mantener una copia actualizada de datos importantes.

7.3 Automatización mediante GPO
Algunas configuraciones se han automatizado mediante políticas de grupo:

Distribución automática de impresoras.

Aplicación de configuraciones de red.

Instalación de software (si se utilizó).

Configuración de WSUS para actualizaciones controladas.

7.4 Beneficios de la automatización en el laboratorio
Reducción de tareas manuales.

Mayor consistencia en la administración del entorno.

Detección temprana de problemas.

Ahorro de tiempo en tareas repetitivas.

Mejor organización y control del dominio.

La automatización implementada en el laboratorio permite mantener el entorno de forma eficiente y asegura que procesos críticos se ejecuten de manera fiable y constante.

## 8. Monitorización

La monitorización del dominio es esencial para garantizar la estabilidad, seguridad y correcto funcionamiento de todos los servicios del entorno. En este laboratorio se han utilizado diversas herramientas integradas en Windows Server para supervisar eventos, rendimiento, servicios y actividad del sistema.

### 8.1 Visor de eventos

El Visor de eventos permite revisar registros críticos del sistema:

- Eventos de Active Directory.
- Errores y advertencias del servicio DNS.
- Fallos de replicación.
- Eventos de seguridad (inicios de sesión, auditorías).
- Problemas de servicios o controladores.

Se han revisado periódicamente los registros de:
- **Aplicación**
- **Sistema**
- **Seguridad**
- **DNS Server**
- **Directory Service**
- **File Replication Service**

Esta herramienta permite detectar problemas antes de que afecten al funcionamiento del dominio.

### 8.2 Monitorización de servicios con PowerShell

Se ha utilizado PowerShell para comprobar el estado de servicios críticos:

powershell
  Get-Service
  Get-Service -Name DNS
  Get-Service -Name NTDS
  Get-Service -Name DHCPServer

Además, se creó un script para revisar automáticamente los servicios esenciales del dominio.

8.3 Monitor de recursos
El Monitor de recursos permite supervisar en tiempo real:

Uso de CPU.

Consumo de memoria.

Actividad de disco.

Tráfico de red.

Se han identificado procesos que generan carga excesiva y se ha validado el comportamiento de servicios como DNS, AD DS y WSUS.

8.4 Performance Monitor (Monitor de rendimiento)
Se han utilizado contadores avanzados para analizar el rendimiento del sistema:

Latencia de disco.

Uso de CPU.

Memoria disponible.

Consultas DNS por segundo.

Actividad de Active Directory (NTDS).

Además, se han creado conjuntos de recopiladores de datos para registrar métricas durante periodos prolongados y generar informes detallados.

8.5 Validación y mantenimiento
La monitorización se ha complementado con:

Revisión periódica de eventos críticos.

Supervisión del estado de servicios.

Análisis de tendencias de rendimiento.

Identificación de cuellos de botella.

Documentación de incidencias detectadas.

La monitorización implementada en el laboratorio permite mantener el dominio estable, detectar problemas de forma temprana y garantizar que los servicios esenciales funcionen correctamente.

## 9. Evidencias y capturas

A lo largo del desarrollo del laboratorio se han generado diversas capturas que sirven como evidencia visual del trabajo realizado. Estas imágenes documentan configuraciones, validaciones, estados del sistema y resultados de pruebas realizadas en cada fase del proyecto.

Todas las capturas se encuentran organizadas dentro de la carpeta:
  08-Documentación/Capturas/


### 9.1 Contenido de las capturas

Las capturas incluyen, entre otras:

- Instalación y promoción del controlador de dominio.
- Configuración de Active Directory, usuarios, grupos y OU.
- Aplicación y validación de GPOs.
- Configuración de servicios como DNS, DHCP, NTP, WSUS y SMB.
- Unión de equipos al dominio.
- Scripts y tareas programadas en ejecución.
- Monitorización del sistema mediante:
  - Visor de eventos
  - PowerShell
  - Monitor de recursos
  - Performance Monitor

### 9.2 Uso de las capturas en el manual

Las capturas sirven como evidencia técnica del funcionamiento del laboratorio y permiten validar:

- Que las configuraciones se realizaron correctamente.
- Que los servicios están activos y funcionando.
- Que las políticas se aplican en los equipos cliente.
- Que la monitorización detecta correctamente el estado del sistema.

---

Las evidencias visuales complementan la documentación escrita y permiten demostrar de forma clara y verificable cada uno de los pasos realizados en el laboratorio.

## 10. Conclusiones

El laboratorio de Windows Server desarrollado en este proyecto representa una implementación completa y funcional de un entorno empresarial basado en Active Directory. A través de cada una de las fases documentadas, se ha construido una infraestructura sólida que integra servicios críticos, políticas de seguridad, automatización y monitorización avanzada.

Este entorno permite comprender de forma práctica cómo se administra un dominio corporativo, cómo se gestionan usuarios y equipos, y cómo se configuran servicios esenciales como DNS, DHCP, NTP, WSUS, impresión y comparticiones SMB. Además, se han aplicado buenas prácticas de seguridad y se han utilizado herramientas de supervisión para garantizar la estabilidad del sistema.

El laboratorio demuestra:

- Capacidad para diseñar y desplegar un dominio Active Directory desde cero.  
- Competencia en la configuración de servicios fundamentales del entorno Windows Server.  
- Conocimiento en la aplicación de políticas de grupo para controlar usuarios y equipos.  
- Habilidad para automatizar tareas administrativas mediante scripts y tareas programadas.  
- Dominio de herramientas de monitorización para analizar el rendimiento y detectar incidencias.  
- Organización profesional de documentación y evidencias técnicas.

Este manual técnico sirve como evidencia del trabajo realizado y como referencia para futuras implementaciones, ampliaciones o auditorías del entorno. El laboratorio queda completamente funcional, documentado y preparado para ser utilizado como base de aprendizaje, demostración profesional o entorno de pruebas.





