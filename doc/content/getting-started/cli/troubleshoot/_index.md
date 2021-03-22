---
title: "Troubleshooting CLI"
description: ""
weight: 3
---

This section provides troubleshooting tips on the common errors when using the command-line interface.

<!--more-->

## Unable to login to CLI. What do I do?

Improper [Configuration]({{< ref "getting-started/cli/installing-cli#configuration" >}}) of the CLI environment, i.e., `ttn-lw-cli.yml` of your deployment will redirect to the `localhost` URL.

**e.g:** Successful configuration will redirect to your deployment as shown below:
	
```
INFO Opening your browser on https://thethings.example.com/oauth/authorize?client_id=cli&redirect_uri=local-callback&response_type=code
WARN Could not open your browser, you'll have to go there yourself error=fork/exec /usr/bin/xdg-open: permission denied
INFO After logging in and authorizing the CLI, we'll get an access token for future commands.
INFO Waiting for your authorization...
```

{{< note >}} If the `ttn-lw-cli` has been installed via a `snap` package in the `Linux` operating system, the `ttn-lw-cli` login command will not automatically redirect the browser for the `OAuth token` authentication. Due to the restriction of permissions with the `snap` package. Hence, you need to click on the URL from the terminal output to get the login `OAuth token`.{{</ note >}}

## Insufficient rights for the user

This error had seen when a user does not have sufficient rights to perform the operations.

## Value does not match the regex pattern 

This error is seen when the value of `ID` fields(Device ID/ Gateway ID) does not follow the naming convention of {{% tts %}} during the CLI registration. Usually, the naming convention of the `ID` field must contain only lowercase letters, numbers, and dashes (-). 

The following regular expression is used to validate IDs:

`(^[a-z0-9](?:[-]?[a-z0-9]){2,}$)`

