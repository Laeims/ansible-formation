# Exercices

chrony.yml
```
---  # chrony.yml

- hosts: all

  tasks:

    - name: Load distribution-specific parameters
      include_vars: >
        chrony_{{ansible_distribution|lower|replace(" ", "-") }}.yml

    - name: Update package information on Debian/Ubuntu
      apt:
        update_cache: true
        cache_valid_time: 3600
      when: ansible_os_family == "Debian"

    - name: Install Chrony
      package:
        name: "{{chrony_package_name}}"

    - name: Start Chrony
      service:
        name: "{{chrony_service_name}}"
        state: started
        enabled: true

    - name: Install custom conf
      template:
        dest: "{{chrony_config_directory}}"
        mode: 0644
        src: chrony-conf.j2
      notify : Reload Chrony

  handlers:

    - name: Reload Chrony
      service:
        name: "{{chrony_service_name}}"
        state: restarted

...
```

templates/chrony-conf.j2
```
{# templates/chrony-conf.j2 #}
# {{chrony_config_directory}}
server 0.fr.pool.ntp.org iburst
server 1.fr.pool.ntp.org iburst
server 2.fr.pool.ntp.org iburst
server 3.fr.pool.ntp.org iburst
driftfile /var/lib/chrony/drift
makestep 1.0 3
rtcsync
logdir /var/log/chrony

```

vars/chrony_debian.yml
```
---  # vars/chrony_debian.yml

chrony_package_name: chrony
chrony_service_name: chrony
chrony_config_directory: /etc/chrony/chrony.conf

...
```

chrony_rocky.yml
```
---  # vars/chrony_rocky.yml

chrony_package_name: chrony
chrony_service_name: chronyd
chrony_config_directory: /etc/chrony.conf

...
```

chrony_ubuntu.yml
```
---  # vars/chrony_ubuntu.yml

chrony_package_name: chrony
chrony_service_name: chrony
chrony_config_directory: /etc/chrony/chrony.conf

...
```

chrony_opensuse-leap.yml
```
---  # vars/chrony_opensuse-leap.yml

chrony_package_name: chrony
chrony_service_name: chronyd
chrony_config_directory: /etc/chrony.conf

...

```
