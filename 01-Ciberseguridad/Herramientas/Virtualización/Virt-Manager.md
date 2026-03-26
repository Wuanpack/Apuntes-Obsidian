---
tags:
  - virtualizacion/virt-manager
---

## ¿Qué es? 

Virt-Manager (Virtual Machine Manager) es una interfaz gráfica de escritorio ligera para gestionar máquinas virtuales (VM) en Linux, enfocada principalmente en KVM, pero compatible también con Xen y LXC.

Utiliza la biblioteca libvirt para crear, editar, iniciar y detener máquinas virtuales, además de monitorear el rendimiento en tiempo real y gestionar redes/almacenamiento.

## KVM/QEMU

KVM (Kernel-based Virtual Machine) y QEMU (Quick Emulator) son tecnologías de virtualización de código abierto en Linux que, al trabajar juntas, permiten crear máquinas virtuales de alto rendimiento. KVM transforma el kernel de Linux en un hipervisor, gestionando la CPU y memoria, mientras que QEMU emula el hardware (disco, red, video)

---

## Instalación de Virt-Manager (KVM/QEMU)

### 1. Verificar que el CPU soporte virtualización

```bash
egrep -c '(vmx|svm)' /proc/cpuinfo
```

Tiene que devolver un valor mayor a 0 . `vmx` es Intel, `svm` es AMD.

### 2. Instalar KVM y Virt-Manager

```bash
sudo dnf install @virtualization -y
```

Ese grupo instala todo de una vez: KVM, QEMU, libvirt y Virt-Manager.

### 3. Iniciar y habilitar el servicio

```bash
sudo systemctl enable --now libvirtd
```

### 4. Verificar que esté corriendo

```bash
sudo systemctl status libvirtd
```

### 5. Agregar el usuario al grupo libvirt

```bash
sudo usermod -aG libvirt $USER
sudo usermod -aG kvm $USER
```

### 6. Abrir Virt-Manager

```bash
virt-manager
```

### 7. Crear una máquina virtual

Una vez abierto:

1. Click en **"Nueva máquina virtual"** (ícono de monitor con +)
2. Selecciona **"Archivo de imagen ISO local"**
3. Busca la ISO que quieras instalar
4. Asigna RAM y CPUs
5. Crea o selecciona un disco virtual
6. Click en **"Finalizar"**

---
