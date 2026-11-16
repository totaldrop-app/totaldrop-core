# Architecture Decision Records

Every binding architectural, cryptographic, packaging, and governance choice in
TotalDrop is recorded here in English ([0019](0019-english-by-default.md)).

| Record | Summary | Status |
| --- | --- | --- |
| [0001](0001-one-repository.md) | One repository, a folder per platform | Superseded by [0020](0020-modular-subplatform-matrix.md) |
| [0002](0002-protocol-v0.md) | Protocol v0 (CPace + Noise XXpsk3 + ML-KEM-768 + QUIC STREAM) | Accepted |
| [0003](0003-cloudflare-infrastructure.md) | Site, rendezvous, and relay on Cloudflare Workers & Pages | Accepted |
| [0004](0004-mullvad-style-accounts.md) | An account is only a random number | Superseded by [0013](0013-ghost-ring-accounts.md) |
| [0005](0005-donations.md) | Revenue comes solely from transparent public donations | Accepted |
| [0006](0006-linux-qt.md) | The Linux app uses Qt 6 and QML with 100% desktop theme fidelity | Accepted |
| [0007](0007-working-process.md) | Issue-first workflow, independent review, and CI-built releases | Accepted |
| [0008](0008-languages-and-regions.md) | 35 languages and regional settings from a single ICU/CLDR ARB source | Accepted |
| [0009](0009-ios-macos.md) | iOS and macOS with free CI; Apple Developer signing only for release | Accepted |
| [0010](0010-android-background-transfer.md) | Android background transfers run as user-initiated data-transfer jobs | Accepted |
| [0011](0011-android-material-3-expressive.md) | Android adopts Material 3 Expressive incrementally | Accepted |
| [0012](0012-name-and-mark.md) | Open-source code; TotalDrop name and Köşe mark reserved for official builds | Accepted |
| [0013](0013-ghost-ring-accounts.md) | Zero server account state: the post-quantum Ghost Ring | Accepted |
| [0014](0014-steam-deck.md) | Steam Deck, Steam Machine, and Steam Frame supported via Linux Flatpak | Accepted |
| [0015](0015-package-managers.md) | Package manager channels start from reproducible CI-built binaries | Accepted |
| [0016](0016-windows-microsoft-store.md) | Windows app built with WinUI 3 over Rust bridge (`msix`, `winget`, `zip`) | Accepted |
| [0017](0017-personal-sponsors-page.md) | Interim donation collection via project lead's Sponsors & Buy Me a Coffee | Accepted |
| [0018](0018-connectivity-roadmap.md) | Custom QUIC/relay stack retained; IPv6, UPnP/PCP, and LAN added incrementally | Accepted |
| [0019](0019-english-by-default.md) | All repositories, issues, reviews, and documents are written in English | Accepted |
| [0020](0020-modular-subplatform-matrix.md) | 11 modular repositories (`53` active sub-platform × CPU units + `1` reserved repository) | Accepted |

To propose a new decision, open an English pull request adding `NNNN-short-name.md`
and append a row to the table above.
