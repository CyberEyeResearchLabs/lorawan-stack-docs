---
title: "Installing the CLI"
description: ""
weight: 1
---

This section contains instructions for installing the command-line interface.

<!--more-->
{{< tabs/container "Linux" "macOS" "Windows" >}}

<!-- _______________________________________________________________Linux________________________________________________________________________ -->
{{< tabs/tab "Linux" >}}


<!--more-->

### Package managers (recommended)

#### Linux

Open the `terminal` in Linux and run the below commands to install the package manager.

```bash
$ sudo snap install ttn-lw-stack
$ sudo snap alias ttn-lw-stack.ttn-lw-cli ttn-lw-cli
```

[Adding image of the package manager installation in progress]

{{< note >}} When installing with `snap`, auto-completion is enabled automatically. {{</ note >}}

{{< /tabs/tab >}}
<!-- ____________________________________________________________END________________________________________________________________________ -->


<!-- ____________________________________________________________macOS________________________________________________________________________ -->

{{< tabs/tab "macOS" >}}

<!--more-->

### Package managers (recommended)

#### macOS

```bash
$ brew install TheThingsNetwork/lorawan-stack/ttn-lw-stack
```

{{< note >}} When installing with `brew`, auto-completion is enabled automatically. {{</ note >}}


{{< /tabs/tab >}}
<!-- ____________________________________________________________END________________________________________________________________________ -->


<!-- ____________________________________________________________Windows________________________________________________________________________ -->

{{< tabs/tab "Windows" >}}

### Package managers (recommended)

