---
title: "About the empty flag"
description: "Use the empty flag to test your code and build your tables without populating data."
sidebar_label: "The empty flag"
pagination_next: "docs/build/sample-flag"
pagination_prev: null
---

# About the `--empty` flag

:::note

The `--empty` flag is not currently available for Python models. If the flag is used with a Python model, it will be ignored.

:::

During dbt development, you might want to validate that your models are semantically correct without the time-consuming cost of building the entire model in the data warehouse. The [`run`](/reference/commands/run) and [`build`](/reference/commands/build) commands support the `--empty` flag for building schema-only dry runs. The `--empty` flag limits the refs and sources to zero rows. dbt will still execute the model SQL against the target data warehouse but will avoid expensive reads of input data. This validates dependencies and ensures your models will build properly.

### Examples

Run all models in a project while building only the schemas in your development environment:

```
dbt --empty
```

Run a specific model:

```
dbt --select path/to/your_model --empty
```

dbt will build and execute the SQL, resulting in an empty schema in the data warehouse.

#### Opting out of auto-filtering
If there’s an upstream model that does not support `--empty` and you *don’t* want the reference to it to be filtered, you can specify `ref('upstream_model').render()` to opt-out of auto-filtering. This may result in the model containing a non-zero number of rows.
