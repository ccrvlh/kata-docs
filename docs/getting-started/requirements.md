---
sidebar_position: 1
---

# Requirements

## Prerequisites

Kata Containers requires nested virtualization or bare metal. Check
[hardware requirements](/src/runtime/README.md#hardware-requirements) to see if your system is capable of running Kata
Containers.

## Plataform Supports

Kata Containers currently runs on 64-bit systems supporting the following
technologies:

| Architecture          | Virtualization technology                    |
| --------------------- | -------------------------------------------- |
| `x86_64`, `amd64`     | [Intel](https://www.intel.com) VT-x, AMD SVM |
| `aarch64` ("`arm64`") | [ARM](https://www.arm.com) Hyp               |
| `ppc64le`             | [IBM](https://www.ibm.com) Power             |
| `s390x`               | [IBM](https://www.ibm.com) Z & LinuxONE SIE  |

## Hardware Requirements

The [Kata Containers runtime](src/runtime) provides a command to
determine if your host system is capable of running and creating a
Kata Container:

```bash
$ kata-runtime check
```

> **Notes:**
>
> - This command runs a number of checks including connecting to the
>   network to determine if a newer release of Kata Containers is
>   available on GitHub. If you do not wish this to check to run, add
>   the `--no-network-checks` option.
>
> - By default, only a brief success / failure message is printed.
>   If more details are needed, the `--verbose` flag can be used to display the
>   list of all the checks performed.
>
> - If the command is run as the `root` user additional checks are
>   run (including checking if another incompatible hypervisor is running).
>   When running as `root`, network checks are automatically disabled.
