# Управление подкластерами {{ dataproc-name }}

Помимо [изменения настроек](subcluster-update.md) отдельного подкластера вы можете создавать новые и удалять имеющиеся подкластеры.

{% note warning %}

В каждом кластере может быть не больше 1 подкластера с ролью `MASTERNODE`, поэтому создавать и удалять подкластеры с этой ролью невозможно. Также невозможно удалять подкластеры с ролью `DATANODE`.

{% endnote %}

## Получить список подкластеров в кластере {#list-subclusters}

{% list tabs %}

- Консоль управления

  1. Перейдите на [страницу каталога]({{ link-console-main }}) и выберите сервис **{{ dataproc-name }}**.

  1. Нажмите на имя нужного кластера, затем выберите вкладку **Подкластеры**.

{% endlist %}


## Добавить подкластер {#add-subcluster}

Количество хостов в кластерах {{ dataproc-name }} ограничено [квотами]({{ link-console-quotas }}) на количество vCPU и объем памяти, которые могут использовать виртуальные машины в вашем облаке. Чтобы увидеть доступные ресурсы, откройте раздел [Квоты]({{ link-console-quotas }}) и найдите блок **Compute Cloud**.

Чтобы добавить подкластер:

{% list tabs %}

- Консоль управления

    1. В [консоли управления]({{ link-console-main }}) выберите нужный каталог.
    1. Выберите сервис **{{ dataproc-name }}** и выберите нужный кластер.
    1. Перейдите в раздел **Подкластеры**.
    1. Нажмите кнопку **Добавить подкластер**.
    1. Выберите количество хостов.
    1. Выберите **Роли** подкластера. Для этого определитесь с сервисами, которые должны быть развернуты на хостах:

       * В подкластерах с ролью `COMPUTENODE` могут быть развернуты:
         * YARN NodeManager;
         * библиотеки Spark.
       * В подкластерах с ролью `DATANODE` могут быть развернуты:
         * HDFS Datanode;
         * YARN NodeManager;
         * HBase RegionServer;
         * библиотеки Spark.

    1. Выберите остальные настройки подкластера:
       * [Класс хостов](../concepts/instance-types.md) — платформа и вычислительные ресурсы, доступные хосту.
       * Тип и размер хранилища.
       * Формат указания сети.
       * Подсеть сети, в которой расположен кластер.
       * (Опционально) Включите опцию **Публичный доступ** для доступа к хостам подкластера из интернета.

          Эту настройку невозможно изменить после создания подкластера.

          {% note tip %}

          Подкластеры `Compute` можно удалить и создать заново с нужным значением этой настройки.

          {% endnote %}

       * (Опционально) Включите опцию **Автоматическое масштабирование**.

    1. Нажмите кнопку **Добавить подкластер**.

    {{ dataproc-name }} запустит операцию создания подкластера.

- Terraform

    1. Откройте актуальный конфигурационный файл {{ TF }} с планом инфраструктуры.

        О том, как создать такой файл, см. в разделе [{#T}](cluster-create.md).

    1. Добавьте в описании кластера {{ dataproc-name }} блок `subcluster_spec` с параметрами нового подкластера:

        ```hcl
        resource "yandex_dataproc_cluster" "<имя кластера>" {
          ...
          cluster_config {
            ...
            subcluster_spec {
              name = "<имя подкластера>"
              role = "<тип подкластера: COMPUTENODE или DATANODE>"
              resources {
                resource_preset_id = "<класс хоста>"
                disk_type_id       = "<тип хранилища>"
                disk_size          = <объем хранилища, ГБ>
              }
              subnet_id   = "<идентификатор подсети в {{ TF }}>"
              hosts_count = <число хостов в подкластере>
              ...
            }
          }
        }
        ```

    1. Проверьте корректность настроек.

        {% include [terraform-validate](../../_includes/mdb/terraform/validate.md) %}

    1. Подтвердите изменение ресурсов.

        {% include [terraform-apply](../../_includes/mdb/terraform/apply.md) %}

    Более подробную информацию о ресурсах, которые вы можете создать с помощью Terraform, см. в [документации провайдера]({{ tf-provider-link }}/dataproc_cluster).

{% endlist %}

## Удалить подкластер {#remove-host}

{% note warning %}

Удалить подкластеры с ролью `DATANODE` невозможно.

{% endnote %}

{% list tabs %}

- Консоль управления

    Чтобы удалить подкластер:

    1. В [консоли управления]({{ link-console-main }}) выберите нужный каталог.
    1. Выберите сервис **{{ dataproc-name }}** и выберите нужный кластер.
    1. Перейдите в раздел **Подкластеры**.
    1. Нажмите значок ![image](../../_assets/options.svg) для нужного подкластера и выберите пункт **Удалить**.
    1. (Опционально) Укажите таймаут [декомиссии](../concepts/decommission.md).
    1. Подтвердите удаление.

    {{ dataproc-name }} запустит операцию удаления подкластера.

- Terraform

    1. Откройте актуальный конфигурационный файл {{ TF }} с планом инфраструктуры.

        О том, как создать такой файл, см. в разделе [{#T}](cluster-create.md).

    1. Удалите из описания кластера {{ dataproc-name }} блок `subcluster_spec` нужного подкластера.

    1. Проверьте корректность настроек.

        {% include [terraform-validate](../../_includes/mdb/terraform/validate.md) %}

    1. Подтвердите удаление ресурсов.

        {% include [terraform-apply](../../_includes/mdb/terraform/apply.md) %}

    Более подробную информацию о ресурсах, которые вы можете создать с помощью Terraform, см. в [документации провайдера]({{ tf-provider-link }}/dataproc_cluster).

{% endlist %}
