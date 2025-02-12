# Exercice

apache-debian.yml 
```
---  # apache-debian.yml

- hosts: debian

  tasks:

    - name: Update package information
      apt:
        update_cache: true
        cache_valid_time: 3600

    - name: Install Apache
      apt:
        name: apache2

    - name: Install custom web page
      copy:
        dest: /var/www/html/index.html
        mode: 0644
        content: |
          <!doctype html>
          <html>
            <head>
              <meta charset="utf-8">
              <title>Serveur Apache</title>
            </head>
            <body>
              <h1>PLaybook 01 debian</h1>
            </body>
          </html>
```

apache-rocky.yml
```
---  # apache-rocky.yml

- hosts: rocky

  tasks:

    - name: Install Apache
      dnf:
        name: httpd, php

    - name: Start & enable Apache
      service:
        name: httpd
        state: started
        enabled: true

    - name: Install custom web page
      copy:
        dest: /var/www/html/index.html
        mode: 0644
        content: |
          <!doctype html>
          <html>
            <head>
              <meta charset="utf-8">
              <title>Serveur Apache</title>
            </head>
            <body>
              <h1>Serveur 01 Rocky</h1>
            </body>
          </html>                 
```

apache-suse.yml
```
---  # apache-suse.yml

- hosts: suse

  tasks:

    - name: Install Apache
      zypper:
        name: apache2

    - name: Start & enable Apache
      service:
        name: apache2
        state: started
        enabled: true

    - name: Install custom web page
      copy:
        dest: /srv/www/htdocs/index.html
        mode: 0644
        content: |
          <!doctype html>
          <html>
            <head>
              <meta charset="utf-8">
              <title>Serveur Apache</title>
            </head>
            <body>
              <h1>Serveur 01 Suse</h1>
            </body>
          </html>
```
