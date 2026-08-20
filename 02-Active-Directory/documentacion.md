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

## Promoción del servidor a controlador de dominio

Una vez instalado el rol de Active Directory Domain Services, el siguiente paso consiste en promover el servidor para que actúe como controlador de dominio dentro del laboratorio.

### Pasos realizados

1. En el Administrador del servidor, se selecciona la notificación que indica que el rol AD DS requiere una configuración adicional.
2. Se elige la opción **Promover este servidor a controlador de dominio**.
3. Se selecciona **Agregar un nuevo bosque** para crear un dominio desde cero.
4. Se define el nombre del dominio del laboratorio.
5. Se establece el nivel funcional del bosque y del dominio según las opciones disponibles.
6. Se configura la contraseña del Modo de Restauración de Servicios de Directorio (DSRM).
7. Se revisan las opciones de DNS y se aceptan las configuraciones recomendadas.
8. Se valida la configuración y se inicia el proceso de promoción.
9. El servidor se reinicia automáticamente para completar la operación.

### Objetivo de este paso

Convertir el servidor en el controlador principal del dominio, permitiendo la gestión centralizada de usuarios, equipos, grupos y políticas dentro del entorno del laboratorio.

## Creación de la estructura de Unidades Organizativas (OUs)

Una vez creado el dominio, se define una estructura de Unidades Organizativas (OUs) para organizar los recursos del laboratorio. Las OUs permiten aplicar políticas de grupo de manera ordenada y gestionar usuarios, grupos y equipos de forma estructurada.

### Pasos realizados

1. Se abre la consola **Usuarios y Equipos de Active Directory**.
2. Dentro del dominio, se crea una OU principal.
3. Dentro de esta OU se crean las siguientes subunidades:
   - **Usuarios**
   - **Grupos**
   - **Equipos**
   - **Administración**
4. Cada OU se utiliza para separar los diferentes tipos de objetos del dominio.
5. Esta estructura facilita la aplicación de GPOs específicas y la administración del entorno.

### Objetivo de este paso

Organizar los recursos del dominio de forma clara y lógica, permitiendo una gestión eficiente y una aplicación precisa de políticas de grupo.

## Creación de usuarios en el dominio

Una vez definida la estructura de OUs, se procede a crear los usuarios que formarán parte del dominio. Estos usuarios se utilizan para iniciar sesión en los equipos cliente y para aplicar políticas de grupo específicas.

### Pasos realizados

1. Se abre la consola **Usuarios y Equipos de Active Directory**.
2. Dentro de la OU **Usuarios**, se selecciona la opción **Nuevo → Usuario**.
3. Se introduce la información básica del usuario:
   - Nombre
   - Apellidos
   - Nombre de inicio de sesión (formato: usuario@laboratorio.local)
4. Se establece una contraseña inicial y se configuran las opciones:
   - El usuario debe cambiar la contraseña en el próximo inicio de sesión.
   - La contraseña nunca expira (así lo elegí).
5. Se repite el proceso para crear todos los usuarios necesarios para las pruebas.
6. Los usuarios quedan listos para iniciar sesión en los equipos cliente unidos al dominio.

### Objetivo de este paso

Crear las cuentas necesarias para realizar pruebas de inicio de sesión, aplicación de políticas de grupo y administración de recursos dentro del dominio.

## Creación de grupos en el dominio

Los grupos permiten organizar usuarios y asignar permisos de manera más eficiente dentro del dominio. En lugar de aplicar permisos usuario por usuario, se aplican directamente al grupo, facilitando la administración del entorno.

### Pasos realizados

1. Se abre la consola **Usuarios y Equipos de Active Directory**.
2. Dentro de la OU **Grupos**, se selecciona la opción **Nuevo → Grupo**.
3. Se define el nombre del grupo según su función.
4. Se selecciona el tipo de grupo:
   - **Seguridad** (para permisos y acceso a recursos).
   - **Distribución** 
5. Se elige el ámbito del grupo:
   - **Global** (recomendado para la mayoría de escenarios).
   - **Dominio local** (para permisos específicos dentro del dominio).
   - **Universal** (solo si se trabaja con múltiples dominios).
6. Se crean los grupos necesarios para organizar el laboratorio.
7. Finalmente, se agregan los usuarios correspondientes a cada grupo según su función.

### Objetivo de este paso

Establecer una estructura de grupos que permita gestionar permisos y recursos de manera centralizada, simplificando la administración del dominio.

## Registro de equipos dentro del dominio

Una vez que los clientes Windows se unen al dominio, aparecen automáticamente en la consola de Active Directory. Para mantener una estructura organizada, estos equipos se mueven a la OU correspondiente.

### Pasos realizados

1. Se abre la consola **Usuarios y Equipos de Active Directory**.
2. Dentro del dominio, se localiza el equipo recién unido (generalmente aparece en la OU **Computers** por defecto).
3. Se selecciona el equipo y se elige la opción **Mover**.
4. Se desplaza el equipo a la OU **Equipos** dentro de la estructura creada previamente.
5. Se repite el proceso para cada equipo cliente unido al dominio.
6. Una vez movidos, los equipos quedan listos para recibir políticas de grupo específicas.

### Objetivo de este paso

Mantener una estructura ordenada dentro del dominio y asegurar que los equipos reciban las GPOs aplicadas a su OU correspondiente.

## Permisos y administración básica en Active Directory

Una vez creados los usuarios, grupos y equipos dentro del dominio, se realizan configuraciones básicas de permisos para controlar el acceso a recursos y definir responsabilidades dentro del entorno.

### Pasos realizados

1. Se abre la consola **Usuarios y Equipos de Active Directory**.
2. Se selecciona un grupo previamente creado.
3. Se accede a las propiedades del grupo y se agregan los usuarios que deben formar parte de él.
4. Se asignan permisos específicos según la función del grupo:
   - Permisos de lectura o modificación sobre determinadas OUs.
   - Delegación de control para tareas administrativas básicas.
5. Se utiliza el asistente de **Delegación de control** para asignar permisos como:
   - Crear, eliminar o administrar usuarios.
   - Resetear contraseñas.
   - Unir equipos al dominio.
6. Se revisan los permisos aplicados para asegurar que cada grupo tiene únicamente los privilegios necesarios.
7. Se valida que los usuarios pueden realizar las tareas asignadas según su rol dentro del laboratorio.

### Objetivo de este paso

Establecer una administración básica del dominio, asegurando que los usuarios y grupos tengan los permisos adecuados para realizar sus funciones sin comprometer la seguridad del entorno.

## Estado de la configuración de Active Directory

La configuración básica de Active Directory queda completada con la creación del dominio, la estructura de OUs, los usuarios, los grupos y el registro de los equipos dentro del entorno.  
A partir de este punto, el dominio está preparado para aplicar políticas de grupo, gestionar permisos avanzados y continuar con la administración del entorno del laboratorio.

Esta sección establece la base necesaria para trabajar con GPOs, seguridad, automatización y servicios adicionales dentro del dominio.




