---
title: Disable
description: ""
summary: Disable Storage Integration for applications and end-devices.
weight: 30
---

The Storage Integration is implemented as an [Application Package]({{< ref "/reference/application-packages" >}}). In order to disable it, you have to delete a default association for an application and an association for an end-device.

{{< cli-only >}}

## Disable for an Application

You can list down the default associations of an application using the below command:

```bash
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

Out of the listed default associations, you can choose the ones to delete by its `f_port` number. Use the below command to delete the default association:

```bash
$ ttn-lw-cli applications packages default-associations delete "app1" 100
```

## Disable for an End Device

You can list down the associations of an end-device using the below command:
```bash
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

Out of the listed associations, you can choose the ones to delete by its `f_port` number. Use the below command to delete the association:

```bash
$ ttn-lw-cli applications packages associations delete "app1" "dev1" 100
```
