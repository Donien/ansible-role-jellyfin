# Ansible Role - Jellyfin

This role aims to install Jellyfin as well as allow for configuration of certain aspects of Jellyfin.

- [Requirements](#requirements)
- [Role Variables](#role-variables)
- [Example Playbook](#example-playbook)
- Additional Resources To Manage
    - [Users](doc/users.md)
    - [Library](doc/library.md)

---

# Requirements

None yet.

# Role Variables

- `jellyfin_http_port`
    - Description: The HTTP port Jellyfin should listen on.
    - Type: `int/string`
    - Default: `8096`
- `jellyfin_http_port_old`
    - Description: The HTTP port previously used. Setting this manually is necessary when changing the HTTP port from a non-default number to a new one.
    - Type: `int/string`
    - Default: `8096`
- `jellyfin_https_port`
    - Description: The HTTPS port Jellyfin should listen on.
    - Type: `int/sring`
    - Default: `8920`
- `jellyfin_admin_username`
    - Description: The username used for API calls against Jellyfin. Will also be created as the first user, if Jellyfin is set up freshly.
    - Type: `string`
    - Default: `Jellyfin`
- `jellyfin_admin_password`
    - Description: The password for the user used for API calls against Jellyfin.
    - Type: `string`
    - Default: `Jellyfin`
- `jellyfin_remote_access`
    - Description: Whether to allow connections to Jellyfin from outside local networks.
    - Type: `bool`
    - Default: `false`
- `jellyfin_automatic_port_mapping`
    - Description: Whether automatic port mapping should be enabled.
    - Type: `bool`
    - Default: `false`
- `jellyfin_ui_culture`
    - Description: Prefered display language. (Currently seems broken. Manual per user display language settings work though.)
    - Type: `string`
    - Default: `en-GB`
- `jellyfin_metadata_language`
    - Description: Prefered metadat language.
    - Type: `string`
    - Default: `en`
- `jellyfin_metadata_country_code`
    - Description: Prefered metadata language country.
    - Type: `string`
    - Default: `GB`
- `jellyfin_bind_addresses`
    - Description: The addresses Jellyfin should bind to.
    - Type: `list`
    - Default: `[ "{{ ansible_default_ipv4.address }}" ]`
- `jellyfin_local_networks`
    - Description: The addresses / networks Jellyfin should consider to be local networks.
    - Type: `list`
    - Default: `[ 127.0.0.0/8, "{{ ansible_default_ipv4.address}}/{{ ansible_default_ipv4.prefix }}" ]`

# Example Playbook

```
---

- name: Jellyfin Role
  hosts:
    - my_host

  vars:
    jellyfin_admin_username: "admin"
    jellyfin_admin_password: "admin"

    jellyfin_http_port: 8765

    jellyfin_remote_access: true

    jellyfin_ui_culture: "de"
    jellyfin_metadata_country_code: "DE"
    jellyfin_metadata_language: "de"

  roles:
    - jellyfin
```
