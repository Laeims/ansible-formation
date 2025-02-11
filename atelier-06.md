# Exercice

sudo vim /etc/hosts

```
# /etc/hosts
127.0.0.1      localhost.localdomain  localhost
192.168.56.10  00.sandbox.lan    control
192.168.56.20  01.sandbox.lan      target01
192.168.56.30  02.sandbox.lan     target02
192.168.56.40  03.sandbox.lan       target03
```

ssh-keygen

ssh-copy-id vagrant@target01  
ssh-copy-id vagrant@target02  
ssh-copy-id vagrant@target03  

sudo apt update  
sudo apt install ansible  
sudo apt install -y direnv  
echo 'eval "$(direnv hook bash)"' >> ~/.bashrc  
source ~/.bashrc  

ansible all -i target01,target02,target03 -m ping  
mkdir ~/monprojet  
touch ~/monprojet/ansible.cfg  
vim ~/monprojet/ansible.cfg   

echo 'export ANSIBLE_CONFIG=$(expand_path ansible.cfg)' > .envrc  
direnv allow  
mkdir -v ~/journal  
cd  
echo 'export ANSIBLE_CONFIG=$(expand_path ./monprojet/ansible.cfg)' > .envrc  
direnv allow  

```
[defaults]
inventory = ./inventory
log_path = ~/journal/ansible.log
```

ansible all -i target01,target02,target03 -m ping  
cat ~/journal/ansible.log  

vim ~/monprojet/hosts  
```
[testlab]
target01
target02
target03

[testlab:vars]
ansible_python_interpreter=/usr/bin/python3
ansible_user=vagrant
ansible_become=yes
```
ansible all -m ping  
ansible all -a "head -n 1 /etc/shadow"  

```
target03 | CHANGED | rc=0 >>
root:*:19769:0:99999:7:::
target02 | CHANGED | rc=0 >>
root:!$y$j9T$cnYeciMny4hdKr8syHPzE.$hxcd/wjU5wCDVKm1HbZGS0Uy/b7B9Nwgiz.JiqspIE6:19732:0:99999:7:::
target01 | CHANGED | rc=0 >>
root:!$6$OtVuw4E9xL/Nzile$vACSEse85MEa7qevVkcmccS5ZV2i7Z7cZFXKUi0dz5rcKqpiZzLskZycIsypNh9uL5Iw14DIcUQwDp0Oucduw0:19733::::::
```
exit  
vagrant destroy -f  

