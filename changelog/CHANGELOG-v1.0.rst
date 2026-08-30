====================================
vbotka.ansible-ucl 1.0 Release Notes
====================================

.. contents:: Topics


1.1.6
=====

Release Summary
---------------

Major Changes
-------------

Minor Changes
-------------

* Command Injection & Execution Safety (list args over shell strings):

  - Replaced fragile shell-string formatting (f"{uclcmd} set ... {value}") with
    tokenized Python lists ([uclcmd, "set", ...]).

  - If a value or upath contains spaces, quotes, or special characters,
    shell-string interpolation previously risked broken commands or shell
    escapes. Passing list arguments to module.run_command executes the binary
    safely without a subshell.

* Eliminated Risky Mutable Globals:

  - Encapsulated mutable run state into an explicit ExecutionState dataclass
    passed cleanly between functions.

* Structured UCL Value Serialization (_format_value):

  - Boolean, numeric, and dictionary/list values passed to value are properly
    converted to UCL-compatible string literals or JSON-encoded strings before
    invoking uclcmd.

* Improved Temporary File Management:

  - Used tempfile.NamedTemporaryFile within safe handlers and ensured temporary
    files are cleaned up reliably on failure.

* Ansible Documentation Standards:

  - Ensured all choices, types, and return values strictly adhere to Galaxy /
    ansible-test sanity schemas.

  - Removed deprecated global variables and unnecessary _debug internals in
    favor of Ansible standard return keys.


1.1.5
=====

Release Summary
---------------
Maintenance update.

Major Changes
-------------

Minor Changes
-------------
* Fix the deprecation warning: Importing 'to_bytes' from
  'ansible.module_utils._text' is deprecated.


1.1.4
=====

Release Summary
---------------
Maintenance update.

Major Changes
-------------

Minor Changes
-------------
* Updated documentation and docstrings.
* Remove encoding declaration.


1.1.3
=====

Release Summary
---------------
Fix docs.

Major Changes
-------------

Minor Changes
-------------
* Fix extends_documentation_fragment. Add backup.
* Fix extends_documentation_fragment FQDN.
* Remove documentation attributes.
* Update tests
* Remove stdout_callback from ansible.cfg.
  Add callback_result_format = yaml
* Link module to the directory library.
* Update README.


1.1.2
=====

Release Summary
---------------
Fix docs.

Major Changes
-------------

Minor Changes
-------------
* Fix docs description.
* Fix docs attributes lint.
* Fix docs examples YAML lint.


1.1.1
=====

Release Summary
---------------
Formatting replaced by f-strings.

Major Changes
-------------

Minor Changes
-------------
* Formatting replaced by f-strings.


1.1.0
=====

Release Summary
---------------
Maintenance update.

Major Changes
-------------

Minor Changes
-------------
* Add changelog
* Add SPDX-License-Identifier: BSD-2-Clause
* Update README
* Update examples, playbooks
* Update ansible-lint configuration
* Remove .ansible-lint

Bugfixes
--------

Breaking Changes / Porting Guide
--------------------------------
