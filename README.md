[![Build Status](https://travis-ci.org/CSC-IT-Center-for-Science/ansible-role-users.svg)](https://travis-ci.org/CSC-IT-Center-for-Science/ansible-role-users)
# ansible-role-users
Ansible Role to add local unix users

# Calling the role

When you call the role, if your ansible version >= 2.1 it needs the "gather_subset: "!all" parameter. E.g.

<pre>
- name: Configure users
  hosts: admin_hosts
  gather_subset: "!all"
  roles:
     - ansible-role-users
</pre>

This gathers enough info to be usable by the role, but doesn't try to ssh in which might by definition fail.

# Role Variables

<pre>
admingroup: "admin"
adminshell: "/bin/bash"
adminusers:
 - {name: admin1, state: 'present', uid: 5001, groups: "{{admingroup}}", shell: "{{adminshell}}", pubkey: "ssh-rsa KEY admin1@example.com" }
adminremove_passwords: false
 - {name: badadmin2, state: 'absent', uid: 5001, groups: "{{admingroup}}", shell: "{{adminshell}}", pubkey: "ssh-rsa KEY badadmin2@example.com" }
 - {name: rsyncuser1, state: 'present', uid: 5003, groups: "{{admingroup}}", shell: "{{adminshell}}", pubkey: "ssh-rsa KEY rsync1@example.com", options: 'command="/usr/local/bin/rrsync /allow/rrsync/here/directory",no-agent-forwarding,no-port-forwarding,no-pty,no-user-rc,no-X11-forwarding' }
</pre>

 - adminremove_passwords: True
  - this will set passwords on the users to "\*"
 - admin_sudoers: True
  - this will not add the admingroup to sudoers

# multiple ssh keys to a single user

Can be done with this trick:
<pre>
newline: "\n"

  - { name: multisshkeyuser, uid: 5004, group: "{{admingroup}}", groups: "{{admingroup}}", state: "present", shell: "{{adminshell}}", pubkey: "ssh-rsa KEY1 {{ newline }} ssh-rsa KEY2 {{ newline }} ssh-rsa KEY3" }

</pre>

# License

MIT

# Contributors

 - https://github.com/martbhell
 - https://github.com/peterjenkins1
 - https://github.com/khappone
