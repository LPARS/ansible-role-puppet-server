# Ansible Role: Puppet Server

[![CI](https://github.com/LPARS/ansible-role-puppet-server/actions/workflows/ci.yml/badge.svg)](https://github.com/LPARS/ansible-role-puppet-server/actions/workflows/ci.yml)

An Ansible role that installs [Puppet](https://www.puppet.com) or [OpenVox](https://voxpupuli.org/openvox/) server on Linux.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    puppet_version: "7"

The major version of Puppet/OpenVox to be installed.

    r10k_package: "r10k"

The r10k package to use. Choices include r10k and g10k. NOTE: Only used for Debian-based OSes.

    git_server: ""
    git_user: ""
    git_repo: ""

The Git server, user/organization, and repository that will be used by r10k to clone the repository.

    puppet_server_service_state: "started"
    puppet_server_service_enabled: true
    puppet_server_service_manage: false

The service that should be run on this server. By default, this role will not manage the Puppet/OpenVox server service.

    r10k_ssh_key_path: "/root/.ssh"
    r10k_ssh_private_key: ""
    r10k_ssh_public_key: ""

The directory where r10k's SSH keys will be copied, and the literal string contents of the keys. Always use Ansible Vault to encrypt the private key.
Providing the public key is optional but recommended for easier identification.

## Dependencies

This role is designed to be used with [ansible-role-puppet-agent](https://github.com/LPARS/ansible-role-puppet-agent).
To ensure that server and agent versions match, this role shares overlapping variables such as `puppet_version` and `puppet_release` (deb/rpm).
To install ansible-role-puppet-agent, use the included `requirements.yml`.

## Example Playbook

    - name: Install and configure Puppet/OpenVox server
      hosts: all
      become: true
      roles:
        - lpars.puppet_server
        - lpars.puppet_agent

## License

MIT

## Acknowledgments

This Ansible role was inspired by Jeff Geerling's https://github.com/geerlingguy/ansible-role-puppet. A huge thanks to him for helping me learn Ansible.
