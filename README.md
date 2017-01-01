# ansible-gitea

## Synopsis

```yml
- hosts: all
  vars:
    gitea_database_name: gitea
    gitea_database_user: gitea
    gitea_database_password: "{{ vault_crypted_gitea_database_pass }}"
    gitea_salt: "{{ vault_crypted_gitea_salt }}"
    gitea_domain: git.example.com
    gitea_database_uri: mysql.example.com:3306
  roles:
    - alvaroaleman.gitea
```

## Description

Simple role to install the Gogs git server.

## Requirements

* [silpion.lib](https://github.com/silpion/ansible-lib.git)

## Role Variables

* ``gitea_domain``: The baseurl for linkgeneration  ``mandatory``
* ``gitea_database_bassword``: Database password for gitea ``mandatory``
* ``gitea_salt``: The salt to use for password storage ``mandatory``
* ``gitea_database_uri``: Uri to use for database connection (default: ``localhost:3306``)
* ``gitea_database_name``: Name of the database gitea shall use (default: ``gitea``)
* ``gitea_database_user``: Name of the database usre gitea shall use (default: ``gitea``)
* ``gitea_database_type``: Type of gitea database (default: ``mysql``)
* ``gitea_http_port``: Http port gitea shall bind to (default: ``3000``)
* ``gitea_ssh_port``: SSH port gitea shall bind to (default: ``2222``)
* ``gitea_http_proto``: Whether to prepend ``http`` or ``https`` to generated links (default: ``http``)
* ``gitea_logdir``: The directory to write logs into (default: ``/var/run/gitea``)
* ``gitea_appini_template``: Template to use fot gitea ``app.ini`` config file (default: ``builtin_app.ini.j2``)
* ``gitea_home``: Folder in which to put gitea data (default: ``/srv/gitea``)
* ``gitea_username``: Username under which to run gitea. Must be root if you want gitea to bind to ports < 1024 (default: ``gitea``)
* ``gitea_install_dir``: Folder to install gitea into (default: ``/opts/gitea``)
* ``gitea_config_dir``: Folder in which to put gitea config (default: ``/etc/gitea``)
* ``gitea_version``: The version of gitea to install (default: ``0.9.113``)
* ``gitea_http_listen_addr``: The address to listen on for http request (default: '')


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
