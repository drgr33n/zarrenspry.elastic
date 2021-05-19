#################################
zarrenspry.elastic.elassticsearch
#################################

Provisions a single elasticsearch node with x-pack security enabled. This role is based
on the `geerlingguy/ansible-role-elasticsearch <https://github.com/geerlingguy/ansible-role-elasticsearch>`_.

This role is also in a pre-alpha state so don't expect it to work yet :D

Table of Contents
#################
- `Requirements`_
   -  `Operating systems`_
- `Variables`_
- `Author`_

Requirements
############
Operating systems
-----------------
This role will work on the following Operating systems.

- CentOS 7

Variables
#########
+-------------------------------------------+--------------+--------------------------+------------------------------------------------------+
| Name                                      | Type         | Default                  | Description                                          |
+===========================================+==============+==========================+======================================================+
| elasticsearch_version                     | string       | 7x                       | Major version to install                             |
+-------------------------------------------+--------------+--------------------------+------------------------------------------------------+
| elasticsearch_service_enabled             | boolean      | true                     | Enable/Disable elasticsearch systemd service.        |
+-------------------------------------------+--------------+--------------------------+------------------------------------------------------+
| elasticsearch_network_host                | string       | localhost                | Set the bind address to a specific IP (IPv4 or IPv6) |
+-------------------------------------------+--------------+--------------------------+------------------------------------------------------+
| elasticsearch_http_port                   | integer      | 9200                     | Set the desired HTTP port                            |
+-------------------------------------------+--------------+--------------------------+------------------------------------------------------+
| elasticsearch_jvm_heap_size_min           | string       | 1g                       | Set the init JVM heap size.                          |
+-------------------------------------------+--------------+--------------------------+------------------------------------------------------+
| elasticsearch_jvm_heap_size_max           | string       | 1g                       | Set the max JVM heap size.                           |
+-------------------------------------------+--------------+--------------------------+------------------------------------------------------+
| elasticsearch_home_dir                    | string       | /usr/share/elasticsearch | Set the elasticsearch home directory.                |
+-------------------------------------------+--------------+--------------------------+------------------------------------------------------+
| elasticsearch_conf_dir                    | string       | /etc/elasticsearch       | Set the elasticsearch configuration directory.       |
+-------------------------------------------+--------------+--------------------------+------------------------------------------------------+
| elasticsearch_xpack_enabled               | boolean      | true                     | Enable/Disable xpack security add-on                 |
+-------------------------------------------+--------------+--------------------------+------------------------------------------------------+
| elasticsearch_api_basic_auth_password     | string       | changeme                 | Bootstrap administrative password.                   |
+-------------------------------------------+--------------+--------------------------+------------------------------------------------------+
| elasticsearch_tls_keystore_password       | string       | changeme                 | TLS CA keystore password.                            |
+-------------------------------------------+--------------+--------------------------+------------------------------------------------------+
| elasticsearch_system_user_passwords       | dict         | See table below          | Built-in user passwords.                             |
+-------------------------------------------+--------------+--------------------------+------------------------------------------------------+
| elasticsearch_keystore_additional_entries | list         | []                       | Additional keystore entries.                         |
+-------------------------------------------+--------------+--------------------------+------------------------------------------------------+
| elasticsearch_users                       | dict         | See table below          | Users to be created upon provisioning.               |
+-------------------------------------------+--------------+--------------------------+------------------------------------------------------+

elasticsearch_system_user_passwords

+------------------------+--------+----------+---------------------------------------+
| Name                   | Type   | Default  | Description                           |
+========================+========+==========+=======================================+
| apm_system             | string | changeme | apm_system user password.             |
+------------------------+--------+----------+---------------------------------------+
| kibana_system          | string | changeme | kibana_system user password.          |
+------------------------+--------+----------+---------------------------------------+
| logstash_system        | string | changeme | logstash_system user password.        |
+------------------------+--------+----------+---------------------------------------+
| beats_system           | string | changeme | beats_system user password.           |
+------------------------+--------+----------+---------------------------------------+
| remote_monitoring_user | string | changeme | remote_monitoring_user user password. |
+------------------------+--------+----------+---------------------------------------+

elasticsearch_users

The elasticsearch_users variable takes a dict of strings that is converted to JSON and passed
onto the elasticsearch API. See the example below for further details.

.. code-block:: yaml

    elasticsearch_users:
      admin:
        password: changeme
        email: admin@acme.local
        full_name: Systems Administrator
        enabled: true
        roles:
          - superuser
          - kibana_admin

Author
######
Zarren Spry <zarrenspry@gmail.com>