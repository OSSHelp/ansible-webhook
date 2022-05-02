# webhook

[![Build Status](https://drone.osshelp.ru/api/badges/ansible/webhook/status.svg)](https://drone.osshelp.ru/ansible/webhook)

Ansible role for [webhook](https://github.com/adnanh/webhook) installation and configuration.

## Usage (example)

```yaml
    - role: webhook
      webhook_default_setup: true
      webhook_extra_groups: [nogroup, users]
      webhook_params:
        hotreload: true
        listen: 0.0.0.0
        port: 12345
        prefix: hook
        verbose: true
        scripts: ['lxhelper-deployment']
        headers: ['X-Data-Source=demo']
      webhook_lxhelper_deployment:
        token: token_placeholder
        target_regex: '^(testing|someclient)$'
      webhook_custom_hooks:
        - id: uptime
          execute-command: uptime
          command-working-directory: /tmp
          include-command-output-in-response: true
          include-command-output-in-response-on-error: true
```

For example of advanced custom webhooks configuration check `webhook_default_hooks` list in [defaults](defaults/main.yml).

## Available parameters

### Main

| Param | Default | Description |
| -------- | -------- | -------- |
| `webhook_version` | `2.6.10` | Version to install, is being used in default binary/checksum urls. |
| `webhook_user` | `webhook` | User to create for webhook-server. |
| `webhook_extra_groups` | `[]` | Extra groups to add created user to. |
| `webhook_default_hooks` | See [defaults](defaults/main.yml) | List, describing default webhooks. |
| `webhook_disable_default_hooks` | `false` | If set to `true` no default webhooks will be added. |
| `webhook_custom_hooks` | `[]` | List, describing custom webhooks. Will be appended to `webhook_default_hooks` if `webhook_disable_default_hooks` is set to `false`. |
| `webhook_download.url` | See [defaults](defaults/main.yml) | Url to get binary from. |
| `webhook_download.checksum` | See [defaults](defaults/main.yml) | Url to get checksums from. |
| `webhook_dirs` | See [defaults](defaults/main.yml) | Absolute path to directories (download, scripts, binary, conf, logs, templates) |
| `webhook_dirs.scripts_source` | `scripts` | Relative path to scripts j2-templates in current repository |
| `webhook_default_setup` | `false` | Whether to install [deploy-functions](https://gitea.osshelp.ru/ansible/deploy-functions) and additional stuff for initial setup during deployment. |
| `webhook_default_sudoers` | `true` |  Whether to generate sudoers.d config |
| `webhook_sudo_scripts` | `[lxhelper]` | List of script names in `webhook_dirs.scripts` for enabling sudo access to |

### Webhook-server params

You can control all of the params via overriding `webhook_params` array (see [defaults](defaults/main.yml))

## FAQ

### ERROR: Found unknown escape character

If there is an error like this in logs:

> [webhook] couldn't load hooks from file! error converting YAML to JSON: yaml: line 63: found unknown escape character

Then you should use double character ‘\’ in your regexps. For example:

```yaml
regex: "^\\w+(\\d+)?(-\\w+)?-(prod)$"
```

## Useful links

- [Official documentation](https://github.com/adnanh/webhook/tree/master/docs)
- [Our article](https://oss.help/kb3989)

## TODO

- add logrotate config

## License

GPL3

## Author

OSSHelp Team, see <https://oss.help>
