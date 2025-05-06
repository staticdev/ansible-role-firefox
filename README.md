# Ansible role: Firefox

[![Tests](https://github.com/staticdev/ansible-role-firefox/workflows/Tests/badge.svg)][tests]

[tests]: https://github.com/staticdev/ansible-role-firefox/actions?workflow=Tests

**DEPRECATED: this project is not maintained anymore in favor direct installation with [nix package manager](https://nixos.wiki/wiki/Nix_package_manager) and [Nixpkgs](https://github.com/NixOS/nixpkgs).**

Installs [Firefox] from official PPA repository and optionally creates profiles with extensions.
Extensions are installed but need to be manually enabled from Firefox.

Note: on Debian it will remove the ESR version in favor to PPA more up-to-date releases.

## Requirements

[requests] is required on the remote host to install extensions.
The OS of the remote host is supported, see [ansible-galaxy staticdev/firefox].

## Role Variables

### Default directory for profiles

```yaml
firefox_home: ~/.mozilla/firefox
```

### Profile settings

The **firefox_profiles** is object with profile names als fields. For each profile, a list of extension names can be specified under the field **extensions**. These extensions will be installed for that profiles. Secondly, a list of preference key-value pairs can be specified under the field **preferences**. These are also profile-specific and will be put or modified in the **user.js** file of the profile.

## Example Playbook

```yaml
- hosts: localhost

  vars:
    firefox_profiles:
      default:
        extensions:
          - ublock-origin
        preferences:
          network.cookie.cookieBehavior: 1
          privacy.donottrackheader.enabled: true
          datareporting.healthreport.uploadEnabled: false
      secondprofile:
        extensions:
          - adblock-plus
        preferences:
          privacy.donottrackheader.enabled: false
          privacy.trackingprotection.enabled: false
          signon.rememberSignons: false
          datareporting.healthreport.uploadEnabled: false

  roles:
    - staticdev.firefox
```

## License

MIT

## Author Information

[staticdev]

## Credits

This Ansible role is a modified version of the [ansible-firefox] originally created by GitHub user [unrblt] and modified by [basvandenbrink].

[ansible-firefox]: https://github.com/basvandenbrink/ansible-firefox
[ansible-galaxy staticdev/firefox]: https://galaxy.ansible.com/staticdev/firefox
[basvandenbrink]: https://github.com/basvandenbrink
[firefox]: https://www.mozilla.org/firefox/
[requests]: https://docs.python-requests.org/en/master
[staticdev]: https://github.com/staticdev
[unrblt]: https://github.com/unrblt
