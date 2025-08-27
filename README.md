# SRE Challenge - Vagrant + Ansible

The project automates provisioning of the sample application using **Ansible** and **Vagrant**, replacing the provided `provision.sh` script.


## Prerequisites 
- [Vagrant](https://developer.hashicorp.com/vagrant/downloads)  
- [VirtualBox](https://www.virtualbox.org/) (or any Vagrant provider)  
- [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)  
- Ansible `community.docker` collection:  
  ```bash
  ansible-galaxy collection install community.docker

## Project Overview
- Infrastructure provisioning is done via **Ansible roles**.  
- Application is deployed using **Docker + Docker Compose**.  
- All tasks are **idempotent** and structured into reusable roles. 

## Bring it up (recommended)
1. Clone the repository
```bash
   git clone https://github.com/ChepkemoiPeris/sre-challenge-submission.git
   cd sre-challenge-submission
```
2. Start and provision the VM:
```bash
    vagrant up
```
   This will Install required system dependencies,Install and configure Docker and Deploy the sample app using Docker Compose

3. Access the app:
   - From your host: http://192.168.56.10:8080/

4. Health endpoint:
   http://192.168.56.10:8080/healthz

##  Debugging / Troubleshooting
1. SSH into the VM if needed:

   ```bash
   vagrant ssh
   ```

2. Manage the stack manually (inside the VM):

   ```bash
   cd /vagrant
   docker compose ps
   docker compose logs -f web
   docker compose up -d --build
   ```
3. Verify Docker is working:
```bash
   docker version
   docker ps
```
4. Re-run Ansible provisioning if needed:
```bash
vagrant provision
```
 ##  Customization
 Default variables, such as the Docker user or the compose_file path are defined in:

roles/*/defaults/main.yaml
 

If you want to override them:

Update values in roles/*/vars/main.yaml instead of editing role files directly.

Then re-run provisioning:
```bash
vagrant provision
```