# Políticas de Grupo (GPOs) en el dominio

Esta sección documenta la creación, configuración y aplicación de las Políticas de Grupo (GPOs) dentro del dominio del laboratorio. Las GPOs permiten controlar configuraciones de usuarios y equipos de manera centralizada, asegurando un entorno administrado y coherente.

## Objetivo de esta sección

Explicar de forma clara cómo se crean, vinculan y administran las GPOs en el dominio, incluyendo configuraciones básicas y avanzadas aplicadas a usuarios y equipos dentro de las OUs definidas previamente.

## Creación de una GPO básica

Las Políticas de Grupo permiten aplicar configuraciones de manera centralizada a usuarios y equipos dentro del dominio. Para comenzar, se crea una GPO básica que servirá como ejemplo de configuración inicial.

### Pasos realizados

1. Se abre la consola **Administración de directivas de grupo (GPMC)**.
2. Dentro del dominio, se selecciona la OU donde se aplicará la política (por ejemplo, `Usuarios` o `Equipos`).
3. Se elige la opción **Crear un GPO en este dominio y vincularlo aquí**.
4. Se asigna un nombre descriptivo a la política (por ejemplo: `GPO - Configuración básica`).
5. Una vez creada, se edita la GPO para definir las configuraciones necesarias.
6. La política queda lista para aplicar ajustes tanto de usuario como de equipo según las necesidades del laboratorio.

### Objetivo de este paso

Establecer una política inicial que sirva como base para aplicar configuraciones centralizadas dentro del dominio y facilitar la administración del entorno.

## Configuración básica dentro de la GPO

Una vez creada la GPO, se aplica una configuración sencilla para demostrar cómo las políticas afectan a los usuarios o equipos del dominio. Esta configuración sirve como ejemplo inicial antes de implementar políticas más avanzadas.

### Pasos realizados

1. Se abre la consola **Administración de directivas de grupo (GPMC)**.
2. Se selecciona la GPO creada previamente y se elige la opción **Editar**.
3. Dentro del editor de políticas, se navega a:
   - **Configuración del equipo** o  
   - **Configuración del usuario**,  
   según el tipo de ajuste que se desea aplicar.
4. Se selecciona una configuración básica, como:
   - Cambiar la página de inicio del navegador.
   - Deshabilitar el Panel de control.
   - Mostrar un mensaje de bienvenida al iniciar sesión.
5. Se habilita o configura la opción seleccionada.
6. Se cierra el editor y la GPO queda lista para aplicarse a los objetos de la OU correspondiente.

### Objetivo de este paso

Demostrar cómo aplicar una configuración sencilla dentro de una GPO y preparar el entorno para políticas más avanzadas que se implementarán posteriormente.

## Actualización y aplicación de las GPOs

Una vez configurada una GPO, es necesario asegurarse de que los equipos y usuarios del dominio reciban y apliquen correctamente las políticas definidas. Para ello, se realiza una actualización manual o se espera a que el sistema aplique las políticas de forma automática.

### Pasos realizados

1. En un equipo cliente unido al dominio, se abre una ventana de **Símbolo del sistema** o **PowerShell**.
2. Se ejecuta el comando:
  gpupdate /force

Este comando fuerza la actualización de las políticas de usuario y de equipo.
3. Se espera a que el sistema confirme la aplicación de las políticas.
4. En caso de que alguna política requiera reinicio o cierre de sesión, el sistema lo indicará.
5. Para verificar qué políticas se han aplicado, se utiliza el comando:
  gpresult /r

6. Se revisa la salida del comando para confirmar que la GPO creada aparece en la lista de políticas aplicadas.
7. Una vez validado, la GPO queda oficialmente activa en el equipo o usuario correspondiente.

### Objetivo de este paso

Asegurar que las políticas configuradas en el dominio se aplican correctamente en los equipos y usuarios, garantizando un entorno administrado y coherente.

## Estado de la configuración de GPOs

La configuración básica de las Políticas de Grupo queda completada con la creación de una GPO inicial, la aplicación de una configuración sencilla y la validación de su funcionamiento en los equipos del dominio.  
A partir de este punto, el entorno está preparado para implementar políticas más avanzadas relacionadas con seguridad, restricciones, automatización y administración centralizada.

Esta sección establece la base necesaria para continuar con la documentación de medidas de seguridad dentro del laboratorio.



