# ansible-gogs

## Synopsis

Synopsis...

## Description

Description...

## Requirements

Requirements...

## Role Variables

* ``variable_name``: Variable description (<!variable type>, default: ``variable default value``)

### complex_variable_name

Complex variable documentation...

### another_complex_variable_name

Complex variable documentation...

## Dependencies

Dependencies...

### Dependency variables

Dependency variables documentation...

## Example Playbook

```yaml
- hosts: all
  roles:
     - { role: ansible-gogs }
```

## Contributing

If you want to contribute to this repository please be aware that this
project uses a [gitflow](http://nvie.com/posts/a-successful-git-branching-model/)
workflow with the next release branch called ``next``.

Please fork this repository and create a local branch split off of the ``next``
branch and create pull requests back to the origin ``next`` branch.

## License

Apache Version 2.0

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

<!Author Name> @<!email_prefix> <!email_suffix>


<!-- vim: set nofen ts=4 sw=4 et: -->
