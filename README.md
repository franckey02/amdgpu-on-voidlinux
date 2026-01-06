# Guía para configurar amdgpu en Void Linux

## 🚀 **Pasos para activar amdgpu:**

### **1. Configurar parámetros del kernel:**
```bash
sudo nano /etc/default/grub
```
Agregar esto a `GRUB_CMDLINE_LINUX_DEFAULT`:
```bash
radeon.si_support=0 amdgpu.si_support=1 radeon.cik_support=0 amdgpu.cik_support=1
```
Actualizar GRUB:
```bash
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

### **2. Configurar initramfs (DRACUT):**
```bash
sudo nano /etc/dracut.conf.d/amdgpu.conf
```
Agregar:
```bash
omit_drivers+=" radeon "
add_drivers+=" amdgpu "
```
Reconstruir:
```bash
sudo dracut --force
```

### **3. Instalar drivers gráficos:**
```bash
sudo xbps-install mesa mesa-dri mesa-vulkan-radeon vulkan-loader vulkan-tools xf86-video-amdgpu
```

### **4. Reiniciar:**
```bash
sudo reboot
```

## ✅ **Verificar instalación:**
```bash
lsmod | grep amdgpu
vkcube
```

Testeado en amd r5 430
