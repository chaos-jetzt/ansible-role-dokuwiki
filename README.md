ansible-role-dokuwiki
=========

This role installs and configures Dokuwiki the host you specify. It relies heavily on [PeterMosmans](https://github.com/PeterMosmans) work at [ansible-role-dokuwiki](https://github.com/PeterMosmans/ansible-role-dokuwiki) and tries to be as compatible as possible. But since this doesn't fit perfectly with our setup and the new "hogfather" Dokuwiki version, we settled to recreate it.

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

Node: When you want to define multi-dimensional configuration parameters in `dokuwiki_additonal_configuration` you can concatenate the levels using `>` in the name as a seperator. So `auth>mysql>server` would become `$conf['auth']['mysql']['server']`.

```yaml
---
- hosts: dokuwiki
	roles:
    - chaos-jetzt.dokuwiki
	vars:
		dokuwiki_basedir: /var/www/dokuwiki
		dokuwiki_authtype: mysql
		dokuwiki_user: www-data
		dokuwiki_plugins:
			- name: popularity
				state: absent
			- name: move
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
				value: localhost
			- name: 'auth>mysql>user'
				value: dbuser
			- name: 'auth>mysql>password'
				value: localhost
			- name: 'auth>mysql>database'
				value: localhost
```

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
