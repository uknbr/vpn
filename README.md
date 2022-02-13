# My VPN setup

- Create dedicated user with random generated password
- Install basic packages
- Support CentOS and Ubuntu
- Install Docker and Docker Compose
- Configure SSH with non default port and fail2ban
- Clone and deploy amazing project (OpenVPN + PiHole)

### Configuration
1. setup.yaml
2. vpn.ini

### Usage

#### Bateries included

```bash
ansible-playbook setup.yaml
```

#### VPN configuration

```bash
ansible-playbook setup.yaml --extra-vars "vpn_name=foo vpn_password=bar"
```

#### Keep SSH with default config (insecure)

```bash
ansible-playbook setup.yaml --skip-tags ssh
```

#### Only VPN (make sure you already have all dependencies)

```bash
ansible-playbook setup.yaml --tags vpn
```