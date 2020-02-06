# RabbitMQ Ansible Role

## Version

See:

- [RabbitMQ - Server Releases](https://www.rabbitmq.com/releases/rabbitmq-server/)

Set the `rabbitmq_version` variable to define the version of RabbitMQ to install.

```yaml
rabbitmq_version: '3.8.1'
```

## Users

See:

- [Ansible - RabbitMQ User Module](http://docs.ansible.com/ansible/rabbitmq_user_module.html)
- [RabbitMQ - Access Control](https://www.rabbitmq.com/access-control.html)

Set the `rabbitmq_users` variable to define an array of present users.

```yaml
rabbitmq_users:
  - user: admin
    password: admin
    tags: administrator
```

| parameter      | required | default | choices | comments |
| -------------- | -------- | ------- | ------- | -------- |
| configure_priv | no       | .*      |         |          |
| node           | no       | rabbit  |         |          |
| password       | yes      |         |         |          |
| read_priv      | no       | .*      |         |          |
| tags           | no       |         |         |          |
| user           | yes      |         |         |          |
| vhost          | no       | /       |         |          |
| write_priv     | no       | .*      |         |          |

### Remove Users

Set the `rabbitmq_users_absent` variable to define an array of absent users.

```yaml
rabbitmq_users_absent:
  - guest
```

## Virtual Hosts

See:

- [Ansible - RabbitMQ Virtual Host Module](http://docs.ansible.com/ansible/rabbitmq_vhost_module.html)
- [RabbitMQ - Virtual Hosts](https://www.rabbitmq.com/vhosts.html)

Set the `rabbitmq_vhosts` variable to define an array of present virtual hosts.

```yaml
rabbitmq_vhosts:
  - /one
  - name: /two
    node: rabbit
    tracing: no
```

| parameter  | required | default | choices                          | comments |
| ---------- | -------- | ------- | -------------------------------- | -------- |
| name       | yes      |         |                                  |          |
| node       | no       | rabbit  |                                  |          |
| tracing    | no       | no      | <ul><li>yes</li><li>no</li></ul> |          |

### Remove Virtual Hosts

Set the `rabbitmq_vhosts_absent` variable to define an array of absent virtual hosts.

```yaml
rabbitmq_vhosts_absent:
  - /vhost
```

## Plugins

See:

- [Ansible - RabbitMQ Plugin Module](http://docs.ansible.com/ansible/rabbitmq_plugin_module.html)
- [RabbitMQ - Plugins](https://www.rabbitmq.com/plugins.html)

Set the `rabbitmq_plugins` variable to define an array of enabled plugins.

```yaml
rabbitmq_plugins:
  - name: rabbitmq_management
    broker_state: online
  - name: rabbitmq_delayed_message_exchange
    url: http://www.rabbitmq.com/community-plugins/v3.6.x/rabbitmq_delayed_message_exchange-0.0.1.ez
```

| parameter    | required | default | choices             | comments            |
| -------------| -------- | ------- | ------------------- | ------------------- |
| name         | yes      |         |                     |                     |
| broker_state | no       | online  | [online, offline]   |                     |
| url          | no       |         |                     | Installs the plugin |
| state        | no       | enabled | [enabled, disabled] |                     |

### Disable Plugins

Set the `state` of a plugin to disabled.

## Configuration

See:

- [RabbitMQ - Configuration](https://www.rabbitmq.com/configure.html)

Set the `rabbitmq_config` variable to define the configuration.

```yaml
rabbitmq_config:
  listeners.tcp.default: 5672
```

Set the `rabbitmq_env` variable to define the environment variables. Note that the keys should not contain the
"RABBITMQ_" prefix.

```yaml
rabbitmq_env:
  DIST_PORT: 25672
```

## Clustering

Clustering can be configured through a config file as described in [Config AutoDiscovery (RMQ doc)](https://www.rabbitmq.com/cluster-formation.html#peer-discovery-classic-config). 
This should be more resilient than invoking `rabbitmqctl` to do clustering related operations. Use `rabbitmq_config_keys` to insert the required keys in the config.


/!\ Please note that AutoDiscovery only work with pristine nodes as RabbitMQ will only read this config at the very first startup.

(You can always hard reset an existing node by removing its MnesiaDB if you don't care about its content)

### Erlang Cookie

Set the `rabbitmq_erlang_cookie` variable to define the Erlang cookie.

```yaml
rabbitmq_erlang_cookie: g9avtqdzdm2p5oe9
```

## License

MIT
