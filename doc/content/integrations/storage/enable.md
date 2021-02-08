---
title: Enable
description: ""
summary: Enable Storage Integration for applications and end-devices.
weight: 20
---

The Storage Integration is implemented as an [Application Package]({{< ref "/reference/application-packages" >}}). In order to enable it for an application (or a single end device), you have to create a package association.

{{< cli-only >}}

{{< note >}} The `f_port` for the default association and association is set to `100`. This value is irrelevant. **The storage integration will receive and store all uplink messages, regardless of `f_port`**. The `f_port` value is only needed because of the way application packages work with {{% tts %}}. {{</ note >}}


## Enable for an Application

Set up a default association between the desired application and the `storage-integration` package.

```bash
$ ttn-lw-cli applications packages default-associations set "app1" 100 --package-name storage-integration
```

{{< warning >}} **Do not configure more than one default association for the same application**, since that will lead to storing duplicate messages in the persistent storage. {{</ warning >}}

## Enable for an End Device

Set up an association between the desired end device and the `storage-integration` package.

```bash
$ ttn-lw-cli applications packages associations set "app1" "dev1" 100 --package-name storage-integration
```

{{< warning >}} **Do not configure multiple associations for the same end device**, since that will lead to storing duplicate uplinks in the persistent storage. {{</ warning >}}