# Ansible role: Firefox

[![Tests](https://github.com/staticdev/ansible-role-firefox/workflows/Tests/badge.svg)][tests]

[tests]: https://github.com/staticdev/ansible-role-firefox/actions?workflow=Tests

Installs [Firefox] and optionally creates profiles with extensions.
Extensions are installed but need to be manually enabled from Firefox.

## Requirements

[requests] is required on the remote host to install extensions.

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

GPLv2

## Author Information

[staticdev]

## Credits

This Ansible role is a modified version of the [ansible-firefox] originally created by GitHub user [unrblt] and modified by [basvandenbrink].

[ansible-firefox]: https://github.com/basvandenbrink/ansible-firefox
[basvandenbrink]: https://github.com/basvandenbrink
[firefox]: https://www.mozilla.org/firefox/
[requests]: https://docs.python-requests.org/en/master
[staticdev]: https://github.com/staticdev
[unrblt]: https://github.com/unrblt
