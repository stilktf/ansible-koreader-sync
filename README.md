Ansible Role to set up a KOReader Sync server
=========

This Ansible role sets up a [KOReader sync server](https://github.com/koreader/koreader-sync-server) via Docker. Using this role, you can deploy a KOReader sync server easily & consistently.

> [!NOTE]
> This role is not officially supported by the KOReader developers.

Requirements
------------

This role uses the Docker module, so you must have Docker already installed on the host you want to use the role on. If you are going to build the Docker image, you need Git installed (usually this is installed with Ansible)

Role Variables
--------------

### Default variables
| Variable name    | Explanation                                                                                                | Default value         |
| -------------    | -----------                                                                                                | -------------         |
| server_port      | The port to forward the server to                                                                          | 7200                  |
| container_name   | The name of the sync server's container                                                                    | kosync                |
| server_directory | Where to store the sync server's files                                                                     | /opt/(container name) |
| server_version   | The version to use (from [Docker](https://hub.docker.com/r/koreader/kosync))                               | latest                |
| build_image      | Whether to build the Docker image. This is useful for architectures the image doesn't support, like arm64. | false                 |

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

```yaml
---
- hosts: localhost
  remote_user: root
  roles:
    - role: stilktf.koreader_sync
      server_port: 7200
      container_name: kosync
      server_directory: /opt/kosync
      server_version: latest
```

To deploy your server using a web server like Caddy, you could use this configuration:
```caddyfile
sync.yourdomain.xyz {
  reverse_proxy :7200 {
    transport http {
      tls_insecure_skip_verify
    }
  }
}
```

License
-------

Apache 2.0

Author Information
------------------

[Website](https://stilk.tf) - [GitHub](https://github.com/stilktf) - [Bluesky](https://bsky.app/profile/stilk.tf)
