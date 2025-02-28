# Exercice

chrony-01.yml
```
---  # chrony-01.yml

- hosts: all

  tasks:

    - name: Install Chrony Rocky
      dnf:
        name: chrony
      when: ansible_distribution == "Rocky"

    - name: Install Chrony Ubuntu + Debian
      apt:
        name: chrony
      when: ansible_os_family in "Debian"

    - name: Install Chrony Suse
      zypper:
        name: chrony
      when: ansible_distribution == "openSUSE Leap"


    - name: Start & enable Chrony
      service:
        name: chronyd
        state: started
        enabled: true

    - name: Chrony conf
      copy:
        dest: /etc/chrony.conf
        mode: 0644
        content: |
          # /etc/chrony.conf
          server 0.fr.pool.ntp.org iburst
          server 1.fr.pool.ntp.org iburst
          server 2.fr.pool.ntp.org iburst
          server 3.fr.pool.ntp.org iburst
          driftfile /var/lib/chrony/drift
          makestep 1.0 3
          rtcsync
          logdir /var/log/chrony
      notify: Restart chrony

  handlers:

    - name: Restart chrony
      service:
        name: chronyd
        state: restarted
...

```

chrony-02.yml
```
---  # chrony-02.yml

- hosts: all

  vars:

    chrony:
      Debian:
        chrony_package: apt
        chrony_service: chrony
        chrony_confdir: /etc/chrony/chrony.conf
      Ubuntu:
        chrony_package: apt
        chrony_service: chrony
        chrony_confdir: /etc/chrony/chrony.conf
      Rocky:
        chrony_package: dnf
        chrony_service: chronyd
        chrony_confdir: /etc/chrony.conf
      openSUSE Leap:
        chrony_package: zypper
        chrony_service: chronyd
        chrony_confdir: /etc/chrony.conf

  tasks:

    - name: Install Chrony
      package:
        name: "{{chrony[ansible_distribution].chrony_package}}"

    - name: Start & enable Chrony
      service:
        name: "{{chrony[ansible_distribution].chrony_service}}"
        state: started
        enabled: true

    - name: Chrony conf
      copy:
        dest: "{{chrony[ansible_distribution].chrony_confdir}}"
        mode: 0644
        content: |
          # /etc/chrony.conf
          server 0.fr.pool.ntp.org iburst
          server 1.fr.pool.ntp.org iburst
          server 2.fr.pool.ntp.org iburst
          server 3.fr.pool.ntp.org iburst
          driftfile /var/lib/chrony/drift
          makestep 1.0 3
          rtcsync
          logdir /var/log/chrony
      notify: Restart chrony

  handlers:

    - name: Restart chrony
      service:
        name: chronyd
        state: restarted

...

```
