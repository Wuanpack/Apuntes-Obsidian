---
tags:
  - tryhackme
---

1. Antes de instalar OpenVPN, verificar que los paquetes estén actualizados:
```bash
sudo dnf update && sudo dnf upgrade
```
2. Descargar el archivo de configuración (username.ovpn)
3. Correr el archivo con 
   ```bash
   sudo openvpn ~/Descargas/username.ovpn
   ```
4. Testear la conexión ejecutando `ping 192.168.128.1` en la terminal. Si la conexión es exitosa, debería aparecer una respuesta que aparezca como `PING 192.168.128.1 (192.186.128.1):56 data bytes`.
5. Cerrar la terminal con el `openvpn` corriendo cortará la conexión, por lo que hay que abrir otra terminal para trabajar.