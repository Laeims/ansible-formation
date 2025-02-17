# Exercice

pkg-info.yml
```
---  # pkg-info.yml

- hosts: all

  tasks:

    - name: Gestionnaire
      debug:
        msg: >-
          Gestionnaire = {{ansible_pkg_mgr}}

...
```

python-info.yml  
```
---  # python-info.yml

- hosts: all

  tasks:

    - name: Python version
      debug:
        msg: >-
          Python version = {{ansible_python_version}}

...
```

dns-info.yml  
```
---  # dns-info.yml

- hosts: all

  tasks:

    - name: DNS
      debug:
        msg: >-
          DNS appelés = {{ansible_dns}}

...
```
