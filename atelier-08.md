# Exercice

## ! Non terminé !

Chaque partie est réalisée 2 fois, si il ya une difference elle est noté dans la partie **retour**  


ansible all -m package -a "name=tree"  
**retour :**  

ansible all -m package -a "name=git"  
**retour :**  

ansible all -m package -a "name=nmap"  
**retour :**  

---  

ansible all -m package -a "name=tree" state=absent  
**retour :**  

ansible all -m package -a "name=git" state=absent  
**retour :**  

ansible all -m package -a "name=nmap" state=absent   
**retour :**  

---  

ansible all -m copy -a "src=/etc/fstab dest=/tmp/test3.txt"   
**retour :**  

---  

ansible all -m file -a "dest=/tmp/test3.txt state=absent"   
**retour :**  

---  

ansible all -m command -a "df -h /"  
**retour :**  

