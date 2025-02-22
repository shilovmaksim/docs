---
sourcePath: ru/ydb/ydb-docs-core/ru/core/yql/reference/yql-core/builtins/_includes/aggregation/max_min_by.md
sourcePath: ru/ydb/yql/reference/yql-core/builtins/_includes/aggregation/max_min_by.md
---
## MAX_BY и MIN_BY {#max-min-by}

**Сигнатура**
```
MAX_BY(T1?, T2)->T1?
MAX_BY(T1, T2)->T1?
MAX_BY(T1, T2, limit:Uint64)->List<T1>?

MIN_BY(T1?, T2)->T1?
MIN_BY(T1, T2)->T1?
MIN_BY(T1, T2, limit:Uint64)->List<T1>?
```

Вернуть значение первого аргумента для строки таблицы, в которой второй аргумент оказался минимальным/максимальным.

Опционально можно указать третий аргумент N, который влияет на поведение в случае, если в таблице есть несколько строк с одинаковым минимальным или максимальным значением:

* Если N не указано — будет возвращено значение одной из строк, а остальные отбрасываются.
* Если N указано — будет возвращен список со всеми значениями, но не более N, все значения после достижения указанного числа отбрасываются.

При выборе значения N рекомендуется не превышать порядка сотен или тысяч, чтобы не возникало проблем с ограниченной доступной памятью на кластерах {{ backend_name }}.

Если для задачи обязательно нужны все значения, и их количество может измеряться десятками тысяч и больше, то вместо данных агрегационных функций следует использовать `JOIN` исходной таблицы с подзапросом, где по ней же сделан `GROUP BY + MIN/MAX` на интересующих вас колонках.

{% note warning "Внимание" %}

Если второй аргумент всегда NULL, то результатом агрегации будет NULL.

{% endnote %}

При использовании [фабрики агрегационной функции](../../basic.md#aggregationfactory) в качестве первого аргумента [AGGREGATE_BY](#aggregateby) передается `Tuple` из значения и ключа.

**Примеры**
``` yql
SELECT
  MIN_BY(value, LENGTH(value)),
  MAX_BY(value, key, 100)
FROM my_table;
```

``` yql
$min_by_factory = AggregationFactory("MIN_BY");
$max_by_factory = AggregationFactory("MAX_BY", 100);

SELECT
    AGGREGATE_BY(AsTuple(value, LENGTH(value)), $min_by_factory),
    AGGREGATE_BY(AsTuple(value, key), $max_by_factory)
FROM my_table;
```
