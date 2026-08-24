# Laboratorio Windows Server 2022

Repositorio que documenta un laboratorio completo de administraci&oacute;n
de sistemas sobre Windows Server 2022. El entorno se ejecuta sobre
m&aacute;quinas virtuales en VirtualBox, con un controlador de
dominio, un cliente Windows 10 y un cliente adicional para pruebas
de backup. Toda la documentaci&oacute;n est&aacute; organizada por
&aacute;reas de trabajo, con capturas reales de cada paso y comandos
de validaci&oacute;n ejecutados desde el lado cliente.

El objetivo es mostrar, de principio a fin, c&oacute;mo se monta y
se administra un dominio corporativo real: desde la configuraci&oacute;n
de la infraestructura de red hasta la monitorizaci&oacute;n del
servidor, pasando por la gesti&oacute;n de identidades, las
pol&iacute;ticas, la seguridad y la automatizaci&oacute;n.

## El entorno

- Controlador de dominio: AD01, con los servicios AD DS, DNS, DHCP
  y WSUS levantados.
- Cliente del dominio: Window-Client-WS, Windows 10 unido a
  contoso.com.
- Cliente adicional: SMR-Client Backup, usado para las pruebas de
  respaldo.
- Red interna: 192.168.0.0/24 sobre un adaptador de VirtualBox en
  modo red interna.
- Dominio: contoso.com, con nivel funcional Windows 2016.

## Temas cubiertos

- Infraestructura de virtualizaci&oacute;n con VirtualBox y
  configuraci&oacute;n de red.
- Active Directory: dise&ntilde;o de OUs, creaci&oacute;n de
  usuarios y grupos, uni&oacute;n de equipos al dominio.
- Directivas de grupo (GPOs): creaci&oacute;n, edici&oacute;n,
  vinculaci&oacute;n y validaci&oacute;n con `gpresult`.
- Seguridad: auditor&iacute;a de eventos, firewall con seguridad
  avanzada y pol&iacute;ticas de cuenta.
- Automatizaci&oacute;n con PowerShell y tareas programadas.
- Servicios de infraestructura: DHCP, DNS y WSUS.
- Monitorizaci&oacute;n del servidor con herramientas nativas de
  Windows.

## C&oacute;mo est&aacute; organizado

El repositorio se divide en siete carpetas, una por cada &aacute;rea
de trabajo. Dentro de cada una hay un README que explica el contexto,
muestra las capturas de los pasos dados y, cuando aplica, cierra con
un comando de validaci&oacute;n que confirma que todo funciona. Las
capturas de pantalla est&aacute;n en la carpeta `Imagenes/` de cada
secci&oacute;n, numeradas para mantener el orden de lectura.

La forma natural de recorrerlo es seguir el orden num&eacute;rico de
las carpetas, que va de la infraestructura base hasta la
monitorizaci&oacute;n. Pero cada secci&oacute;n se entiende de
forma independiente y se puede leer suelta sin perder el hilo.


