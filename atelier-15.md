# Exercice

kernel.yml
```
---  # kernel.yml

- hosts: all
  gather_facts: false

  tasks:

    - name: Noyaux
      command: uname -a
      changed_when: false
      register: uname_cmd

    - debug:
        msg: "{{uname_cmd}}"

...
```
Variante avec le parametre var :
```
 - debug:
        var: uname_cmd.stdout_lines
```

packages.yml
```
---  # packages.yml

- hosts: rocky,suse
  gather_facts: false

  tasks:

    - name: Paquets totaux
      shell: rpm -qa | wc -l
      changed_when: false
      register: pt_cmd

    - debug:
        msg: "{{pt_cmd}}"
...


```
