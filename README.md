# ansible-role-users
Ansible Role to add local unix users

# Role Variables

<pre>
admingroup: "admin"
adminshell: "/bin/bash"
adminusers:
 - {name: admin1, state: 'present', uid: 5001, groups: "{{admingroup}}", shell: "{{adminshell}}", pubkey: "ssh-rsa KEY admin1@example.com" }
adminremove_passwords: false
</pre>

 - adminremove_passwords: True
  - this will set passwords on the users to "*"

# License

MIT

# Contributors

 - https://github.com/martbhell
 - https://github.com/peterjenkins1
