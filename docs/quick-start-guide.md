---
sidebar_position: 2
title: "Quick Start Guide"
---

# Quick Start Guide

The easiest way to get started with Kata is with `kata-manager`.
It will install all required pieces for Kata to run and uses Docker as the container interface.

## Introduction

`kata-manager` automates the Kata Containers installation procedure documented for [these Linux distributions](README.md#supported-distributions).

> **Note**:
>
> - `kata-manager` requires `curl` and `sudo` installed on your system.
> - Full installation mode is only available for Docker container manager. For other setups, you
>   can still use `kata-manager` to [install Kata package](#install-the-kata-packages-only), and then setup your container manager manually.
> - You can run `kata-manager` in dry run mode by passing the `-n` flag. Dry run mode allows you to review the
>   commands that `kata-manager` would run, without doing any change to your system.

## Full Installation

This command does the following:

1. Installs Kata Containers packages
2. Installs Docker
3. Configure Docker to use the Kata OCI runtime by default

```bash
$ bash -c "$(curl -fsSL https://raw.githubusercontent.com/kata-containers/tests/master/cmd/kata-manager/kata-manager.sh) install-docker-system"
```

## Install the Kata packages only

Use the following command to only install Kata Containers packages.

```bash
$ bash -c "$(curl -fsSL https://raw.githubusercontent.com/kata-containers/tests/master/cmd/kata-manager/kata-manager.sh) install-packages"
```

## Further Information

For more information on what `kata-manager` can do, refer to the [`kata-manager` page](https://github.com/kata-containers/tests/blob/master/cmd/kata-manager).
