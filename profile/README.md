<div align="center">

# NodeLink

**Send a file. Share a code.**

Decentralized, anonymous, terminal-only file-transfer infrastructure — written in Rust.

[![License: AGPL-3.0](https://img.shields.io/badge/license-AGPL--3.0-d8492a.svg)](./LICENSE)
![Status: alpha](https://img.shields.io/badge/status-alpha-c9871f.svg)
[![Made with Rust](https://img.shields.io/badge/made%20with-Rust-000000.svg?logo=rust)](https://www.rust-lang.org/)
[![Protocol: QUIC / HTTP3](https://img.shields.io/badge/protocol-QUIC%20%2F%20HTTP3-2f9e6b.svg)](#how-it-works)

[Website](https://nodelinkapp.xyz) ·
[Network map](https://map.nodelinkapp.xyz) ·
[Status](https://status.nodelinkapp.xyz) ·
[Discussions](https://github.com/NodeLink-Project/nodelink/discussions)

</div>

---

## What is NodeLink?

NodeLink is a free, anonymous way to move files of **any size** across a decentralized network, entirely from your terminal. You send a file, you get back a short recovery code, and anyone with that code can retrieve the file — no account, no web upload form, no size limit, no inspection of what you transfer.

Files are split into segments that are distributed across nodes worldwide and reassembled on retrieval. There is deliberately **no browser-based transfer**: everything goes through the `nl` client over QUIC, which keeps the transfer path narrow and predictable.

```
$ nl send report.zip
  ✔ segmented · distributed · ready
  recovery code:  7F3K-9Q2X-NL

$ nl get 7F3K-9Q2X-NL
  ✔ located · reassembled · saved to ./report.zip
```

<!--
GitHub can't run the asciinema player inline, so the pattern above shows the
SVG poster and links to the player on asciinema.org. To publish your own demo:

  1. asciinema rec nodelink-demo.cast     # then run `nl send` and `nl get`, keep it ~15-20s
  2. asciinema upload nodelink-demo.cast  # prints an https://asciinema.org/a/<id> URL
  3. replace the two REPLACE_WITH_CAST_ID above with that numeric <id>

Prefer self-hosting? Use the asciinema-player JS/CSS on your own page
(e.g. nodelinkapp.xyz) and link to it from here instead.
-->


---

## Why NodeLink

| | NodeLink | WeTransfer, Drive & similar |
|---|:---:|:---:|
| Size limit | none | capped |
| Anonymity | no account, no tracking | account / identity required |
| Architecture | decentralized | centralized |
| Content inspection | none | scanned |
| Price | free | freemium / paid |
| Access | terminal (`nl`) | web / app |

---

## How it works

1. **Segment** — the file is split locally into multiple segments.
2. **Distribute** — segments are spread across nodes in the network.
3. **Code** — you receive a compact recovery code (e.g. `7F3K-9Q2X-NL`).
4. **Retrieve** — anyone with the code fetches the segments and reassembles the file.

The transport layer is **QUIC over UDP (HTTP/3)**, chosen for fast connection setup, multiplexed segment streams, and resilience on lossy networks. The network itself is organized per region into a **Node** (routing / coordination) and one or more **Clusters** (storage / relay). You can watch the live layout on the [network map](https://map.nodelinkapp.xyz).

---

## Contributing

Contributions are very welcome, especially from Rustaceans. Good ways to start:

- Browse issues tagged [`good first issue`](https://github.com/NodeLink-Project/nodelink/labels/good%20first%20issue)
- Open a thread in [Discussions](https://github.com/NodeLink-Project/nodelink/discussions) for questions, ideas or design feedback
- Report bugs via [Issues](https://github.com/NodeLink-Project/nodelink/issues)

Please keep pull requests focused, and open a discussion first for anything large so we can align on direction.

---

## License

NodeLink is released under the **GNU Affero General Public License v3.0** (AGPL-3.0). See [LICENSE](./LICENSE).

The AGPL's network clause means that if you run a modified version of NodeLink as a network service, you must make your modified source available to its users. The **NodeLink name and logo are not covered by this license** and are reserved.

---

## Maintainer

Built and maintained by **Sandro Soria** ([@Sandro642](https://github.com/Sandro642)).

- Organization: [github.com/NodeLink-Project](https://github.com/NodeLink-Project)
- Contact: sandro.soria@proton.me

---

<div align="center">
<sub>Written in Rust · QUIC / UDP / HTTP3 · Open source (AGPL-3.0)</sub>
<br>
<sub>⚠️ Anonymity is a technical property of the network, not a legal exemption — you remain responsible for what you transfer.</sub>
</div>

---

// NodeLink Project
// Copyright (C) 2026 Sandro Soria
// This program is free software: you can redistribute it and/or modify it
// under the terms of the GNU Affero General Public License as published by
// the Free Software Foundation, either version 3 of the License, or
// (at your option) any later version. Distributed WITHOUT ANY WARRANTY.
// See <https://www.gnu.org/licenses/> for the full license.
