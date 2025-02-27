---
title: Dendrite
display_order: 2
categories:
  - server
description: Dendrite is a second-generation Matrix homeserver written in Go!
author: Matrix.org team
maturity: Beta
language: Go
license: Apache-2.0
repo: https://github.com/matrix-org/dendrite
---

Dendrite is a second-generation Matrix homeserver written in Go. It intends to provide an efficient, reliable and scalable alternative to Synapse:

* **Efficient:** A small memory footprint with better baseline performance than an out-of-the-box Synapse.
* **Reliable:** Implements the Matrix specification as written, using the same test suite as Synapse as well as a brand new Go test suite.
* **Scalable:** Runs at any scale, from single-user single-process monolith deployments up to massive multi-process (or even multi-machine) polylith deployments.

Find the code at [GitHub](https://github.com/matrix-org/dendrite)!

Join us in:

- **[#dendrite:matrix.org](https://matrix.to/#/#dendrite:matrix.org)** - General chat about the Dendrite project, for users and server admins alike
- **[#dendrite-dev:matrix.org](https://matrix.to/#/#dendrite-dev:matrix.org)** - The place for developers, where all Dendrite development discussion happens
- **[#dendrite-alerts:matrix.org](https://matrix.to/#/#dendrite-alerts:matrix.org)** - Release notifications and important info, highly recommended for all Dendrite server admins
