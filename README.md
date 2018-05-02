# mattermost-hubot

Installs and configure hubot for the use with a Mattermost instance.

## Requirements

A Debian-based system

## Role Variables

| Name                                   | Required/Default                | Description                                                                                               |
|:---------------------------------------|:--------------------------------|:----------------------------------------------------------------------------------------------------------|
| `mattermost_hubot_install_path`        | `/var/www/mattermost-hubot`     | Path where to install the hubot files to                                                                  |
| `mattermost_hubot_user`                | `www-data`                      | User under which the hubot should run. The user has to exist                                              |
| `mattermost_hubot_group`               | `www-data`                      | Group under which the hubot should run. The group has to exist                                            |
| `mattermost_hubot_mattermost_host`     | :heavy_check_mark:              | URL to the mattermost instance                                                                            |
| `mattermost_hubot_mattermost_team`     | :heavy_check_mark:              | Team name where the hubot should run under                                                                |
| `mattermost_hubot_mattermost_user`     | :heavy_check_mark:              | The user that should be used to login                                                                     |
| `mattermost_hubot_mattermost_password` | :heavy_check_mark:              | The password for `mattermost_hubot_mattermost_user`                                                       |
| `mattermost_hubot_websocket_port`      | `443`                           | Overrides the default port 443 for websocket (`wss://`) connections                                       |
| `mattermost_hubot_http_port`           | `443`                           | Overrides the default port (80 or 443) for http:// or https:// connections                                |
| `mattermost_hubot_tls_verify`          | `True`                          | Set to `False` to disable certificate verfication                                                         |
| `mattermost_hubot_use_tls`             | `True`                          | Set to `False` to switch to http/ws protocols                                                             |
| `mattermost_hubot_log_level`           | `info`                          | Set log level                                                                                             |
| `mattermost_hubot_reply`               | `True`                          | Set to `False` to stop posting reply responses as comments                                                |
| `mattermost_hubot_ignore_users`        | ` `                             | List of users that should be ignored                                                                      |
| `mattermost_hubot_owner`               | :heavy_check_mark:              | Mail of person that runs this bot                                                                         |
| `mattermost_hubot_name`                | `James`                         | Name under which the bot should react                                                                     |
| `mattermost_hubot_description`         | `Your friendly and helpful bot` | Description which the bot should use                                                                      |
| `mattermost_hubot_enviroment`          | `{}`                            | Dictionary to set more enviroment variables. The key is the variable name and the value the value         |
| `mattermost_hubot_plugins`             | See below                       | List of plugins to be installed. Name of the package is the same name used in the npm package repository. |

### `mattermost_hubot_plugins` Default
Per default following packages are installed:
  - hubot-diagnostics
  - hubot-help
  - hubot-heroku-keepalive
  - hubot-google-images
  - hubot-google-translate
  - hubot-pugme
  - hubot-maps
  - hubot-redis-brain
  - hubot-rules
  - hubot-shipit

## Example Playbook

```yml
- hosts: all
  become: true
  vars:
    mattermost_hubot_mattermost_team: teamname
    mattermost_hubot_mattermost_user: hubot
    mattermost_hubot_mattermost_password: yourpassword
    mattermost_hubot_mattermost_host: url.to.your.mattermost.instance.com
    mattermost_hubot_owner: your@mailaddress.com
    mattermost_hubot_enviroment:
      - REDIS_URL: redis://:password@192.168.0.1:16379/prefix 
    mattermost_hubot_plugins:
      - hubot-diagnostics
      - hubot-help
      - hubot-google-images
      - hubot-google-translate
      - hubot-pugme
      - hubot-maps
      - hubot-redis-brain
      - hubot-rules
      - hubot-shipit
      - hubot-tell-a-joke
      - hubot-voting
  roles:
    - mattermost-hubot
```

## License

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-sa/4.0/).


## Author Information

- [Fritz Otlinghaus (Scriptkiddi)](https://github.com/scriptkiddi) _fritz.otlinghaus@stuvus.uni-stuttgart.de_
