---
sourcePath: en/ydb/ydb-docs-core/en/core/reference/ydb-cli/_includes/auth/options_cloud_additional.md
---
When using authentication modes that involve token rotation along with regularly re-requesting them from IAM (**Refresh Token** and **Service Account Key**), a special parameter can be set to indicate where the IAM service is located:

- `--iam-endpoint <URL>` : Sets the URL of the IAM service to request new tokens in authentication modes with token rotation. The default value is `"iam.api.cloud.yandex.net"`.

