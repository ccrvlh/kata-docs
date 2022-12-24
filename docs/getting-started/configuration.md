---
sidebar_position: 3
---

# Configuration

The runtime uses a TOML format configuration file called `configuration.toml`.
The file is divided into sections for settings related to various
parts of the system including the runtime itself, the [agent](../agent) and
the [hypervisor](#hypervisor-specific-configuration).

Each option has a comment explaining its use.

> **Note:**
>
> The initial values in the configuration file provide a good default configuration.
> You may need to modify this file to optimise or tailor your system, or if you have
> specific requirements.

### Configuration file location

#### Runtime configuration file location

The shimv2 runtime looks for its configuration in the following places (in order):

- The `io.data containers.config.config_path` annotation specified
  in the OCI configuration file (`config.json` file) used to create the pod sandbox.

- The containerd
  [shimv2](/docs/design/architecture/README.md#shim-v2-architecture)
  options passed to the runtime.

- The value of the `KATA_CONF_FILE` environment variable.

- The [default configuration paths](#stateless-systems).

#### Utility program configuration file location

The `kata-runtime` utility program looks for its configuration in the
following locations (in order):

- The path specified by the `--config` command-line option.

- The value of the `KATA_CONF_FILE` environment variable.

- The [default configuration paths](#stateless-systems).

> **Note:** For both binaries, the first path that exists will be used.

#### Drop-in configuration file fragments

To enable changing configuration without changing the configuration file
itself, drop-in configuration file fragments are supported. Once a
configuration file is parsed, if there is a subdirectory called `config.d` in
the same directory as the configuration file its contents will be loaded
in alphabetical order and each item will be parsed as a config file. Settings
loaded from these configuration file fragments override settings loaded from
the main configuration file and earlier fragments. Users are encouraged to use
familiar naming conventions to order the fragments (e.g. `config.d/10-this`,
`config.d/20-that` etc.).

Non-existent or empty `config.d` directory is not an error (in other words, not
using configuration file fragments is fine). On the other hand, if fragments
are used, they must be valid - any errors while parsing fragments (unreadable
fragment files, contents not valid TOML) are treated the same as errors
while parsing the main configuration file. A `config.d` subdirectory affects
only the `configuration.toml` _in the same directory_. For fragments in
`config.d` to be parsed, there has to be a valid main configuration file _in
that location_ (it can be empty though).

### Hypervisor specific configuration

Kata Containers supports multiple hypervisors so your `configuration.toml`
configuration file may be a symbolic link to a hypervisor-specific
configuration file. See
[the hypervisors document](../../docs/hypervisors.md) for further details.

### Stateless systems

Since the runtime supports a
[stateless system](https://clearlinux.org/about),
it checks for this configuration file in multiple locations, two of which are
built in to the runtime. The default location is
`/usr/share/defaults/kata-containers/configuration.toml` for a standard
system. However, if `/etc/kata-containers/configuration.toml` exists, this
takes priority.

The below command lists the full paths to the configuration files that the
runtime attempts to load. The first path that exists will be used:

```bash
$ kata-runtime --show-default-config-paths
```

The runtime will log the full path to the configuration file it is using. See
the [logging](#logging) section for further details.

To see details of your systems runtime environment (including the location of
the configuration file being used), run:

```bash
$ kata-runtime env
```
