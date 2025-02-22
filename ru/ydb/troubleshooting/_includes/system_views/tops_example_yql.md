---
sourcePath: ru/ydb/ydb-docs-core/ru/core/troubleshooting/_includes/system_views/tops_example_yql.md
---
  Топ запросов по времени выполнения за последнюю минуту, когда случались запросы

  ```sql
  PRAGMA AnsiInForEmptyOrNullableItemsCollections;
  $last = (
      SELECT
          MAX(IntervalEnd)
      FROM `.sys/top_queries_by_duration_one_minute`
  );
  SELECT
      IntervalEnd,
      Rank,
      QueryText,
      Duration
  FROM `.sys/top_queries_by_duration_one_minute`
  WHERE IntervalEnd IN $last
  ```

  Запросы, прочитавшие больше всего байт, в разбивке по минутам

  ```sql
  SELECT
      IntervalEnd,
      QueryText,
      ReadBytes,
      ReadRows,
      Partitions
  FROM `.sys/top_queries_by_read_bytes_one_minute`
  WHERE Rank = 1
  ```