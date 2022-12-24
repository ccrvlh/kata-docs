---
sidebar_position: 1
---

# Overview

A [Kata Container](https://github.com/kata-containers) utilizes a Virtual Machine (VM) to enhance security and
isolation of container workloads. As a result, the system has a number of differences
and limitations when compared with the default [Docker\*](https://www.docker.com/) runtime,
[`runc`](https://github.com/opencontainers/runc).

Some of these limitations have potential solutions, whereas others exist
due to fundamental architectural differences generally related to the
use of VMs.

The [Kata Container runtime](../src/runtime)
launches each container within its own hardware isolated VM, and each VM has
its own kernel. Due to this higher degree of isolation, certain container
capabilities cannot be supported or are implicitly enabled through the VM.

## Definition of a limitation

The [Open Container Initiative](https://www.opencontainers.org/)
[Runtime Specification](https://github.com/opencontainers/runtime-spec) ("OCI spec")
defines the minimum specifications a runtime must support to interoperate with
container managers such as Docker. If a runtime does not support some aspect
of the OCI spec, it is by definition a limitation.

However, the OCI runtime reference implementation (`runc`) does not perfectly
align with the OCI spec itself.

Further, since the default OCI runtime used by Docker is `runc`, Docker
expects runtimes to behave as `runc` does. This implies that another form of
limitation arises if the behavior of a runtime implementation does not align
with that of `runc`. Having two standards complicates the challenge of
supporting a Docker environment since a runtime must support the official OCI
spec and the non-standard extensions provided by `runc`.

## Scope

Each known limitation is captured in a separate GitHub issue that contains
detailed information about the issue. These issues are tagged with the
`limitation` label. This document is a curated summary of important known
limitations and provides links to the relevant GitHub issues.

The following link shows the latest list of limitations:

- https://github.com/pulls?utf8=%E2%9C%93&q=is%3Aopen+label%3Alimitation+org%3Akata-containers

## Contributing

If you would like to work on resolving a limitation, please refer to the
[contributors guide](https://github.com/kata-containers/community/blob/main/CONTRIBUTING.md).
If you wish to raise an issue for a new limitation, either
[raise an issue directly on the runtime](https://github.com/kata-containers/kata-containers/issues/new)
or see the
[project table of contents](https://github.com/kata-containers/kata-containers)
for advice on which repository to raise the issue against.

## Pending items

This section lists items that might be possible to fix.
