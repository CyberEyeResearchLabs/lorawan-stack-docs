---
title: Disable
description: ""
summary: Disable Storage Integration for applications and end-devices.
weight: 30
---

The Storage Integration is implemented as an [Application Package]({{< ref "/reference/application-packages" >}}).

{{< note >}} Disabling Storage Integration for applications can be done using {{% tts %}} Console or CLI. Disabling Storage Integration for individual end devices is available only via CLI. {{</ note >}}

## Disable for an Application

{{< tabs/container "Console" "CLI" >}}

{{< tabs/tab "Console" >}}

To disable the integration, you only need to click the **Deactivate Storage Integration** button:

{{< figure src="activated-storage-integration.png" alt="Activated Storage Integration screen" >}}

{{< /tabs/tab >}}

{{< tabs/tab "CLI" >}}

To disable the integration, delete the package association, or the default association:

```bash
# List default associations
$ ttn-lw-cli applications packages default-associations list "app1"
{
  "defaults": [
    {
      "ids": {
        "application_ids": {
          "application_id": "app1"
        },
        "f_port": 100
      },
      "created_at": "2020-08-24T21:09:44.649890166Z",
      "updated_at": "2020-08-24T21:09:44.649890166Z",
      "package_name": "storage-integration"
    }
  ]
}
```

```bash
$ ttn-lw-cli applications packages default-associations delete "app1" 100
```

{{< /tabs/tab >}}

{{< /tabs/container >}}

## Disable for an End Device

```bash
# List default associations
$ ttn-lw-cli applications packages associations list "app1" "dev1"
{
  "associations": [
    {
      "ids": {
        "end_device_ids": {
          "device_id": "dev1",
          "application_ids": {
            "application_id": "app1"
          }
        },
        "f_port": 100
      },
      "created_at": "2020-08-24T21:09:44.649890166Z",
      "updated_at": "2020-08-24T21:09:44.649890166Z",
      "package_name": "storage-integration"
    }
  ]
}
```
```bash
$ ttn-lw-cli applications packages associations delete "app1" "dev1" 100
```