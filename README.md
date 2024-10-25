# Ansible networking configuration

Deploying and configuring of cloud and networking resources using Ansible and Equinix.

## Project Setup

Make sure to setup a Python virtual environment for the project.

```bash
$ python3.12 -m venv .venv
.... setup ....

/user/repo $ source .venv/bin/activate

(.venv) /user/repo $ which python
/user/repo/.venv/bin/python

(.venv) /user/repo $ python --version
Python 3.12.7

```

Install Ansible and playbook dependencies.

``` bash
(.venv) $ pip install ansible==6.7.0
(.venv) $ ansible-galaxy collection install equinix.cloud
(.venv) $ pip install -r https://raw.githubusercontent.com/equinix/ansible-collection-equinix/main/requirements.txt
```

### Setting an Equinix API Key

Make sure to create an Equinix API key via the console and export it to your shell before running Ansible.

```bash
(.venv) $ export METAL_AUTH_TOKEN="YOUR TOKEN"
(.venv) $ echo $METAL_AUTH_TOKEN
YOUR TOKEN
```

### Creating Equinix SSH keys

You should generate a new ssh key pair for your Equinix connections. You can do this by following the prompts of the `ssh-keygen` command. For this project you should store these keys in the `keys` directory with the names `equinix_id_ed25519` and `equinix_id_ed25519.pub`.

Make sure your SSH keys are only readable by your own user using the following command on the keys

``` bash
(.venv) $ chmod 666 ./keys/equinix_id_ed25519 ./keys/equinix_id_ed25519.pub
```

### Updating Ansible var file

You will want to update the `main.vars.yml` file with values matching your Equinix project ID and SSH key id.

If you need to find out the ID of your key you can use the following ansible playbook to output all of the ssh keys in your Equinix project

``` bash
(.venv) $ ansible-playbook -i ./inventory.equinix.yml ./playbooks/project-info.yml
```

## Running playbooks

All Ansible playbooks are stored in the `playbooks` directory. You can run them using the following command.

``` bash
(.venv) $ ansible-playbook -i ./inventory.equinix.yml ./playbooks/<filename>
```

The following playbooks are also available for you to run once you have setup the project prerequisite.

* [`project-info.yml`](./playbooks/project-info.yml) - Gather information about your Equinix project like the SSH key ID
* [`deploy.yml`](./playbooks/deploy.yml) - Provision Equinix metal devices onto your account
* [`destroy.yml`](./playbooks/destroy.yml) - Delete any Equinix platform resources that are deployed by the project
* [`networking-configure.yml`](./playbooks/networking-configure.yml) - Configure private VLAN networking between metal devices
* [`networking-modify.yml`](./playbooks/networking-modify.yml) - Modify the VLAN connectivity of metal devices
* [`test-connectivity`](./playbooks/test-connectivity.yml) - Run a ping test between metal devices over the VLAN network
