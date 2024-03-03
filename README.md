Role Name
=========

An Ansible role to install [rss-lemmy-bot](https://github.com/kensand/rss-lemmy-bot) 
as a containered service using Podman and managed by systemd.

Requirements
------------

Podman 4.4 or later is required to be installed. Currently this role doesn't install it or check for it. 

That's the version that adds support for ".container" files used here.

Role Variables
--------------

See [./defaults/main.yml](./defaults/main.yml) for the variables and their docs.

You can choose your version of the Docker image to use and set all the variables that would go
in the rss-lemmy-bot config.json.

Dependencies
------------

You could use another role to Podman.

Example Playbook
----------------

    - hosts: my-server
      become: true
      vars:
        some_vars_go_here: true
      tasks:
        - name: Include rss-to-lemmy-bot role
          tags: lemmy
          include_role:
             name: markstosberg.rss-lemmy-bot
             apply:
               tags: lemmy

Security
-------

The bot will run with UID 1000 within the container, not root.

Service Management and Logging
------------------------------

The role will create a systemd service named `rss-lemmy-bot` which will set to start at boot.
Normal systemd commands can be used to manage the service and review the logs:

    systemctl stop rss-lemmy-bot
    systemctl start rss-lemmy-bot
    systemctl status rss-lemmy-bot
    journalctl -u rss-lemmy-bot

The service will produce logging each time it starts and finishes scanning feeds like the following.

> Mar 03 13:47:13 host rss-lemmy-bot[18636]: Scanning feed https://example.com/feed/. Latest Item in feed is Sun Mar 03 2024 03:17:11 GMT+0000 (Coordinated Universal Time).
> Mar 03 13:47:13 host rss-lemmy-bot[18636]: Finished scanning https://example.com/feed/. Posted 0 items. Latest item in feed is from Sun Mar 03 2024 03:17:11 GMT+0000 (Coordinated Universal Time).

License
-------

BSD

Author Information
------------------

- [Mark Stosberg](https://mark.stosberg.com/)
