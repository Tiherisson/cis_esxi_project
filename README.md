# Ansible Role: CIS VMware ESXi 8 Benchmark

![Ansible](https://img.shields.io/badge/ansible-role-blue?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)

Ce projet contient un **rôle Ansible** pour appliquer les recommandations de sécurité du **CIS VMware ESXi 8 Benchmark v1.2.0**.

## Fonctionnalités

Le rôle `cis_esxi` applique les configurations suivantes sur vos hôtes ESXi :

- **Base** : Configuration NTP, restrictions TPS.
- **Management** : Désactivation SSH/Shell/MOB, Timeouts de session, Bannières de login.
- **Logging** : Configuration du Syslog distant.
- **Réseau** : Sécurisation des vSwitches (Rejet Promiscuous/Forged/MAC Changes).
- **Virtual Machine** : Isolation, Désactivation copier/coller/D&D, Limites de logs (Appliqué à toutes les VMs).

## Pré-requis

- Ansible avec la collection `community.vmware`.
- Accès HTTPS (443) aux hôtes ESXi.
- Compte utilisateur avec privilèges d'administration.

## Installation

```bash
git clone https://github.com/Tiherisson/cis_esxi_project
cd cis_security_project/roles
# (Copiez le rôle cis_esxi si nécessaire)
```

## Utilisation

1. Définissez vos hôtes ESXi dans l'inventaire :
   ```ini
   [esxi_hosts]
   esxi01.example.com ansible_user=root ansible_password=secret
   ```

2. Lancez le playbook :
   ```bash
   ansible-playbook cis_esxi_hardening.yml
   ```

## Variables Principales

| Variable | Description | Défaut |
|----------|-------------|--------|
| `cis_esxi_ntp_servers` | Liste des serveurs NTP | `[]` |
| `cis_esxi_disable_ssh` | Désactive le service SSH | `true` |
| `cis_esxi_enable_ntp` | Active le service NTP | `true` |
| `cis_esxi_remote_syslog`| Serveur Syslog distant | `""` |
| `cis_esxi_shell_timeout`| Timeout Shell ESXi (sec) | `600` |

*(Voir `roles/cis_esxi/defaults/main.yml` pour tout)*
