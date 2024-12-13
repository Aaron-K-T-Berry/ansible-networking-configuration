# Ansible networking configuration

Deploying and configuring of cloud and networking resources using Ansible and AWS.

## Project Setup

Make sure to set up a Python virtual environment for the project:

```bash
$ python3.12 -m venv .venv
.... setup ....

/user/repo $ source .venv/bin/activate

(.venv) /user/repo $ which python
/user/repo/.venv/bin/python

(.venv) /user/repo $ python --version
Python 3.12.7

```

Install Ansible and playbook dependencies:

``` bash
(.venv) $ pip install ansible==11.1.0
(.venv) $ ansible-galaxy collection install amazon.aws
(.venv) $ pip install -r https://raw.githubusercontent.com/ansible-collections/community.aws/refs/heads/main/requirements.txt
```

## Running playbooks

All Ansible playbooks are stored in the `playbooks` directory. You can run them using the following command:

``` bash
(.venv) $ ansible-playbook -i ./inventory.aws.yml ./playbooks/<filename>
```

The following playbooks are also available for you to run once you have set up the project prerequisites:

* [`deploy.yml`](./playbooks/deploy.yml) - Provision AWS instances onto your account
* [`destroy.yml`](./playbooks/destroy.yml) - Delete any AWS resources that are deployed by the project
* [`networking-initial.yml`](./playbooks/networking-configure.yml) - Configure private connectivity to EC2 for development
* [`networking-modified.yml`](./playbooks/networking-modified.yml) - Modify the EC2 security groups
* [`test-connectivity.yml`](./playbooks/test-connectivity.yml) - Run a ping test between EC2 instances' private and public IP addresses
