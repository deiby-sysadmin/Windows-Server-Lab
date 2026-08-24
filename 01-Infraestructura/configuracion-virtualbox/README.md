# 🖥️ Configuración de VirtualBox — Infraestructura del Laboratorio

En esta sección se documenta la configuración base de las máquinas virtuales
utilizadas en el laboratorio de **Windows Server 2022**. Todo el entorno se
ejecuta sobre **Oracle VM VirtualBox**, con una red interna que aísla las
comunicaciones entre los equipos del dominio y una interfaz **NAT** que
proporciona salida a Internet.

---

## 🧩 Equipos del laboratorio

| Equipo               | Sistema Operativo        | Rol                                          |
|----------------------|--------------------------|----------------------------------------------|
| `Windows Server`     | Windows Server 2012 (64) | Controlador de dominio (DC01)                |
| `Window-Client-WS`   | Windows 10 (64-bit)      | Cliente unido al dominio (PC01)              |
| `SMR-Client Backup`  | —                        | Cliente de pruebas para backups              |

---

## 🌐 Topología de red

El laboratorio utiliza **dos adaptadores de red** por máquina virtual:

- **Adaptador 1:** Red interna `Windows_Ser_Practicas` (comunicación entre VMs)
- **Adaptador 2:** NAT (salida a Internet para actualizaciones)

---

## 📸 Capturas de la configuración

A continuación se muestran las imágenes que documentan paso a paso la
configuración del entorno en VirtualBox.

### 🔧 Configuración del servidor — DC01

![Configuración DC01](./Imagenes/01-infraestructura-configuracion-DC01.png)

*Configuración general de la máquina virtual `Windows Server`. Se asignaron
**4 GB de RAM**, **2 procesadores**, **50 GB de disco** y controladora
gráfica VBoxSVGA. La aceleración de paravirtualización está habilitada
(Hyper-V) para mejorar el rendimiento.*

---

### 🌐 Configuración de IP estática — DC01

![Configuración IP DC01](./Imagenes/01-infraestructura-configuracion-IP-DC01.png)

*Asignación de dirección IP estática en el adaptador de red del servidor,
fundamental para que actúe como **Controlador de Dominio** y **servidor
DNS** dentro de la red del laboratorio.*

| Parámetro             | Valor         |
|-----------------------|---------------|
| Dirección IP          | `192.168.0.3` |
| Máscara de subred     | `255.255.255.0` |
| Puerta de enlace      | `192.168.0.2` |
| Servidor DNS preferido| `127.0.0.1`   |

> ⚠️ El servidor DNS apunta a `127.0.0.1` (localhost) ya que este equipo
> será quien ofrezca el servicio DNS tras la promoción a DC.

---

### 🔧 Configuración del cliente — PC01

![Configuración PC01](./Imagenes/01-infraestructura-configuracion-PC01.png)

*Configuración general de la máquina virtual cliente `Window-Client-WS`,
basada en **Windows 10 (64-bit)** con **2 GB de RAM** y **50 GB de disco**.
Esta máquina será posteriormente **unida al dominio** del laboratorio.*

---

### 📋 Plataforma de virtualización

![Plataforma de virtualización](./Imagenes/01-infraestructura-plataforma-virtualizacion.png)

*Vista general del **VirtualBox Manager** con las tres máquinas virtuales
del laboratorio: `SMR-Client Backup`, `Windows Server` y `Window-Client-WS`,
mostrando su estado (apagadas / guardadas) en el momento de la captura.*

---

### 🔌 Red del laboratorio

![Red del laboratorio](./Imagenes/01-infraestructura-red-laboratorio.png)

*Configuración de los adaptadores de red de las VMs. Cada equipo dispone
de un adaptador **Intel PRO/1000 MT Desktop** conectado a la red interna
`Windows_Ser_Practicas`, y un segundo adaptador en modo **NAT** para
acceso a Internet.*

---

## ✅ Resultado esperado

Tras esta configuración base, el laboratorio queda preparado para:

1. Promocionar `Windows Server` a **Controlador de Dominio**.
2. Unir `Window-Client-WS` al dominio creado.
3. Desplegar los servicios y políticas documentados en las siguientes
   secciones del repositorio (`02-Active-Directory`, `03-GPOs`, etc.).

---

## 🧭 Navegación

⬅️ [`01-Infraestructura`](../) · 🏠 [`README principal`](../../../README.md)


