---
sidebar_position: 3
title: "Network"
---

# Network

### Networking

#### Host network

Host network (`nerdctl/docker run --net=host`or [Kubernetes `HostNetwork`](https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/pod-v1/#hosts-namespaces)) is not supported.
It is not possible to directly access the host networking configuration
from within the VM.

The `--net=host` option can still be used with `runc` containers and
inter-mixed with running Kata Containers, thus enabling use of `--net=host`
when necessary.

It should be noted, currently passing the `--net=host` option into a
Kata Container may result in the Kata Container networking setup
modifying, re-configuring and therefore possibly breaking the host
networking setup. Do not use `--net=host` with Kata Containers.

#### Support for joining an existing VM network

Docker supports the ability for containers to join another containers
namespace with the `docker run --net=containers` syntax. This allows
multiple containers to share a common network namespace and the network
interfaces placed in the network namespace. Kata Containers does not
support network namespace sharing. If a Kata Container is setup to
share the network namespace of a `runc` container, the runtime
effectively takes over all the network interfaces assigned to the
namespace and binds them to the VM. Consequently, the `runc` container loses
its network connectivity.

#### docker run --link

The runtime does not support the `docker run --link` command. This
command is now deprecated by docker and we have no intention of adding support.
Equivalent functionality can be achieved with the newer docker networking commands.

See more documentation at
[docs.docker.com](https://docs.docker.com/network/links/).

### Resource management

Due to the way VMs differ in their CPU and memory allocation, and sharing
across the host system, the implementation of an equivalent method for
these commands is potentially challenging.

See issue https://github.com/clearcontainers/runtime/issues/341 and [the constraints challenge](#the-constraints-challenge) for more information.

For CPUs resource management see
[CPU constraints](design/vcpu-handling.md).

## Architectural limitations

This section lists items that might not be fixed due to fundamental
architectural differences between "soft containers" (i.e. traditional Linux\*
containers) and those based on VMs.

### Storage limitations

#### Kubernetes `volumeMounts.subPaths`

Kubernetes `volumeMount.subPath` is not supported by Kata Containers at the
moment.

See [this issue](https://github.com/kata-containers/runtime/issues/2812) for more details.
[Another issue](https://github.com/kata-containers/kata-containers/issues/1728) focuses on the case of `emptyDir`.

### Host resource sharing

#### Privileged containers

Privileged support in Kata is essentially different from `runc` containers.
The container runs with elevated capabilities within the guest and is granted
access to guest devices instead of the host devices.
This is also true with using `securityContext privileged=true` with Kubernetes.

The container may also be granted full access to a subset of host devices
(https://github.com/kata-containers/runtime/issues/1568).

See [Privileged Kata Containers](how-to/privileged.md) for how to configure some of this behavior.

## Appendices

### The constraints challenge

Applying resource constraints such as cgroup, CPU, memory, and storage to a workload is not always straightforward with a VM based system. A Kata Container runs in an isolated environment inside a virtual machine. This, coupled with the architecture of Kata Containers, offers many more possibilities than are available to traditional Linux containers due to the various layers and contexts.

In some cases it might be necessary to apply the constraints to multiple levels. In other cases, the hardware isolated VM provides equivalent functionality to the the requested constraint.

The following examples outline some of the various areas constraints can be applied:

- Inside the VM

  Constrain the guest kernel. This can be achieved by passing particular values through the kernel command line used to boot the guest kernel. Alternatively, sysctl values can be applied at early boot.

- Inside the container

  Constrain the container created inside the VM.

- Outside the VM:

  - Constrain the hypervisor process by applying host-level constraints.

  - Constrain all processes running inside the hypervisor.

    This can be achieved by specifying particular hypervisor configuration options.

Note that in some circumstances it might be necessary to apply particular constraints
to more than one of the previous areas to achieve the desired level of isolation and resource control.
