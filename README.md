# Ai-Server-YouTube-Video
# ProxMox

```bash
nano /etc/default/grub
GRUB_CMDLINE_LINUX_DEFAULT="quiet intel_iommu=on iommu=pt"
```

```bash
update-grub
```

```bash
cat > /etc/modules-load.d/vfio.conf <<'EOF'
vfio
vfio_iommu_type1
vfio_pci
EOF
```

```bash
cat > /etc/modprobe.d/vfio-p100.conf <<'EOF'
options vfio-pci ids=10de:15f8 disable_vga=1
EOF
```

```bash
cat > /etc/modprobe.d/blacklist-nvidia.conf <<'EOF'
blacklist nouveau
blacklist nvidia
blacklist nvidiafb
blacklist nvidia_drm
blacklist nvidia_uvm
blacklist nvidia_modeset
EOF
```

```bash
update-initramfs -u -k all
reboot
```

# Ubuntu Or PopOs

```bash
sudo apt update && sudo apt full-upgrade -y
sudo apt install build-essential dkms linux-headers-$(uname -r) -y
sudo apt install nvidia-driver-580-server -y
sudo reboot
nvidia-smi
sudo apt install nvtop -y
```

# ollama

```bash
curl -fsSL https://ollama.com/install.sh | sh
```

```bash
sudo systemctl edit ollama
```

```ini
[Service]
Environment="OLLAMA_HOST=0.0.0.0:11434"
```

```bash
sudo systemctl daemon-reload
sudo systemctl restart ollama
```
