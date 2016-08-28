# ansible-gogs

## Synopsis

```yml
- hosts: all
  vars:
    gogs_database_name: gogs
    gogs_database_user: gogs
    gogs_database_password: "{{ vault_crypted_gogs_database_pass }}"
    gogs_salt: "{{ vault_crypted_gogs_salt }}"
    gogs_domain: git.example.com
    gogs_database_uri: mysql.example.com:3306
  roles:
    - alvaroaleman.gogs
```

## Description

Simple role to install the Gogs git server.

## Requirements

* [silpion.lib](https://github.com/silpion/ansible-lib.git)

## Role Variables

* ``gogs_domain``: The baseurl for linkgeneration  ``mandatory``
* ``gogs_database_bassword``: Database password for gogs ``mandatory``
* ``gogs_salt``: The salt to use for password storage ``mandatory``
* ``gogs_database_uri``: Uri to use for database connection (default: ``localhost:3306``)
* ``gogs_database_name``: Name of the database gogs shall use (default: ``gogs``)
* ``gogs_database_user``: Name of the database usre gogs shall use (default: ``gogs``)
* ``gogs_database_type``: Type of gogs database (default: ``mysql``)
* ``gogs_http_port``: Http port gogs shall bind to (default: ``3000``)
* ``gogs_ssh_port``: SSH port gogs shall bind to (default: ``2222``)
* ``gogs_http_proto``: Whether to prepend ``http`` or ``https`` to generated links (default: ``http``)
* ``gogs_logdir``: The directory to write logs into (default: ``/var/run/gogs``)
* ``gogs_appini_template``: Template to use fot gogs ``app.ini`` config file (default: ``builtin_app.ini.j2``)
* ``gogs_home``: Folder in which to put gogs data (default: ``/srv/gogs``)
* ``gogs_username``: Username under which to run gogs. Must be root if you want gogs to bind to ports < 1024 (default: ``gogs``)
* ``gogs_install_dir``: Folder to install gogs into (default: ``/opts/gogs``)
* ``gogs_config_dir``: Folder in which to put gogs config (default: ``/etc/gogs``)
* ``gogs_version``: The version of gogs to install (default: ``0.9.71``)


## Contributing

If you want to contribute to this repository please be aware that this
project uses a [gitflow](http://nvie.com/posts/a-successful-git-branching-model/)
workflow with the next release branch called ``next``.

Please fork this repository and create a local branch split off of the ``next``
branch and create pull requests back to the origin ``next`` branch.

## License

AGPLv3

## Integration testing

This role provides integration tests using the Ruby RSpec/serverspec framework
with a few drawbacks at the time of writing this documentation.

Running integration tests requires a number of dependencies being
installed. As this role uses Ruby RSpec there is the need to have
Ruby with rake and bundler available.

```shell
# install role specific dependencies with bundler
bundle install
```

<!-- -->

```shell
# run the complete test suite with Docker
rake suite
```

<!-- -->

```shell
# run the complete test suite with Vagrant
source  envvars-vagrant.sample
rake suite

# run the complete test suite with Vagrant without destroying the box afterwards
source  envvars-vagrant.sample
RAKE_ANSIBLE_VAGRANT_DONT_CLEANUP=1 rake suite
```


## Author information

* Alvaro Aleman

<!-- vim: set nofen ts=4 sw=4 et: -->
