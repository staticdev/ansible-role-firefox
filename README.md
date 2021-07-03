# Ansible Role: Firefox

Installs Firefox and optionally creates profiles with extensions.
Extensions are installed but need to be manually enabled from Firefox.

## Requirements

[requests][0] is required on the remote host to install extensions.

## Role Variables

### Default directory for profiles

```yaml
firefox_home: ~/.mozilla/firefox
```

### Profile settings

The `firefox_profiles` is object with profile names als fields. For each profile, a list of extension names can be specified under the field `extensions`. These extensions will be installed for that profiles. Secondly, a list of preference key-value pairs can be specified under the field `preferences`. These are also profile-specific and will be put or modified in the `user.js` file of the profile.

## Example Playbook

```yaml
- hosts: localhost

  vars:
    firefox_profiles:
      default:
        extensions:
          - ublock-origin
        preferences:
          privacy.donottrackheader.enabled: "true"
          privacy.trackingprotection.enabled: "true"
          signon.rememberSignons: "false"
          datareporting.healthreport.uploadEnabled: "false"
      bob:
        extensions:
          - adblock-plus
        preferences:
          privacy.donottrackheader.enabled: "false"
          privacy.trackingprotection.enabled: "false"
          signon.rememberSignons: "false"
          datareporting.healthreport.uploadEnabled: "false"

  roles:
    - basvandenbrink.firefox
```

## Credits

This Ansible role is a modified version of the [Ansible role](https://github.com/basvandenbrink/ansible-firefox) originally created by GitHub user [unrblt](https://github.com/unrblt) and modified by [basvandenbrink](https://github.com/basvandenbrink).

## License

GPLv2

[0]: http://docs.python-requests.org/en/master "requests"
