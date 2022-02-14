set_root_password
=========

Set the root password (including SALT to make this idempotent)

Requirements
------------

None.

Role Variables
--------------

- `root_password`: the desired root password, if not set this will use the `ansible_become_password` variable
- `salt_for_root_password`: a SALT used for ...ahem... salting the root password
- `password_hash_mechanism`: password hashing mechanism, defaults to `sha512`

You can generate the salt with e.g. `openssl rand -base64 16 | tr -d += | head -c 16; echo ""` or similar. If you do not set this, then the task will be shown as changed each time, even though the password stays the same. But the salt is changed each time...

Dependencies
------------

None

Example Playbook
----------------

    - hosts: servers
      roles:
        - role: 'johanneskastl.set_root_password'
          vars:
            root_password: 'supersecret password that should be encrypted in ansible-vault and not in a playbook in cleartext'
            salt_for_root_password: 'bBzjzIL1qyk6taGc'

License
-------

BSD-3-Clause

Author Information
------------------

I am Johannes Kastl, reachable via kastl@b1-systems.de.
