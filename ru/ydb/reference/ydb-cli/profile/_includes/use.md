---
sourcePath: ru/ydb/ydb-docs-core/ru/core/reference/ydb-cli/profile/_includes/use.md
---
# Использование профиля

## Соединение по выбранному профилю {#explicit}

Профиль может быть применен при запуске команды {{ ydb-short-name }} CLI указанием опции `--profile <profile_name>`:

``` bash
{{ ydb-cli }} --profile <profile_name> <команда и опции команды>
```

Например:

``` bash
{{ ydb-cli }} --profile mydb1 scheme ls -l
```

В таком случае все параметры соединения с БД будут взяты из профиля. При этом, если в профиле не указано параметров аутентификации, то {{ ydb-short-name }} CLI попробует их определить по переменным окружения, как описано в статье [Соединение с БД и аутентификация - Переменные окружения](../../connect.md#env).

## Соединение по выбранному профилю и параметрам командной строки {#explicit-and-pars}

Опция `--profile` может быть не единственной среди параметров соединения в командной строке, например:

``` bash
{{ ydb-cli }} --profile mydb1 -d /local2 scheme ls -l
```

``` bash
{{ ydb-cli }} --profile mydb1 --user alex scheme ls -l
```

В таком случае указанные в командной строке параметры соединения имеют приоритет перед сохраненными в профиле. Такой формат позволяет переиспользовать профили для соединения с разными БД или под разными учетными записями. Также, указание в командной строке параметра аутентификации (как `--user alex` в примере выше) отключает проверку переменных окружения независимо от их наличия в профиле.

## Соединение по активированному профилю {#implicit}

Если в командной строке не указана опция `--profile`, то {{ ydb-short-name }} CLI попробует взять из текущего активированного профиля все параметры соединения, которые он не смог определить другими способами (из опций командной строки или переменных окружения, как описано в статье [Соединение с БД и аутентификация](../../connect.md)).

Неявное применение активированного профиля может приводить к ошибкам, поэтому перед использованием данного режима рекомендуется изучить статью [Активированный профиль](../activate.md).