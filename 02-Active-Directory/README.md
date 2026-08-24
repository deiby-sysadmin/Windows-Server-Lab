# Active Directory — contoso.com

Este apartado documenta el trabajo realizado sobre Active Directory en
el servidor DC01 del laboratorio. El dominio configurado es
contoso.com y la máquina servidor tiene la dirección IP 192.168.0.3,
con el servicio DNS apuntando a 127.0.0.1 tras la promoción a
controlador de dominio.

El objetivo de esta sección es dejar constancia de la estructura de
unidades organizativas creadas, los usuarios y grupos dados de alta,
la unión de equipos al dominio y la verificación de que todo el
conjunto funciona correctamente desde el lado cliente.

## Roles necesarios

Antes de empezar a trabajar con Active Directory conviene tener claros
los roles instalados en el servidor, ya que condicionan qué servicios
se pueden levantar. En el DC01 están activos AD DS, DHCP, DNS, IIS,
NDAS, los servicios de archivo y almacenamiento, los servicios de
Escritorio remoto y WSUS. Todos los análisis de BPA aparecen en estado
Listo en el momento de la captura, sin errores pendientes.

![Roles del servidor](./imagenes/02-ad-roles-servidor.png)

## Diseño de la estructura de OUs

La primera decisión de diseño fue definir la jerarquía de unidades
organizativas. Se optó por una estructura que refleja una organización
real, separando equipos, grupos, impresoras y usuarios, y añadiendo
dos OUs adicionales para representar delegaciones geográficas
(oficina norte y oficina sur).

![Estructura de OUs](./imagenes/02-ad-estructura-ous.png)

La OU raíz utilizada como contenedor principal es CONTOSO, ubicada
dentro de contoso.com. Dentro de ella se ubicaron las siguientes OUs:

- equipos, que contiene las cuentas de máquina unidas al dominio.
- grupos, destinada a los grupos de seguridad.
- impresoras, pensada para las cuentas de impresora publicadas.
- usuarios, donde se dieron de alta las cuentas de usuario.
- oficina norte y oficina sur, OUs adicionales para delegaciones.

Esta separación permite aplicar GPOs de forma granular y delegar la
administración por áreas sin afectar al resto del dominio.

## Creación de grupos de seguridad

Dentro de la OU grupos se crearon tres grupos de seguridad globales:
Administracion, Recursos y Soporte. La idea es aplicar permisos
diferenciados sobre los recursos compartidos del dominio en función
del grupo al que pertenezca cada usuario.

![Grupos de seguridad creados](./imagenes/02-ad-grupos-seguridad.png)

Los grupos se crearon con ámbito global y tipo seguridad, que es la
combinación habitual cuando se van a utilizar para asignar permisos
sobre recursos del dominio y se quiere poder anidar usuarios de
cualquier OU dentro del dominio.

## Alta de usuarios

Los usuarios se dieron de alta directamente desde la consola Usuarios
y equipos de Active Directory sobre la OU usuarios. En el laboratorio
se crearon dos cuentas de prueba: Deliby D. pineda y Jonathan J.
Ramirez.

![Usuarios creados](./imagenes/02-ad-usuarios-creados.png)

Las cuentas se configuraron con contraseña inicial y la opción de
cambio en el primer inicio de sesión, que es la práctica recomendada
en entornos de Active Directory para cuentas recién creadas.

## Unión de un equipo al dominio

Para validar que el controlador de dominio y el DNS funcionan
correctamente, se unió un equipo cliente al dominio. El equipo elegido
fue VENTAS-01 y se unió al dominio contoso.com desde la ventana de
Propiedades del sistema, apartado Cambios en el dominio o el nombre
del equipo.

![Unión de VENTAS-01 al dominio](./imagenes/02-ad-union-equipo-dominio.png)

Tras pulsar Aceptar, el sistema mostró el mensaje "Se unió
correctamente al dominio contoso.com", confirmando que la integración
se completó sin errores. Este paso valida de forma práctica tres
cosas a la vez: que el DNS resuelve el nombre del dominio, que el
DC01 está replicando correctamente y que la máquina cliente negocia
el join sin problemas de credenciales ni de red.

## Verificación con gpresult

Una vez el usuario Deliby inició sesión en VENTAS-01, se ejecutó el
comando gpresult /r desde una ventana de símbolo del sistema para
confirmar que el equipo recibe correctamente las directivas y que el
usuario pertenece a los grupos esperados.

![Resultado de gpresult /r](./imagenes/02-ad-gpresult-grupos.png)

La salida muestra varios datos útiles para validar el entorno.
Aparece el nombre del equipo (VENTAS-01), el perfil del usuario
(deliby), la OU a la que pertenece el usuario dentro del dominio
(Usuarios, dentro de contoso.com) y la fecha en la que se aplicó la
directiva por última vez. En la sección de grupos de seguridad se
confirma que el usuario pertenece a Usuarios del dominio, Usuarios y
Usuarios autentificados, que son los grupos predeterminados que todo
usuario del dominio recibe al ser creado.

## Resumen

Con los pasos descritos en este apartado el dominio contoso.com queda
operativo con la jerarquía de OUs definida, los grupos de seguridad
creados, los usuarios dados de alta y un equipo cliente validado
dentro del dominio. Las secciones siguientes del repositorio (GPOs,
seguridad, servicios) se apoyan directamente sobre esta base.
