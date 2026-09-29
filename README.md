# Pi-NUT
Ansible playbook to install NUT on a Raspberry Pi.

## 1. Add user to sudoers

Create a sudoers drop-in file for the `nut` user:

```bash
sudo visudo -f /etc/sudoers.d/nut
```

Add the following line:

```text
nut ALL=(ALL) NOPASSWD: ALL
```

## 2. Set a static IP

Edit the netplan config:

```bash
sudo nano /etc/netplan/99-nut.yaml
```

Use this configuration:

```yaml
network:
  version: 2
  ethernets:
    eth0:
      optional: true
      addresses:
        - 192.168.3.5/24
      routes:
        - to: default
          via: 192.168.3.1
      nameservers:
        addresses:
          - 192.168.3.1
```

Apply the changes:

```bash
sudo netplan apply
```

## 3. Clone repo
```bash
git clone git@github.com:Kenny1217/pi-nut.git
cd pi-nut
```

## 4. Run Ansible playbook

```bash
ansible-playbook playbooks/main.yml --ask-vault-pass
```
