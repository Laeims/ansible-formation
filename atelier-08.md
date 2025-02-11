# Exercice

Chaque partie est réalisée 2 fois, si il ya une difference elle est noté dans la partie **retour**  


ansible all -m package -a "name=tree"  
**retour :**  passage de Changed à Checked pour les trois  

ansible all -m package -a "name=git"  
**retour :**  passage de Changed à Checked pour les trois  

ansible all -m package -a "name=nmap"  
**retour :**  passage de Changed à Checked pour les trois  

---  

ansible all -m package -a "name=tree state=absent"    
**retour :**  passage de Changed à Checked pour les trois   

ansible all -m package -a "name=git state=absent"   
**retour :**  passage de Changed à Checked pour les trois   

ansible all -m package -a "name=nmap state=absent"  
**retour :**  passage de Changed à Checked pour les trois   

---  

ansible all -m copy -a "src=/etc/fstab dest=/tmp/test3.txt"   
**retour :**  passage de Changed à Checked pour les trois   

---  

ansible all -m file -a "dest=/tmp/test3.txt state=absent"   
**retour :**  passage de Changed à Checked pour les trois   

---  

ansible all -m command -a "df -h /"  
**retour :**  Est toujours marqué en Changed  

