---
editable: false
sourcePath: ru/_api-ref/datalens/function-ref/TOPONYM_TO_GEOPOINT.md
---

# TOPONYM_TO_GEOPOINT



#### Синтаксис {#syntax}


```
TOPONYM_TO_GEOPOINT( name )
```

#### Описание {#description}
Преобразует топоним (название города, региона или страны) `name` в формат `Геоточка`.
См. полный [список топонимов]({{ geopoints-list-link }}).

**Типы аргументов:**
- `name` — `Строка`


**Возвращаемый тип**: `Геоточка`

#### Пример {#examples}



| **[value]**              | **TOPONYM_TO_GEOPOINT([value])**   |
|:-------------------------|:-----------------------------------|
| `'Комсомольск-на-Амуре'` | `'[50.550055,137.008685]'`         |
| `'Рио-де-Жанейро'`       | `'[-22.905722,-43.189130]'`        |
| `'Пущино'`               | `'[54.832484,37.620986]'`          |




#### Поддержка источников данных {#data-source-support}

`Материализованный датасет`.
