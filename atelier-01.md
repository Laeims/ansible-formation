
# Exercice 01

vagrant up ubuntu \
vagrant ssh ubuntu  
sudo apt update    
apt-cache search --names-only ansible  
sudo apt install -y ansible \
ansible --version  
exit  
vagrant destroy -f ubuntu  

on note une version d'ansible en **2.10.8**  

# Exercice 02

vagrant up ubuntu  
vagrant ssh ubuntu  
sudo apt update  
sudo apt-add-repository ppa:ansible/ansible  
apt-cache search --names-only ansible  
sudo apt install -y ansible  
ansible --version  
exit  
vagrant destroy -f ubuntu  
  
on note une version d'ansible en **2.17.8**  

# Exercice 03

vagrant up rocky  
vagrant ssh rocky  
python3 -m venv ~/.venv/ansible  
source ~/.venv/ansible/bin/activate  
pip install --upgrade pip  
pip install ansible  
ansible --version  
deactivate  
exit  
vagrant destroy -f rocky  

on note une version d'ansible en **2.15.13**  




