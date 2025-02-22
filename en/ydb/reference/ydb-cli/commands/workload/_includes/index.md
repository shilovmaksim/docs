---
sourcePath: en/ydb/ydb-docs-core/en/core/reference/ydb-cli/commands/workload/_includes/index.md
---
# Load testing

You can use the `workload` command to run different types of workload against your DB.

General command format:

```bash
{{ ydb-cli }} [global options...] workload [subcommands...]
```

* `global options`: [Global parameters](../../../commands/global-options.md).
* `subcommands`: [Subcommands](#subcomands).

See the description of the command to run the data load:

```bash
{{ ydb-cli }} workload --help
```

## Available subcommands {#subcommands}

The following types of load tests are supported at the moment:

* [Stock](../stock.md): An online store warehouse simulator.

