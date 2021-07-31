# Ansible Setup

Control node: macOS latop, homebrew, python3.8
Install ansible:

```
$ python3 -m venv .venv
$ source .venv/bin/activate
$ pip install ansible ansible-lint
```

## Inventory

Setup a host Inventory: `inventory.yml`

```
all:
  hosts:
    hanalei:
      ansible_port: 22
      ansible_user: ubuntu
      ansible_host: XXX.XXX.XXX.XXX
      ansible_ssh_private_key_file: foo.pem
```

## Test

```
$ ansible -i inventory.yml all -a "/bin/echo hello"
hanalei | CHANGED | rc=0 >>
hello

$ ansible -i inventory.yml all -m setup
... <cool stuff>
```

Lint the playbooks:

```
$ ansible-lint provision.yml
```

## Provision the hosts in inventory.yml

```
$ ANSIBLE_NOCOWS=1 ansible-playbook -i inventory.yml provision.yml
...
```
