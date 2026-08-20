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

## Máquinas virtuales del laboratorio

El entorno está compuesto por tres máquinas virtuales principales, cada una cumpliendo un rol específico dentro del dominio.

### Windows Server 2022 (Controlador de dominio)
- Rol principal: Controlador de dominio (AD DS).
- Servicios instalados: Active Directory, DNS, DHCP, políticas de grupo.
- Adaptadores de red: Red interna + NAT.
- Función: Gestionar el dominio, usuarios, grupos, políticas y servicios centrales.

### Cliente Windows 1
- Sistema operativo: Windows10.
- Rol: Equipo unido al dominio para pruebas de GPOs, inicio de sesión y recursos compartidos.
- Adaptador de red: Red interna.

### Cliente Windows 2
- Sistema operativo: Windows10.
- Rol: Segundo equipo unido al dominio para validar configuraciones y políticas en múltiples clientes.
- Adaptador de red: Red interna.

### Objetivo de esta configuración
Permitir la simulación de un entorno empresarial básico con un controlador de dominio y varios equipos cliente para aplicar políticas, probar servicios y validar configuraciones reales.

## Topología general del laboratorio

La topología del laboratorio está diseñada para simular un entorno empresarial básico donde un controlador de dominio gestiona varios equipos cliente dentro de una misma red interna.

### Estructura de la topología

- **Controlador de dominio (Windows Server 2022)**  
  Gestiona el dominio, usuarios, grupos, políticas y servicios esenciales como DNS y DHCP.

- **Clientes Windows**  
  Dos equipos unidos al dominio para validar configuraciones, políticas y servicios.

- **Red interna**  
  Permite la comunicación directa entre el servidor y los clientes sin depender de la red física del host.

- **Acceso a Internet (solo servidor)**  
  El servidor utiliza un adaptador NAT para actualizaciones y descargas necesarias.

### Objetivo de esta topología

Recrear un entorno controlado donde se puedan aplicar políticas de grupo, probar servicios, realizar automatizaciones y validar configuraciones de manera segura y aislada.

## Requisitos del laboratorio

Para que el entorno funcione correctamente, se necesitan los siguientes recursos mínimos:

### Hardware del equipo anfitrión
- Procesador con soporte para virtualización (Intel VT‑x o AMD‑V).
- 8 GB de RAM como mínimo (recomendado 16 GB para mayor fluidez).
- 60 GB de espacio libre en disco.
- Sistema operativo anfitrión compatible con VirtualBox.

### Recursos asignados a las máquinas virtuales
- **Windows Server 2022:** 2–4 GB de RAM, 2 núcleos de CPU, 40 GB de disco.
- **Clientes Windows:** 2 GB de RAM cada uno, 1 núcleo de CPU, 20 GB de disco.

### Software necesario
- VirtualBox o cualquier otro hipervisor compatible.
- ISO de Windows Server 2022.
- ISO de Windows para los clientes.
- Extensiones de VirtualBox 

### Objetivo de estos requisitos
Garantizar que el laboratorio funcione de manera estable y permita realizar todas las prácticas de administración de sistemas sin limitaciones técnicas.

