ansible-role-netatalk
=========

Ansible role to install and configure [Netatalk](http://netatalk.sourceforge.net), an [Apple Filling Protocol](https://en.wikipedia.org/wiki/Apple_Filing_Protocol) (AFP), server. This allows Linux folders to be shared natively to Mac OSX machines.

Combined with [Avahi](https://github.com/brianhartsock/ansible-role-avahi) a Linux server can appear as a native Apple fileserver to Mac OSX machines on the same network.

Requirements
------------

This role has been tested on Ubuntu 16.04 and should work on most modern Debian installations.

The role will need `sudo` privileges so it should be run with `become: True` or a user with sufficient default privileges to install and configure packages.

Role Variables
--------------

The following variables are defined in `defaults/main.yml` and can be used to further configure Netatalk shares. `netatalk_shares` is the most important variable which defines which services are advertised over mDNS.

```yaml
netatalk_shares:
  - /srv/TimeMachine TimeMachine allow:user1,user2 volsizelimit:1048576 cnidscheme:dbd options:tm"
  - /srv/media Media allow:user1,user2 cnidscheme:dbd"
netatalk_afpd_options: '- -tcp -noddp -uamlist uams_randnum.so,uams_dhx.so,uams_dhx2.so -nosavepassword'
```

See [afpd.conf](templates/afpd.conf.j2) and [AppleVolumes.default](templates/AppleVolumes.default.j2) for more detailed documentation on configuring shares and afpd options.

Dependencies
------------

None, however [Avahi](https://github.com/brianhartsock/ansible-role-avahi) is highly recommended.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - name: brianhartsock.netatalk
           become: true

License
-------

MIT

Author Information
------------------

Created with love by [Brian Hartsock](http://blog.brianhartsock.com).
