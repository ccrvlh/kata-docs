---
sidebar_position: 5
---

# Logging

For detailed information and analysis on obtaining logs for other system
components, see the documentation for the
[`kata-log-parser`](../tools/log-parser)
tool.

### Kata containerd shimv2

The Kata containerd shimv2 runtime logs through `containerd`, and its logs will be sent
to wherever the `containerd` logs are directed. However, the
shimv2 runtime also always logs to the system log (`syslog` or `journald`) using the `kata` identifier.

> **Note:** Kata logging [requires containerd debug to be enabled](../../docs/Developer-Guide.md#enabling-full-containerd-debug).

To view the `shimv2` runtime logs:

```bash
$ sudo journalctl -t kata
```
