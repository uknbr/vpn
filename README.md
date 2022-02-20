# My VPN setup

- Create dedicated user with random generated password
- Install basic packages
- Support CentOS and Ubuntu
- Install Docker and Docker Compose
- Configure SSH with non default port and fail2ban
- Clone and deploy amazing project [(OpenVPN + PiHole)](https://github.com/Simonwep/openvpn-pihole)

### Configuration
1. vpn.yaml
2. vpn.ini
3. Vars
   * ./setup/roles/base/vars/main.yaml
   * ./setup/roles/container/vars/main.yaml
   * ./setup/roles/ssh/vars/main.yaml
   * ./setup/roles/vpn/vars/main.yaml

### Usage

#### Bateries included

```bash
ansible-playbook vpn.yaml
```

#### VPN configuration

```bash
ansible-playbook vpn.yaml --extra-vars "vpn_name=foo vpn_password=bar"
```

#### Keep SSH with default config (insecure)

```bash
ansible-playbook vpn.yaml --skip-tags ssh
```

#### Only VPN (make sure you already have all dependencies)

```bash
ansible-playbook vpn.yaml --tags vpn
```