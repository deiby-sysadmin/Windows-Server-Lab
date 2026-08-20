# Infraestructura del Laboratorio Windows Server 2022

Este documento describe la infraestructura base del laboratorio utilizado para la administración de Windows Server 2022. Aquí se detallan los componentes principales, la topología general y las máquinas virtuales que forman parte del entorno.

## Componentes del laboratorio

- **Windows Server 2022** con interfaz gráfica.
- **Cliente Windows 1** unido al dominio.
- **Cliente Windows 2** unido al dominio.
- Red interna configurada en VirtualBox para comunicación entre las máquinas.
- Adaptadores adicionales según sea necesario (NAT, puente, etc.).

## Objetivo de esta sección

Documentar la estructura del laboratorio antes de entrar en configuraciones específicas como Active Directory, GPOs, seguridad, automatización y servicios.

## Configuración de red del laboratorio

El laboratorio utiliza una red interna en VirtualBox para permitir la comunicación entre el servidor y los clientes Windows. La configuración de red se basa en los siguientes adaptadores:

### Adaptadores de red utilizados

- **Adaptador 1 (Servidor):** Red interna para comunicación con los clientes.
- **Adaptador 2 (Servidor):** NAT para permitir acceso a Internet desde el servidor.
- **Adaptador 1 (Clientes):** Red interna para comunicación con el servidor y unión al dominio.

### Objetivo de esta configuración

La red interna garantiza que todas las máquinas puedan comunicarse entre sí sin interferencias externas, mientras que el adaptador NAT del servidor permite realizar actualizaciones, descargas y configuraciones que requieren acceso a Internet.
