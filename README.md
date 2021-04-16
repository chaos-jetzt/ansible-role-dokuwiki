ansible-role-dokuwiki
=========

This role installs and configures [splitbrain](https://github.com/splitbrain/)s [Dokuwiki](https://dokuwiki.org) on your hosts. It's a sucessor to [PeterMosmans](https://github.com/PeterMosmans) work at [ansible-role-dokuwiki](https://github.com/PeterMosmans/ansible-role-dokuwiki). But since this role doesn't fit perfectly with our setup and the new "hogfather" Dokuwiki version, we settled to recreate it.


Requirements
------------

You need to have PHP installed on your system. While it is not required for the installation, to run dokuwiki a webserver such as nginx or apache2 is also required.

Role Variables
--------------

TODO

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Example Playbook
----------------

<!--Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:-->

Note: When you want to define multi-dimensional configuration parameters in `dokuwiki_additonal_configuration` you can concatenate the levels using `>` in the name as a separator. So `auth>mysql>server` would become `$conf['auth']['mysql']['server']`.

Further more, all strings inside the `dokuwiki_additonal_configuration` list must be wrapped in two quotation marks like so: `"'my string'"`. The double quotation marks tell ansible that the value is a string and so the single quotation marks will be a normal part of the string and placed as a string in the `local.php`. See [#3](https://github.com/chaos-jetzt/ansible-role-dokuwiki/pull/3#issuecomment-719563190) for another explanation why it's done that way.

```yaml
---
- hosts: dokuwiki
  roles:
    - chaos-jetzt.dokuwiki
  vars:
    dokuwiki_basedir: /var/www/dokuwiki
    dokuwiki_template: bootstrap3
    dokuwiki_authtype: mysql
    dokuwiki_user: www-data
    dokuwiki_plugins:
      - name: popularity
        state: absent
      - name: move
        state: enabled
      - name: "template:bootstrap3"
        state: enabled
    dokuwiki_addional_acronyms:
      - short: CCC
        long: Chaos Computer Club e.V.
    dokuwiki_addional_entities:
      - from: mü
        to: µ
        state: present
    dokuwiki_additional_schemes:
        - xmpp
        - scheme: gopher
          state: absent
    dokuwiki_additional_interwikis:
        - code: ddg
          url: https://duckduckgo.com/?q={NAME
    dokuwiki_additional_smileys:
        - code: ":dwiki:"
          image: dwiki.png
          source: "https://www.dokuwiki.org/lib/tpl/dokuwiki/images/logo.png"
    dokuwiki_additonal_configuration:
      - name: 'auth>mysql>server'
        value: "'localhost'"
      - name: 'auth>mysql>user'
        value: "'dbuser'"
      - name: 'auth>mysql>password'
        value: "'localhost'"
      - name: 'auth>mysql>database'
        value: "'localhost'"
```

License
-------

This work is licensed under the permissive BSD 3-Clause license. See the [LICENSE](LICENSE) for a full copy of the license text.

Author Information
------------------

This role is inspired by [PeterMosmans](https://github.com/PeterMosmans) work at [ansible-role-dokuwiki](https://github.com/PeterMosmans/ansible-role-dokuwiki), but since we felt it didn't meed our demands especialy with some new dokuwiki features (CLI to manage Plugins) we decided to write our own role.

The Initial code is from [e1mo](https://github.com/e1mo/) for the [chaos.jetzt](https://chaos.jetzt) project.
