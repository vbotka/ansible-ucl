# ansible-ucl

[![license](https://img.shields.io/badge/license-BSD-red.svg)](https://www.freebsd.org/doc/en/articles/bsdl-gpl/article.html)
[![GitHub tag](https://img.shields.io/github/v/tag/vbotka/ansible-ucl)](https://github.com/vbotka/ansible-ucl/tags)

[uclcmd](https://github.com/allanjude/uclcmd) module for Ansible.


## Description

This module is an Ansible 'wrapper' of the *uclcmd* command. Most of the
uclcmd's options was implemented except of

* --noquotes
* --nonewline
* --keys
* --expand

The module is idempotent and supports both check_mode and debug.


## Install

Put the module to DEFAULT_MODULE_PATH

```sh
shell> ansible-config dump|grep DEFAULT_MODULE_PATH
DEFAULT_MODULE_PATH(default) = ['/home/admin/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
```


## Documentation

Only the inline documentation of the module is available. Run the command

```sh
shell> ansible-doc -t module ucl
```


## Example

The option *path* is required. Without other options the module returns the
content of the file in
[UCL](https://wiki.freebsd.org/UniversalConfigurationLanguage)
format. For example, the play below

```yaml
shell> cat playbook.yml
- hosts: srv.example.net
  tasks:
    - ucl:
        path: /etc/pkg/FreeBSD.conf
      register: result
    - debug:
        var: result
```

gives

```yaml
shell> ansible-playbook ucl.yml
  ...
  result:
    changed: false
    cmd: /usr/local/bin/uclcmd get --ucl --delimiter . --file /etc/pkg/FreeBSD.conf .
    failed: false
    msg: 'File: /etc/pkg/FreeBSD.conf; uclcmd: /usr/local/bin/uclcmd; Command get executed.'
    rc: 0
    stderr: ''
    stderr_lines: []
    stdout: |-
      freebsd {
          url = "pkg+http://pkg.FreeBSD.org/${ABI}/quarterly";
          mirror_type = "srv";
          signature_type = "fingerprints";
          fingerprints = "/usr/share/keys/pkg";
          enabled = true;
      }
```

See included playbooks, tasks and tests.


## Test

This module is tested with selected set of the
[uclcmd tests](https://github.com/allanjude/uclcmd/tree/master/tests).
Download these tests and create both local and remote directories ``tests``
including
[Ansible tests](https://github.com/vbotka/ansible-ucl/tree/master/tests.ansible)

```sh
shell> ansible-playbook run-tests.yml -e test_ucl=test_ucl \
                                      -e download_tests=true \
									  - debug=true
```

When the directories ``test`` are created run the play

```sh
shell> ansible-playbook tests-ucl.yml -e test_ucl=test_ucl \
                                      -e debug1=true \
									  -C
```

See NOTES to learn details.


## Requirements

* uclcmd >= 0.1_3

* libucl >= 0.8.1


## See also

* [FreeBSD Universal Configuration Language- Wiki](https://wiki.freebsd.org/UniversalConfigurationLanguage)
* [Source code devel/uclcmd - Command line tool for working with UCL config files](https://github.com/allanjude/uclcmd)
* [Source code libucl - UCL library](https://github.com/vstakhov/libucl/)
* [Source code libucl - Macros support](https://github.com/vstakhov/libucl/#macros-support)


## Author Information

[Vladimir Botka](https://botka.info)
