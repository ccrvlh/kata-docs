---
sidebar_position: 5
---

# Storage limitations

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
