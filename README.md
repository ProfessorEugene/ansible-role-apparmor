# Ansible Role: AppArmor

[![Build Status](https://travis-ci.org/TanmayaA/ansible-role-apparmor.svg?branch=master)](https://travis-ci.org/TanmayaA/ansible-role-apparmor)

Generates AppArmor profile for use with Docker containers.
Mostly an Ansible port of  https://github.com/jfrazelle/bane

## Requirements
* Ubuntu (trusty)
* AppArmor
* Docker (1.9)

## Role Variables

Variable | Description | Type | Default Value | Optional
---------|-------------|------| --------------|---------
profile_name| Container's AppArmor profile name | String |  None | No
read_only_paths|Paths with Read-only access | List of Strings| None | yes
log_writes_on_paths|Paths where any write access should be logged| List of Strings | None | yes
writable_paths|Paths with write access | List of Strings | None | yes
allow_execs|Allowed executable files | List of Strings | None | yes
deny_execs |  Denied executable files | List of Strings | None | yes
allow_caps|Allowed Linux capabilities | List of Strings | None | yes
deny_caps|Denied Linux capabilities | List of Strings | None | yes
network_raw | Raw packet access | Boolean | false | yes
network_packet | Raw packet access | Boolean | false | yes
allow_protocols|Allowed Network protocols | List of Strings | None | yes

## File Globbing examples
http://wiki.apparmor.net/index.php/QuickProfileLanguage#File_Globbing_examples

## Dependencies

None.

## Example Playbook
```
- hosts: localhost
  remote_user: root
  vars:
    profile_name: example
  roles:
    - ansible-role-apparmor
```

## Usage

- Generate and install profile using this Role
- Use this profile name as value to **--security-opt=** parameter of Docker run CLI  or to **SecurityOpt** of Docker remote API.
  Example -
    ```
    docker run --security-opt="apparmor:example"
    ```

## ToDo

* AppArmor
  - [ ] Necessary packages install
  - [ ] Enable / Disable service
* Add AppArmor profile management:
  - [x] Create
  - [ ] Remove

## More Information
- https://help.ubuntu.com/14.04/serverguide/apparmor.html
- http://wiki.apparmor.net/index.php/QuickProfileLanguage
- http://wiki.apparmor.net/index.php/AppArmor_Core_Policy_Reference

## Similar project(s)
- https://github.com/jfrazelle/bane
- https://github.com/debops-contrib/ansible-apparmor

## License
MIT

## Author Information
Tanmaya Anand - http://StackExpress.com/
