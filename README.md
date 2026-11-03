<!--
SPDX-FileCopyrightText: 2026 roolrz
SPDX-License-Identifier: Apache-2.0
-->

# vmm

VM management and virtual-console client.

Uses `lib-vm-policy` requests and `lib-service` VM channels. The VM manager owns
lifecycle policy; the client requests operations, waits for selected outcomes and
attaches to delegated console channels.

See the [implementation entry](src/main.rs) and [component declaration](component.json)
for the public interfaces, build dependencies and delivered artifacts.

## Usage

In a Native session with the required capabilities:

```sh
vmm list
vmm --help
```

## Boundaries

A request deadline does not cancel an already accepted lifecycle operation. Inspect
status before retrying. Console sessions use Ctrl-] for their control menu and restore
terminal settings when the session ends.

## Build and test

Use this checkout inside the [repo-managed workspace](https://github.com/HypeR-Proj/HypeR).
From this repository directory:

```sh
make
make test
```

An absolute `OUT=/path/to/out` selects a shared output directory. The module
entry delegates to build/system, which prepares the installed SDK and declared
dependencies. Native binaries require HypeR; host module checks cover the tests
selected by component.json. A standalone clone does not contain the workspace’s
other source repositories or Native SDK.
