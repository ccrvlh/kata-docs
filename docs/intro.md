---
sidebar_position: 1
---

# Introduction

This documentation has the objective of being a simple way to get started with Kata.

## What is Kata?

Kata Containers is an open source project and community working to build a standard implementation of lightweight Virtual Machines (VMs) that feel and perform like containers, but provide the workload isolation and security advantages of VMs.

## Use Cases

You might want to use Kata for any number of use cases, but the most prominent one is related to security.
As much as containers went a long way when it comes to isolation, the shared host kernel will always
pose a thread. When running when untrusted code, you will definitely want the isolation of a VM.

Kata's objective is to make the usage of VMs as similar to containers as possible, and it focus on the internals: the runtime.
Kata is a runtime, that can seamlessly plug into the containers ecosystem.

## Requirements

Although specific requirements will be discussed further ahead, it is important to keep in mind that Kata builds on top
of virtualization plataforms, specially KVM. So you will need access to a server that has that enabled.
Usually that is not case with regular VPS from the biggest cloud providers, since it would required nested virtualization.

If you are not running on Bare Metal, or is just trying out Kata, both Google Cloud and DigitalOcean allow for nested virtualization.

## License

Kata is an open source project and it's code is licensed under the Apache 2.0 license.
