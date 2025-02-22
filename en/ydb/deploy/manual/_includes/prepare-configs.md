---
sourcePath: en/ydb/ydb-docs-core/en/core/deploy/manual/_includes/prepare-configs.md
---
## Prepare a configuration file for {{ ydb-short-name }} {# preprate-configs}

Download a sample config for the appropriate failure model of your cluster:

* [block-4-2](https://github.com/ydb-platform/ydb/blob/main/ydb/deploy/yaml_config_examples/block-4-2.yaml): For a single-datacenter cluster.
* [mirror-3dc](https://github.com/ydb-platform/ydb/blob/main/ydb/deploy/yaml_config_examples/mirror-3dc-9-nodes.yaml): For a cross-datacenter cluster consisting of 9 nodes.
* [mirror-3dc](https://github.com/ydb-platform/ydb/blob/main/ydb/deploy/yaml_config_examples/mirror-3dc-3-nodes.yaml): For a cross-datacenter cluster consisting of 3 nodes.

1. In the host_configs section, specify all disks and their types on each cluster node. Possible disk types:

```text
host_configs:
- drive:
  - path: /dev/disk/by-partlabel/ydb_disk_01
    type: SSD
  host_config_id: 1
```

* ROT (rotational): HDD.
* SSD: SSD or NVMe.

2. In the `hosts` section, specify the FQDN of each node, their configuration and location in a `data_center` or `rack`.

```text
hosts:
- host: node1.ydb.tech
  host_config_id: 1
  walle_location:
    body: 1
    data_center: 'zone-a'
    rack: '1'
- host: node2.ydb.tech
  host_config_id: 1
  walle_location:
    body: 2
    data_center: 'zone-b'
    rack: '1'
- host: node3.ydb.tech
  host_config_id: 1
  walle_location:
    body: 3
    data_center: 'zone-c'
    rack: '1'
```

