Ansible role: Firefox
=====================

Installs Firefox_ and optionally creates profiles with extensions.
Extensions are installed but need to be manually enabled from Firefox.

Requirements
------------

requests_ is required on the remote host to install extensions.


Role Variables
--------------

Default directory for profiles
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: yaml

    firefox_home: ~/.mozilla/firefox


Profile settings
~~~~~~~~~~~~~~~~

The **firefox_profiles** is object with profile names als fields. For each profile, a list of extension names can be specified under the field **extensions**. These extensions will be installed for that profiles. Secondly, a list of preference key-value pairs can be specified under the field **preferences**. These are also profile-specific and will be put or modified in the **user.js** file of the profile.


Example Playbook
----------------

.. code:: yaml

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


License
-------

GPLv2


Author Information
------------------

`staticdev`_


Credits
-------

This Ansible role is a modified version of the `ansible-firefox`_ originally created by GitHub user `unrblt`_ and modified by `basvandenbrink`_.


.. _Firefox: https://www.mozilla.org/firefox/
.. _ansible-firefox: https://github.com/basvandenbrink/ansible-firefox
.. _basvandenbrink: https://github.com/basvandenbrink
.. _requests: https://docs.python-requests.org/en/master
.. _staticdev: https://github.com/staticdev
.. _unrblt: https://github.com/unrblt
