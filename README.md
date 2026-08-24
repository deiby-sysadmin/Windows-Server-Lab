# Laboratorio Windows Server 2022

Repositorio que documenta un laboratorio completo de administraci&oacute;n
de sistemas sobre Windows Server 2022. El entorno se ejecuta en
m&aacute;quinas virtuales sobre VirtualBox, con un controlador de
dominio, un cliente Windows 10 y un cliente adicional para pruebas
de backup. Toda la documentaci&oacute;n est&aacute; organizada por
&aacute;reas de trabajo, con capturas reales de cada configuraci&oacute;n
y comandos de validaci&oacute;n ejecutados desde el lado cliente.

El objetivo del repositorio es mostrar c&oacute;mo se monta y se
administra un dominio corporativo de principio a fin: desde la
configuraci&oacute;n de la infraestructura de red hasta la
monitorizaci&oacute;n del servidor, pasando por la gesti&oacute;n de
identidades, las pol&iacute;ticas, la seguridad y la automatizaci&oacute;n.

## Entorno del laboratorio

- Controlador de dominio: AD01 (Windows Server 2012 R2 dentro del
  examen 70-740, actualizado a 2022).
- Cliente del dominio: Window-Client-WS (Windows 10).
- Cliente adicional: SMR-Client Backup.
- Red interna: 192.168.0.0/24 sobre VirtualBox.
- Dominio: contoso.com.
- Direcci&oacute;n IP del DC: 192.168.0.3 (fija en la tarjeta de
  red interna).

## Contenido del repositorio

| Secci&oacute;n | Contenido |
|----------------|-----------|
| [01-Infraestructura](./01-Infraestructura/README.md) | Configuraci&oacute;n de las m&aacute;quinas virtuales en VirtualBox: hardware, redes, IP fija del DC01. |
| [02-Active-Directory](./02-Active-Directory/README.md) | Estructura de OUs, alta de usuarios y grupos de seguridad, uni&oacute;n de equipos al dominio via `System Properties`. |
| [03-GPOs](./03-GPOs/README.md) | Creaci&oacute;n de un GPO desde cero, vinculaci&oacute;n a una OU y validaci&oacute;n con `gpresult /r` desde el cliente. |
| [04-Seguridad](./04-Seguridad/README.md) | Auditor&iacute;a de inicio/cierre de sesi&oacute;n, revisi&oacute;n del firewall con WFAS, pol&iacute;ticas de cuenta (contrase&ntilde;a, bloqueo). |
| [05-Automatizaci&oacute;n](./05-Automatizaci&oacute;n/README.md) | Scripts de PowerShell: consulta de informaci&oacute;n del dominio y backup peri&oacute;dico programado en el Programador de tareas. |
| [06-Servicios](./06-Servicios/README.md) | DHCP con reservas, DNS con zonas directa e inversa del dominio, WSUS reci&eacute;n instalado. |
| [07-Monitorizaci&oacute;n](./07-Monitorizaci&oacute;n/README.md) | Visor de eventos, Monitor de rendimiento (`perfmon`), Monitor de recursos (`resmon`) y consola de Servicios. |

## Competencias t&eacute;cnicas demostradas

- Administraci&oacute;n de Active Directory: OUs, grupos, usuarios,
  uni&oacute;n al dominio, validaci&oacute;n con `gpresult`.
- Pol&iacute;ticas de grupo (GPO) y seguridad: directivas locales,
  auditor&iacute;as, bloqueo de cuentas, firewall avanzado.
- Servicios de infraestructura: DHCP, DNS, WSUS.
- Scripting en PowerShell: automatizaci&oacute;n con tareas
  programadas.
- Monitorizaci&oacute;n b&aacute;sica de servidor Windows con
  herramientas nativas.
- Virtualizaci&oacute;n con VirtualBox.

## C&oacute;mo recorrer el repositorio

Cada secci&oacute;n sigue el mismo esquema: una explicaci&oacute;n
introduce el contexto, las capturas muestran los pasos dados y los
comandos de validaci&oacute;n cierran cada tema confirmando que
todo funciona como se espera. Las im&aacute;genes est&aacute;n en la
carpeta `Imagenes/` de cada secci&oacute;n y est&aacute;n
numeradas con un prefijo de dos d&iacute;gitos para mantener el
orden l&oacute;gico de lectura.

Empezar por la secci&oacute;n 01 y avanzar en orden es la forma m&aacute;s
natural de seguir la evoluci&oacute;n del laboratorio, pero cada
secci&oacute;n funciona tambi&eacute;n de forma independiente para
quien llegue buscando un tema concreto.

