# Creating a registry

The created [registry](../../concepts/registry.md) can be used by any users and [service accounts](../../../iam/concepts/users/service-accounts.md) that have rights for the [folder](../../../resource-manager/concepts/resources-hierarchy.md#folder).

{% list tabs %}

- Management console

  1. In the [management console]({{ link-console-main }}), select the folder to create a registry in.

  1. In the list of services, select **Container Registry**.

  1. Specify a name for the registry.

     {% include [name-format](../../../_includes/name-format.md) %}

  1. Click **Create registry**.

- CLI

  {% include [cli-install](../../../_includes/cli-install.md) %}

  {% include [default-catalogue](../../../_includes/default-catalogue.md) %}

  1. Make sure that a registry has not been created in the folder yet:

     ```bash
     yc container registry list
     ```

     Command execution result:

     ```bash
     +----+------+-----------+
     | ID | NAME | FOLDER ID |
     +----+------+-----------+
     +----+------+-----------+
     ```

     If the folder already contains a registry, see [Updating a registry](registry-update.md) for information about how you can change it.

  1. Create a registry:

     ```bash
     yc container registry create --name my-reg
     ```

     Command execution result:

     ```bash
     done
     id: crpd50616s9a2t7gr8mi
     folder_id: b1g88tflru0ek1omtsu0
     name: my-reg
     status: ACTIVE
     created_at: "2019-01-09T14:34:06.601Z"
     ```

     {% include [name-format](../../../_includes/name-format.md) %}
     
     * The flag `--name` is optional. You can create a registry without a name and access it by its ID.
     * The `name` field is user-defined: it is used for listing in the YC CLI and is **not used** in the Docker CLI.

  1. Make sure the registry was created:

     ```bash
     yc container registry list
     ```

     Command execution result:

     ```bash
     +----------------------+--------+----------------------+
     |          ID          |  NAME  |      FOLDER ID       |
     +----------------------+--------+----------------------+
     | crpd50616s9a2t7gr8mi | my-reg | b1g88tflru0ek1omtsu0 |
     +----------------------+--------+----------------------+
     ```

- API

  To create a registry, use the [create](../../api-ref/Registry/create.md) method for the [Registry](../../api-ref/Registry/) resource.

- Terraform

  If you don't have Terraform, [install it and configure the {{ yandex-cloud }} provider](../../../tutorials/infrastructure-management/terraform-quickstart.md#install-terraform).

  1. To a configuration file, add the parameters of the registry that you want to create. For example, you can use the file `example.tf` from the `~/yandex-cloud-terraform` directory:

     ```
     resource "yandex_container_registry" "my-reg" {
       name = "my-registry"
       folder_id = "<folder ID>"
       labels = {
         my-label = "my-label-value"
       }
     }
     ```

     Where:
     * `name`: Registry name.
     * `folder_id`: ID of the folder.
     * `labels`: Set of [labels](../../../overview/concepts/services.md#labels).

     For more information about the resources you can create using Terraform, see the [provider documentation]({{ tf-provider-link }}).

  1. Check that the configuration file is correct.

     1. Use the command line to go to the directory where you saved the configuration file:

        ```bash
        cd /Users/<username>/yandex-cloud-terraform
        ```

     1. Run the check using the command:

        ```bash
        terraform plan
        ```

        Command execution result:

        ```
        Refreshing Terraform state in-memory prior to plan...
        The refreshed state will be used to calculate this plan, but will not be
        persisted to local or remote state storage.
        ...
        Note: You didn't specify an "-out" parameter to save this plan, so Terraform
        can't guarantee that exactly these actions will be performed if
        "terraform apply" is subsequently run.
        ```

  1. Create a registry.

     1. Run the command:

        ```bash
        terraform apply
        ```

        Command execution result:

        ```bash
        An execution plan has been generated and is shown below.
        Resource actions are indicated with the following symbols:
          + create
        ...
          Terraform will perform the actions described above.
          Only 'yes' will be accepted to approve.
        
          Enter a value:
        ```

     1. Confirm creation of the registry. To do this, type `yes` and press **Enter**:

        ```bash
        Enter a value: yes
        ```

        Command execution result:

        ```bash
        yandex_container_registry.default: Creating...
        yandex_container_registry.default: Creation complete after 4s [id=crpuljdfqoj3ve9mtbt1]
        
        Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
        ```

        A registry named `my-registry` is created in the folder.

     1. Check the resources and their settings in the [management console]({{ link-console-main }}).

{% endlist %}