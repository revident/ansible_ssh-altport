# Goals of this playbook
  
To harden direct internet facing hosts.

1. Define and enable an alternate port for ssh in Firewalld.
2. Inform SELINUX that sshd can also listen on the alternate port.
3. Configure sshd to use it's traditional port and the new port.
4. Close off direct ssh login to root.
5. Disable traditional ssh port in Firewalld.

# Ansible + SSH

## First Run

**Make Sure you have a sudo capable account on the system before using this playbook!**

See the [ansible_onbaord](https://github.com/revident/ansible_onboard) repo for an example on how to set up such an account.

The very first run of the playbook can be done with root, or any user that has sudo privileges.

```
ansible-playbook ssh-altport.yml -u svcuser -k -K
```

## Later Runs

As the host is now only reachable on the alternate port, update your ~/.ssh/config to use the new port be default.

```
Host host1.example.com
  Port 22869
```

And connect using your pre established unprivileged user with sudo privileges.

```
ansible-playbook ssh-altport.yml -u svcuser -k -K
```

# Supported Systems

This Playbook was tested against CentOS 7.4 and Fedora 26 + 27, and should work with newer releases.

# Customize this Playbook

All the variables that define the alternate port are defined in:
```
/roles/ssh-altport/vars/main.yml
```
Please change those to something suitable for your environment.

