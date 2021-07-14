---
title: "Troubleshooting AWS ECS Deployment"
description: ""
weight: 7
---

<!--
TODO: https://github.com/TheThingsNetwork/lorawan-stack/issues/2714
Move to generic getting started guide once ready.
-->

This section contains information to troubleshoot {{% tts %}} deployment.

<!--more-->


### TTS no longer accepting connections from UDP gateways after upgradation to latest version

Cross check the below operations

  - Before the version update, complete the database migration.
  
  - If `default` is set to the `DefaultTenantId` in the configuration file, unset the `DefaultTenantId` parameter
  
  ```
  tenancy:
        default-id: 'default'
  ```
  Unset the `DefaultTenantId` as below
  
  ```
  tenancy:
        default-id: ''

  ```

Apply the configurations and restart the necessary services.



## Professional Support

Additional paid support for this deployment is offered by The Things Industries. You can contact us either by mailing us at `support@thethingsindustries.com` or by visiting [our support page](https://www.thethingsindustries.com/stack/aws/support).
