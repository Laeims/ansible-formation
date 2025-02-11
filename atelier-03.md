# Exercice

sudo vim /etc/hosts

```
# /etc/hosts
127.0.0.1      localhost.localdomain  localhost
192.168.56.10  ansible.sandbox.lan    control
192.168.56.20  rocky.sandbox.lan      target01
192.168.56.30  debian.sandbox.lan     target02
192.168.56.40  suse.sandbox.lan       target03
```
ssh-keygen
ssh-copy-id vagrant@target-01
ssh-copy-id vagrant@target-02
ssh-copy-id vagrant@target-03

ansible all -i target01,target02,target03 -m ping

On obtient un triple succes et un warning.
