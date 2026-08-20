# Active Directory en Windows Server 2022

Esta sección documenta la instalación, configuración y administración del servicio de Active Directory Domain Services (AD DS) dentro del laboratorio. Aquí se detallan los pasos realizados para crear el dominio, estructurar las unidades organizativas y gestionar usuarios, grupos y permisos.

## Objetivo de esta sección

Proporcionar una guía clara y estructurada sobre cómo se implementa Active Directory en el entorno del laboratorio, incluyendo la creación del dominio, la organización de recursos y las configuraciones esenciales para su funcionamiento.

## Instalación del rol Active Directory Domain Services (AD DS)

Para convertir el servidor en un controlador de dominio, primero se instala el rol de Active Directory Domain Services (AD DS). Este rol proporciona los servicios necesarios para gestionar usuarios, grupos, equipos y políticas dentro del dominio.

### Pasos realizados

1. Se abre el **Administrador del servidor** desde el menú de inicio.
2. Se selecciona la opción **Agregar roles y características**.
3. Se elige la instalación basada en características y roles.
4. Se selecciona el servidor local como destino.
5. En la lista de roles, se marca **Active Directory Domain Services**.
6. Se aceptan las características adicionales que el sistema solicita.
7. Se continúa con el asistente hasta completar la instalación del rol.
8. Una vez instalado, el servidor queda listo para ser promovido a controlador de dominio.

### Objetivo de este paso

Instalar los componentes necesarios para que el servidor pueda gestionar un dominio y actuar como controlador principal dentro del laboratorio.