You can download [pre-built binaries](https://github.com/TheThingsNetwork/lorawan-stack/releases) for your operating system and processor architecture.

{{< note >}} Make sure to download the latest binaries with every new release of the stack. To know your windows system architecture, run the below command in the windows command prompt `$ echo %PROCESSOR_ARCHITECTURE%` {{</ note >}}

Extract the downloaded `.zip` file and in the extracted folder you can find `ttn-lw-cli.exe` file.


{{< /tabs/tab >}}
<!-- ____________________________________________________________END________________________________________________________________________ -->

## Generate configuration file

For a standard deployment on `thethings.example.com`, all you need is:

<!-- _______________________________________________________________Linux________________________________________________________________________ -->

{{< tabs/tab "Linux" >}}


```bash
$ ttn-lw-cli use thethings.example.com [--fetch-ca] [--user] [--overwrite]
```

{{< /tabs/tab >}}
<!-- ____________________________________________________________END________________________________________________________________________ -->


<!-- ____________________________________________________________macOS________________________________________________________________________ -->

{{< tabs/tab "macOS" >}}

```bash
$ ttn-lw-cli use thethings.example.com [--fetch-ca] [--user] [--overwrite]
```

{{< /tabs/tab >}}
<!-- ____________________________________________________________END________________________________________________________________________ -->


<!-- ____________________________________________________________Windows________________________________________________________________________ -->

{{< tabs/tab "Windows" >}}

```bash
$ ttn-lw-cli.exe use thethings.example.com [--fetch-ca] [--user] [--overwrite]
```

{{< /tabs/tab >}}
<!-- ____________________________________________________________END________________________________________________________________________ -->

This will generate and save the required CLI config file. By default, the file is saved on the current directory, use the `--user` to save it under the user config directory.

If the deployment is using a CA that is not already trusted by your system, use the `--fetch-ca` flag to also connect to the server and retrieve the CA required for establishing secure communication.

{{< note >}} If the file exists already, it is not overwritten and an error is printed instead. You can use `--overwrite` to overwrite the existing configuration file. {{</ note >}}

{{< note >}} You can also use the `--grpc-port` and `--oauth-server-address` flags to override the default values for the gRPC port and the OAuth server address. These are not needed for standard deployments. {{</ note >}}

{{< note >}} For the Cloud-Hosted Deployments in clusters other than `eu1`, please follow the steps in the below section. {{</ note >}}


<!-- _______________________________________________________________Linux________________________________________________________________________ -->

{{< tabs/tab "Linux" >}}

Create a file named `.ttn-lw-cli.yml` by running the below command in `terminal`.

```bash
$ touch .ttn-lw-cli.yml
```

{{< /tabs/tab >}}
<!-- ____________________________________________________________END________________________________________________________________________ -->


<!-- ____________________________________________________________macOS________________________________________________________________________ -->

{{< tabs/tab "macOS" >}}

Create a file named `.ttn-lw-cli.yml` by running the below command in `terminal`.

```bash
$ touch .ttn-lw-cli.yml
```

{{< /tabs/tab >}}
<!-- ____________________________________________________________END________________________________________________________________________ -->


<!-- ____________________________________________________________Windows________________________________________________________________________ -->

{{< tabs/tab "Windows" >}}

Navigate to the working directory and create a file named `.ttn-lw-cli.yml` in the extracted folder by executing the below command.

```bash
$ type nul > .ttn-lw-cli.yml
``` 

{{< /tabs/tab >}}
<!-- ____________________________________________________________END________________________________________________________________________ -->


Alternatively, you can create a file named `.ttn-lw-cli.yml` and paste the following contents:

{{< note >}} For the Cloud-Hosted Deployments, navigate to the [Cloud Addresses](https://enterprise.thethingsstack.io/getting-started/cloud-hosted/addresses/) and enter the `tenant-id` and choose the `cluster` for which you want to generate the content of the CLI configuration file. After filling in those details, copy the contents in the `Command-line Interface` section on the same page and paste them into the `.ttn-lw-cli.yml` file created earlier. {{</ note >}}

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



<!-- _______________________________________________________________Linux________________________________________________________________________ -->

{{< tabs/tab "Linux" >}}

## Configuration

The command-line needs to be configured to connect to your deployment on `thethings.example.com`. You have multiple options to make the configuration file available to the CLI:

1. Environment: `export TTN_LW_CONFIG=/path/to/.ttn-lw-cli.yml`
2. Command-line flag: `-c /path/to/.ttn-lw-cli.yml`
3. Save as `.ttn-lw-cli.yml` in `$XDG_CONFIG_HOME`, your home directory, or the working directory.

{{< warning >}} When using the snap packages, `~/.ttn-lw-cli.yml` will fail with permission errors. Choose a different path. {{</ warning >}}

## Auto Completion

Use `ttn-lw-cli complete` to generate an auto-completion script for the `ttn-lw-cli` command. `bash`, `zsh`, `fish` and `powershell` shells are supported:

```bash
$ ttn-lw-cli complete --shell bash --executable ttn-lw-cli > ttn-lw-cli-autocomplete
```

Source the file to enable auto-completion:

```bash
$ . ./ttn-lw-cli-autocomplete
```

Alternatively, put in a default directory so that it is loaded automatically (This directory depends on your Operating System and your shell).

For `bash`, this directory is typically `/etc/bash_completion.d/`:

```bash
$ sudo cp ./ttn-lw-cli-autocomplete /etc/bash_completion.d/
```

{{< /tabs/tab >}}
<!-- ____________________________________________________________END________________________________________________________________________ -->


<!-- ____________________________________________________________macOS________________________________________________________________________ -->

{{< tabs/tab "macOS" >}}

## Configuration

The command-line needs to be configured to connect to your deployment on `thethings.example.com`. You have multiple options to make the configuration file available to the CLI:

1. Environment: `export TTN_LW_CONFIG=/path/to/.ttn-lw-cli.yml`
2. Command-line flag: `-c /path/to/.ttn-lw-cli.yml`
3. Save as `.ttn-lw-cli.yml` in `$XDG_CONFIG_HOME`, your home directory, or the working directory.

{{< warning >}} When using the snap packages, `~/.ttn-lw-cli.yml` will fail with permission errors. Choose a different path. {{</ warning >}}

## Auto Completion

Use `ttn-lw-cli complete` to generate an auto-completion script for the `ttn-lw-cli` command. `bash`, `zsh`, `fish` and `powershell` shells are supported:

```bash
$ ttn-lw-cli complete --shell bash --executable ttn-lw-cli > ttn-lw-cli-autocomplete
```

Source the file to enable auto-completion:

```bash
$ . ./ttn-lw-cli-autocomplete
```

Alternatively, put in a default directory so that it is loaded automatically (This directory depends on your Operating System and your shell).

For `bash`, this directory is typically `/etc/bash_completion.d/`:

```bash
$ sudo cp ./ttn-lw-cli-autocomplete /etc/bash_completion.d/
```

{{< /tabs/tab >}}
<!-- ____________________________________________________________END________________________________________________________________________ -->


<!-- ____________________________________________________________Windows________________________________________________________________________ -->

{{< tabs/tab "Windows" >}}

## Configuration

The command-line needs to be configured to connect to your deployment on `thethings.example.com`. Run the below command to make the configuration file available to the CLI:

Environment: `set TTN_LW_CONFIG=/path/to/.ttn-lw-cli.yml`

## Auto Completion

Use `ttn-lw-cli complete` to generate an auto-completion script for the `ttn-lw-cli` command. `bash`, `zsh`, `fish` and `powershell` shells are supported:

```bash
$ ttn-lw-cli.exe complete --shell powershell --executable ttn-lw-cli.exe > ttn-lw-cli-autocomplete.ps1
```

Source the file to enable auto-completion:

```bash
$ . ./ttn-lw-cli-autocomplete.ps1
```

Alternatively, put in a default directory so that it is loaded automatically (This directory depends on your Operating System and your shell).


{{< /tabs/tab >}}
<!-- ____________________________________________________________END________________________________________________________________________ -->

---

{{< note >}} For Cloud-Hosted Deployments, the oauth-server-address and identity-server-grpc-address will be in the `eu1` cluster even if you select the `nam1`/`au1` clusters. Also, the command-line needs to be configured to connect to your deployment on `<tenant-id>.eu1.cloud.thethings.industries`. For configuration run the below command in the terminal. Setting Environment - Set the CLI path to `ttn-lw-cli` directory and execute


```bash
$ export TTN_LW_CONFIG=~/path/to/.ttn-lw-cli.yml 
```
{{</ note >}}
