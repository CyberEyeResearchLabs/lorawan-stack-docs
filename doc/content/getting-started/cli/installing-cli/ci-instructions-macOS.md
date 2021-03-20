---
title: "Installing the CLI in macOS"
description: ""
weight: 3
---

This section contains instructions for installing the command-line interface in macOS.

<!--more-->

### Package managers (recommended)

#### macOS

```bash
$ brew install TheThingsNetwork/lorawan-stack/ttn-lw-stack
```

{{< note >}} When installing with `brew`, auto completion is enabled automatically. {{</ note >}}

To upgrade the CLI if it is already installed, use:

```bash
$ brew upgrade TheThingsNetwork/lorawan-stack/ttn-lw-stack
```

### Binaries

You can download [pre-built binaries](https://github.com/TheThingsNetwork/lorawan-stack/releases) for your operating system and processor architecture.

## Configuration

### Generate configuration file

For a standard deployment on `thethings.example.com`, all you need is:

```bash
$ ttn-lw-cli use thethings.example.com [--fetch-ca] [--user] [--overwrite]
```

This will generate and save the required CLI config file. By default, the file is saved on the current directory, use the `--user` to save it under the user config directory.

If the deployment is using a CA that is not already trusted by your system, use the `--fetch-ca` flag to also connect to the server and retrieve the CA required for establishing secure communication.

{{< note >}} If the file exists already, it is not overwritten and an error is printed instead. You can use `--overwrite` to overwrite the existing configuration file. {{</ note >}}

{{< note >}} You can also use the `--grpc-port` and `--oauth-server-address` flags to override the default values for the gRPC port and the OAuth server address. These are not needed for standard deployments. {{</ note >}}

{{< note >}} For the Cloud-Hosted Deployments in clusters other than `eu1`, please follow the steps in the below section. {{</ note >}}

### Manually creating configuration file

Alternatively, you can create a file named `.ttn-lw-cli.yml` and paste the following contents:

**Command:**
```bash
$ touch .ttn-lw-cli.yml
```

**Contents:**

```yaml
oauth-server-address: 'https://thethings.example.com/oauth'

identity-server-grpc-address: 'thethings.example.com:8884'
gateway-server-grpc-address: 'thethings.example.com:8884'
network-server-grpc-address: 'thethings.example.com:8884'
application-server-grpc-address: 'thethings.example.com:8884'
join-server-grpc-address: 'thethings.example.com:8884'
device-claiming-server-grpc-address: 'thethings.example.com:8884'
device-template-converter-grpc-address: 'thethings.example.com:8884'
qr-code-generator-grpc-address: 'thethings.example.com:8884'
```

If you are using an `https` port other than `443`, you need to specify that port, e.g.:

```yaml
oauth-server-address: 'https://thethings.example:8885/oauth'
```

If your deployment uses a custom certificate authority, you'll need to add:

```yaml
ca: /path/to/ca.pem
```

For advanced options, see the [Configuration Reference]({{< ref "/reference/configuration/cli" >}}).

### Configuring CLI

The command-line needs to be configured to connect to your deployment on `thethings.example.com`. You have multiple options to make the configuration file available to the CLI:

1. Environment: `export TTN_LW_CONFIG=/path/to/ttn-lw-cli.yml`
2. Command-line flag: `-c /path/to/ttn-lw-cli.yml`
3. Save as `.ttn-lw-cli.yml` in `$XDG_CONFIG_HOME`, your home directory, or the working directory.

## Auto Completion

Auto completion allows the shell to [automatically fill in commands](https://en.wikipedia.org/wiki/Command-line_completion) after you type the first few letters. It is completely optional but can save you time entering commands.

Use `ttn-lw-cli complete` to generate an auto completion script for the `ttn-lw-cli` command. `bash`, `zsh`, `fish` and `powershell` shells are supported:

```bash
$ ttn-lw-cli complete --shell bash --executable ttn-lw-cli > ttn-lw-cli-autocomplete
```

Source the file to enable auto completion:

```bash
$ . ./ttn-lw-cli-autocomplete
```

Alternatively, put in a default directory so that it is loaded automatically (This directory depends on your Operating System and your shell).

For `bash`, this directory is typically `/etc/bash_completion.d/`:

```bash
$ sudo cp ./ttn-lw-cli-autocomplete /etc/bash_completion.d/
```
