With this role you can also create, delete and update users.  
To manage users you need to create the list variable `jellyfin_users` and set the following mandatory attributes per list entry:

- `name`
    - Description: The name of the user to manage.
    - Type: `string`
    - Default: `None`
- `state`
    - Description: The desired state for this user (choices: `present`, `absent`).
    - Type: `string`
    - Default: `present`

Other than the mandatory attributes you can also choose some other attributes:

- `password`
    - Description: The password for the user. If not defined, `jellyfin_default_password` will be used. If set to `""` no password will be set, allowing for passwordless login. This is only used when creating a user.
    - Type: `string`
    - Default: Value of `jellyfin_default_password`
- `admin`
    - Description: Whether the user should be an administrator.
    - Type: `bool`
    - Default: `false`
- `hidden`
    - Description: Whether the user should be displayed as a choosable option when loggin in.
    - Type: `bool`
    - Default: `false`
- `audio_language`
    - Description: Sets the prefered audio language. Here the **Three Letter ISO Language Name** is needed (e.g. `eng` for english or `ger` for german).
    - Type: `string`
    - Default: `None`
- `subtitle_language`
    - Description: Sets the prefered subtitle language. Here the **Three Letter ISO Language Name** is needed (e.g. `eng` for english or `ger` for german).
    - Type: `string`
    - Default: `None`
- `play_default_track`
    - Description: Whether to play the default audio track regardless of language preferences.
    - Type: `bool`
    - Default: `None`

> In most cases *no default value* means that the current value for the given setting will be kept.


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

    jellyfin_users:
      - name: "testuser1"
        state: "present"
        password: ""
        admin: false
        hidden: false
        audio_language: "ger"
        subtitle_language: "ger"
        play_default_track: false
      - name: "testuser2"
        state: "absent"

  roles:
    - jellyfin
```
