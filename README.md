Setup requirements
=========

```
  pyenv install 3.12.0
  pyenv virtualenv 3.12.0 ansible-env
  pyenv activate ansible-env
  pip install --upgrade pip
  pip install -r requirements.txt
```

New user setup
=========

Add new user, groups, specify authorized ssh keys, home directory.

Role Variables
--------------

You must specify the new user(s) details (name, pwd, authorized ssh key, groups).

```
  host_users:
    - name: ansible
      pwd: "changeMe"
      authorized_keys:
        - "ssh-ed25519 AAAA ansible"
      groups:
        - sudo
        - dev
      home: "/srv/www"
```

Example
----------------

```
  - hosts: webservers
    tasks:
      - name: "Include new user role"
        ansible.builtin.include_role:
          name: "jimtesson.new_user"
          vars:
            host_users:
              - name: ansible
                pwd: "changeMe"
                authorized_keys:
                  - "ssh-ed25519 AAAA ansible"
                groups:
                  - sudo
                  - dev
                home: "/srv/dev"

```
 
Tests
----------------

```
  # create the instance
  molecule create

  # apply the playbook
  molecule converge

  # test the playbook
  molecule verify

  # destroy the instance
  molecule destroy  
```

License
-------

BSD
