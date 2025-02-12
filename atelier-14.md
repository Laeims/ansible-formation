# Exercice

myvars1.yml
```
---  # vars1.yml

- hosts: localhost
  gather_facts: false

  vars:
    voiture: "Chevrolet Impala SS 1967"
    moto: "OUI"

  tasks:
    - debug:
        msg: "Voiture: {{voiture}}, Moto: {{moto}}"

...

```

myvars2.yml
```
---  # myvars2.yml

- hosts: localhost
  gather_facts: false

  tasks:

    - name: Define variables
      set_fact:
        voiture: "Chevrolet Impala SS 1967"
        moto: "OUI"

    - debug:
        msg: "Voiture: {{voiture}}, Moto: {{moto}}"

...

```

myvars3.yml
```
---  # myvars3.yml

- hosts: localhost
  gather_facts: false

  tasks:
    - debug:
        msg: "Voiture: {{voiture}}, Moto: {{moto}}"

...

```
mkdir -v ~/ansible/projets/ema/group_vars
vim group_vars/all.yml
```
---  # group_vars/all.yml

voiture: "Chevrolet Impala SS 1967"
moto: "OUI"

...
```

display_user.yml
```
---  # display_user.yml

- hosts: localhost
  gather_facts: false

  vars_prompt:

    - name: user
      prompt: val for user
      default: microlinux
      private: false

    - name: password
      prompt: val for password
      default: yatahongaga
      private: true

  tasks:
    - debug:
        msg: "user is {{user}}, mdp is {{password}}"

...
```
