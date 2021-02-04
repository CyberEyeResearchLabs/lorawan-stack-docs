---
title: "Installing the CLI in Windows"
description: ""
weight: 4
---

This section contains instructions for installing the command-line interface in Windows.

<!--more-->

### Binaries

You can download [pre-built binaries](https://github.com/TheThingsNetwork/lorawan-stack/releases) for your operating system and processor architecture.

{{< note >}} Make sure to download the latest binaries with every new release of the stack. To know your windows system architecture, run the below command in the windows command prompt {{</ note >}}

```bash
$ echo %PROCESSOR_ARCHITECTURE%
```

Extract the downloaded `.zip` file and in the extracted folder you can find `ttn-lw-cli.exe` file.

## Configuration

### Generate configuration file

For a standard deployment on `thethings.example.com`, all you need is:

```bash
$ ttn-lw-cli.exe use thethings.example.com [--fetch-ca] [--user] [--overwrite]
```

This will generate and save the required CLI config file. By default, the file is saved on the current directory, use the `--user` to save it under the user config directory.

If the deployment is using a CA that is not already trusted by your system, use the `--fetch-ca` flag to also connect to the server and retrieve the CA required for establishing secure communication.

{{< note >}} If the file exists already, it is not overwritten and an error is printed instead. You can use `--overwrite` to overwrite the existing configuration file. {{</ note >}}

{{< note >}} You can also use the `--grpc-port` and `--oauth-server-address` flags to override the default values for the gRPC port and the OAuth server address. These are not needed for standard deployments. {{</ note >}}

### Manually creating configuration file

Alternatively, you can create a file named `.ttn-lw-cli.yml` and paste the following contents:

**Command:**
```bash
$ type nul > .ttn-lw-cli.yml
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

1. Environment: `set TTN_LW_CONFIG=/path/to/ttn-lw-cli.yml`
2. Command-line flag: `-c /path/to/ttn-lw-cli.yml`
3. Save as `.ttn-lw-cli.yml` in `$XDG_CONFIG_HOME`, your home directory, or the working directory.

## Auto Completion

Auto completion allows the shell to [automatically fill in commands](https://en.wikipedia.org/wiki/Command-line_completion) after you type the first few letters. It is completely optional but can save you time entering commands.

Use `ttn-lw-cli complete` to generate an auto completion script for the `ttn-lw-cli` command. `bash`, `zsh`, `fish` and `powershell` shells are supported:

```bash
$ ttn-lw-cli.exe complete --shell powershell --executable ttn-lw-cli.exe > ttn-lw-cli-autocomplete.ps1
```

Source the file to enable auto completion:

```bash
$ . ./ttn-lw-cli-autocomplete.ps1
```
