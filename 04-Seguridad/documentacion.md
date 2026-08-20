# Seguridad en el dominio

Esta sección documenta las medidas de seguridad implementadas dentro del dominio del laboratorio. Incluye configuraciones relacionadas con contraseñas, auditorías, permisos avanzados y políticas destinadas a proteger los recursos del entorno.

## Objetivo de esta sección

Establecer una base sólida de seguridad dentro del dominio, aplicando buenas prácticas y configuraciones esenciales que permiten mantener un entorno controlado, protegido y alineado con los estándares recomendados.

## Configuración de políticas de contraseñas

Las políticas de contraseñas permiten establecer requisitos mínimos de seguridad para todas las cuentas del dominio. Estas configuraciones ayudan a proteger el entorno frente a accesos no autorizados y prácticas inseguras.

### Pasos realizados

1. Se abre la consola **Administración de directivas de grupo (GPMC)**.
2. Se edita la **Directiva de dominio predeterminada** o se crea una GPO específica para gestionar las políticas de contraseñas.
3. Dentro del editor de políticas, se navega a:
   - **Configuración del equipo → Configuración de Windows → Configuración de seguridad → Directivas de cuenta → Directiva de contraseñas**
4. Se configuran los parámetros principales:
   - **Longitud mínima de la contraseña** (por ejemplo, 8 caracteres).
   - **Complejidad de contraseña habilitada** (requiere mayúsculas, minúsculas, números y símbolos).
   - **Duración máxima de la contraseña** (por ejemplo, 30 días).
   - **Historial de contraseñas** (evita reutilizar las últimas contraseñas).
   - **Tiempo mínimo antes de poder cambiar la contraseña**.
5. Se aplican los cambios y se cierra el editor.
6. Para que los equipos reciban la nueva configuración, se ejecuta:
   gpupdate /force

7. Las políticas quedan activas para todos los usuarios del dominio.

### Objetivo de este paso

Garantizar que todas las cuentas del dominio cumplan con requisitos mínimos de seguridad, reduciendo el riesgo de accesos no autorizados y fortaleciendo la protección del entorno.

## Configuración de auditorías básicas

La auditoría permite registrar eventos importantes dentro del dominio, como intentos de inicio de sesión, cambios en objetos de Active Directory o accesos a recursos. Estas configuraciones son esenciales para detectar actividades sospechosas y mantener un entorno seguro.

### Pasos realizados

1. Se abre la consola **Administración de directivas de grupo (GPMC)**.
2. Se crea una GPO específica para auditoría o se edita una existente destinada a seguridad.
3. Dentro del editor de políticas, se navega a:
   **Configuración del equipo → Configuración de Windows → Configuración de seguridad → Directivas de auditoría**
4. Se habilitan las auditorías básicas recomendadas:
   - **Auditar eventos de inicio de sesión** (éxito y error).
   - **Auditar acceso a objetos** (según necesidad).
   - **Auditar cambios de directivas**.
   - **Auditar administración de cuentas** (creación, eliminación o modificación de usuarios y grupos).
5. Se aplican los cambios y se cierra el editor.
6. Para que los equipos reciban la configuración, se ejecuta:
  gpupdate /force

7. Los eventos auditados pueden revisarse posteriormente en el **Visor de eventos** dentro de cada equipo o en el controlador de dominio.

### Objetivo de este paso

Registrar actividades relevantes dentro del dominio para mejorar la visibilidad, detectar comportamientos anómalos y fortalecer la seguridad del entorno.

## Configuración de permisos avanzados

Además de las políticas básicas y la auditoría, es necesario aplicar permisos avanzados para controlar de forma precisa quién puede administrar, modificar o acceder a determinados recursos dentro del dominio. Estos permisos permiten delegar tareas específicas sin otorgar privilegios excesivos.

### Pasos realizados

1. Se abre la consola **Usuarios y Equipos de Active Directory**.
2. Se selecciona la OU o el objeto sobre el cual se desea aplicar permisos avanzados.
3. Se accede a las **Propiedades** y luego a la pestaña **Seguridad**.
4. Se revisan los permisos existentes y se agregan grupos o usuarios según sea necesario.
5. Se asignan permisos específicos como:
   - **Crear y eliminar objetos dentro de la OU**.
   - **Restablecer contraseñas**.
   - **Leer o modificar atributos de usuarios y equipos**.
   - **Unir equipos al dominio**.
6. Para delegar tareas de forma controlada, se utiliza el asistente **Delegación de control**, seleccionando:
   - El grupo o usuario que recibirá los permisos.
   - Las tareas específicas que podrá realizar.
7. Se valida que los permisos aplicados no otorguen más privilegios de los necesarios.
8. Se prueba con una cuenta del grupo delegado para confirmar que puede realizar solo las tareas asignadas.

### Objetivo de este paso

Aplicar un control granular sobre las acciones administrativas dentro del dominio, permitiendo delegar responsabilidades sin comprometer la seguridad del entorno.

## Estado de la configuración de seguridad

La configuración de seguridad del dominio queda establecida con la aplicación de políticas de contraseñas, auditorías básicas y permisos avanzados.  
Estas medidas permiten mantener un entorno controlado, supervisado y protegido frente a accesos no autorizados o cambios no deseados.

A partir de este punto, el laboratorio está preparado para continuar con la implementación y documentación de servicios adicionales dentro del dominio.

