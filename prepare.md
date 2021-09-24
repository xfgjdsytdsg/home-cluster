# prepare

```bash
# storage
sudo apt install linux-headers-amd64 firmware-realtek

sudo apt install zfsutils-linux

ls -l /dev/disk/by-id/

sudo zpool create tank -o ashift=12 raidz2 \
ata-WDC_WD10EFRX-68FYTN0_WD-WCC4J0SEF254 \
ata-WDC_WD10EFRX-68FYTN0_WD-WCC4J0SEFN9A \
ata-WDC_WD10EFRX-68FYTN0_WD-WCC4J0TDU34X \
ata-WDC_WD10EFRX-68FYTN0_WD-WCC4J0TDUPT3 \
ata-WDC_WD10EFRX-68FYTN0_WD-WCC4J7VF4NUS

sudo zfs set compression=lz4 tank
sudo zfs set xattr=sa tank
sudo zfs set atime=off tank
sudo zpool set autoexpand=on tank

sudo zfs create tank/PersistentVolumeClaims
sudo zfs set xattr=sa dnodesize=auto tank/PersistentVolumeClaims

sudo apt install nfs-kernel-server
sudo zfs set sharenfs="rw=192.168.0.0/24,ro=10.0.0.0/8" tank/PersistentVolumeClaims
sudo zfs share tank/PersistentVolumeClaims
sudo zfs set sharenfs=on tank/PersistentVolumeClaims
sudo showmount -e 127.0.0.1

```

```bash
pip install -r requirements.txt
ansible-galaxy install -r requirements.yml
ansible-playbook -i inventory/home-cluster/hosts.yml playbooks/kubernetes/debian-prepare.yml
ansible-playbook -i inventory/home-cluster/hosts.yml playbooks/kubernetes/k3s-install.yml
```

[template-cluster-k3s](https://github.com/k8s-at-home/template-cluster-k3s)

```bash
yay -S --needed kubectl helm sops gnupg pinentry kustomize python-pre-commit prettier
yay -S flux-bin
go install github.com/go-task/task/v3/cmd/task@latest

yay -S direnv
eval "$(direnv hook zsh)"
direnv allow
chmod 400 ~/.kube/config 
chmod 400 kubeconfig
exec $SHELL  
```
