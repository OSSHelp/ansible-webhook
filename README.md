# webhook

[![Build Status](https://drone.osshelp.ru/api/badges/ansible/webhook/status.svg)](https://drone.osshelp.ru/ansible/webhook)

Ansible role for [webhook](https://github.com/adnanh/webhook) installation and configuration.

## Usage (example)

```yaml
    - hosts: all
      roles:
        - { role: webhook,
              webhook: {
              hotreload: true,
              listen: '0.0.0.0',
              port: 8080,
              prefix: 'webhook',
              verbose: false,
              hooks: [ 'deployment' ],
              headers: [ 'X-Custom-Header=some-value' ]
            }
        }
```

## Available parameters

### Main

Short description here.

| Param | Description |
| -------- | -------- |
| user | User to create for webhook-server. |
| extra_groups | Extra groups to add created user to. |
| download_url | Url to get binary from. |
| checksum_url | Url to get checksums from. |
| download_dir | Absolute path to temporal dir for binary placement before moving to more suitable dir. |
| binary_dir | Absolute path to directory where binary will be placed. |
| scripts_dir | Absolute path to directory where scripts will be placed. |
| conf_dir | Absolute path to directory with webhook-server configuration files. |
| logs_dir | Absolute path to directory that will be used for webhook-server logs storage. |
| templates_dir | Absolute path to directory that will be used for initial-setup script and templates placement. |
| webhook_hooks_source_dir | Relative path to hooks (j2-templates of jsons) in current repository |
| webhook_scripts_source_dir | Relative path to scripts templates in current repository |
| default_setup | Whether to install [deploy-functions](https://gitea.osshelp.ru/ansible/deploy-functions) and additional stuff for initial setup via deployment. |
| default_sudoers |  Whether to generate sudoers.d config |
| webhook_sudo_scripts | List of script names in scripts_dir for enabling sudo access to |

### Webhook-server params

You can control all of the params via overriding webhook array (see defaults/main.yml)

## FAQ

### ERROR: Found unknown escape character

If there is an error like this in logs:

> [webhook] couldn't load hooks from file! error converting YAML to JSON: yaml: line 63: found unknown escape character

Then you should use double character ‘\’ in your regexps. For example:

```yaml
    "regex": "^\\w+(\\d+)?(-\\w+)?-(prod)$",
```

## Useful links

- [Official documentation](https://github.com/adnanh/webhook/tree/master/docs)
- [Our article](https://oss.help/kb3989)

## TODO

- add logrotate config for files in logs_dir

## License

GPL3

## Author

OSSHelp Team, see <https://oss.help>
