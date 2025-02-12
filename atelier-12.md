# Exercice

chrony.yml
```
---  # chrony.yml

- hosts: redhat

  tasks:

    - name: Install Chrony
      dnf:
        name: chrony

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

Sur une dizaine d'execution du playbook, le résultat reste toujours identique, mais avec une variation d'environ 1 secondes en fonction des executions.  
Je n'ai pas d'idée particuliere sur comment ameliorer l'idempotence du playbook.
