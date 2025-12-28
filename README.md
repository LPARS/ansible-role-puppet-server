# Ansible Role: Puppet Server

[![CI](https://github.com/LPARS/ansible-role-puppet-server/actions/workflows/ci.yml/badge.svg)](https://github.com/LPARS/ansible-role-puppet-server/actions/workflows/ci.yml)

An Ansible role that installs [Puppet](https://www.puppet.com) or [OpenVox](https://voxpupuli.org/openvox/) server on Linux.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    puppet_version: "7"

The major version of Puppet/OpenVox to be installed.

    puppet_server_package: "puppetserver"

The package to be installed.

    puppet_server_service: "puppetserver"
    puppet_server_service_state: "started"
    puppet_server_service_enabled: true
    puppet_server_service_manage: false

The service that should be run on this server. By default, this role will not manage the Puppet/OpenVox server service.

    puppet_release_deb: "https://apt.puppetlabs.com/puppet{{ puppet_version }}-release-{{ ansible_facts['distribution_release'] }}.deb"

The .deb file for installation on Debian-based OSes.

    puppet_release_rpm: "https://yum.puppetlabs.com/puppet{{ puppet_version }}-release-el-{{ ansible_facts['distribution_major_version'] }}.noarch.rpm"

The .rpm file for installation on RedHat-based OSes.

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
