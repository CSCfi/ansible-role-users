[![Build Status](https://travis-ci.org/CSCfi/ansible-role-users.svg)](https://travis-ci.org/CSCfi/ansible-role-users)
[![Galaxy Role](https://img.shields.io/badge/ansible--galaxy-ansible--role--users-blue)](https://galaxy.ansible.com/CSCfi/ansible-role-users)
# ansible-role-users
Ansible Role to add local unix users

# Calling the role

When you call the role, you may set gather_facts to false.

<pre>
- name: Configure users
  hosts: admin_hosts
  gather_facts: false
  roles:
     - ansible-role-users
</pre>

# Role Variables

More examples can be found in tests/test.yml:
<pre>
admingroup: "admin"
adminshell: "/bin/bash"
adminusers:
 - {name: admin1, state: 'present', uid: 5001, group: "{{admingroup}}", shell: "{{adminshell}}", pubkey: "ssh-rsa KEY admin1@example.com" }
adminremove_passwords: false
 - {name: badadmin2, state: 'absent', uid: 5001, group: "{{admingroup}}", shell: "{{adminshell}}", pubkey: "ssh-rsa KEY badadmin2@example.com" }
 - {name: rsyncuser1, state: 'present', uid: 5003, group: "{{admingroup}}", shell: "{{adminshell}}", pubkey: "ssh-rsa KEY rsync1@example.com", options: 'command="/usr/local/bin/rrsync /allow/rrsync/here/directory",no-agent-forwarding,no-port-forwarding,no-pty,no-user-rc,no-X11-forwarding' }
</pre>

 - adminremove_passwords: True
  - this will set passwords on the users to "\*"
 - admin_sudoers: True
  - this will add the admingroup to sudoers

# multiple ssh keys to a single user

Can be done with this trick:
<pre>
newline: "\n"

  - { name: multisshkeyuser, uid: 5004, group: "{{admingroup}}", groups: "agroup,bgroup", state: "present", shell: "{{adminshell}}", pubkey: "ssh-rsa KEY1 {{ newline }} ssh-rsa KEY2 {{ newline }} ssh-rsa KEY3" }

</pre>

# Caveats

Modifying a logged in user's UID does not work. Don't do it. The role anticipates this and only modifies group and groups for those users.

# License

MIT

# Contributors

 - https://github.com/martbhell
 - https://github.com/peterjenkins1
 - https://github.com/khappone
