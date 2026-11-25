<div align="center">

# The Mercury Project

### CSE499 Senior Capstone  
**Version 1.2.0-rc.1** · Academic Release Candidate

Matthew D. Barker  
Brigham Young University–Idaho

</div>

---

## Overview

Mercury is a lightweight demonstration of real-world secure communications concepts. It was designed and implemented as the CSE499 senior capstone project to show how a communications layer can protect payloads, detect tampering, reject replays, and keep security logic separate from transport logic.

The implementation is deliberately limited. Scope was constrained by academic time limits and by the requirement to avoid exposing proprietary processes developed for ShadowWorx Systems. What is shown is real engineering applied to the problem; what is omitted is intentional.

It is not a production system.

---

## Final Project Presentation

[Watch the Mercury CSE499 Final Project Presentation](https://www.youtube.com/watch?v=WH4le9u4RpQ)

---

## Scope

Mercury demonstrates core secure-communications principles within the boundaries of a senior capstone.

| Demonstrated | Limited by design |
| --- | --- |
| Secure envelope construction and validation | Production hardening |
| Pluggable authenticated-encryption providers | Full key-management and PKI |
| Transport abstraction | Proprietary ShadowWorx processes |
| Replay protection | Certification or classified use |
| Controlled failure behavior | Complete commercial feature set |

The limits exist because of time constraints and confidentiality. They are not claims that the underlying concepts are incomplete.

---

## Solution Structure

| Project | Purpose |
| --- | --- |
| Mercury.Abstractions | Interfaces, contracts, and shared models |
| Mercury.Core | Client coordination, envelope handling, replay protection |
| Mercury.Provider.AesGcm | AES-GCM provider |
| Mercury.Provider.ChaCha20 | ChaCha20-Poly1305 provider |
| Mercury.Provider.AesCcm | AES-CCM provider (included, not wired into RC 1.2 demos) |
| Mercury.Transport.InMemory | In-memory transport |
| Mercury.Transport.Tcp | Length-prefixed TCP transport |
| Mercury.Transport.FileDrop | File-drop transport (included, not wired into RC 1.2 demos) |
| Mercury.Demo.Console | Cross-platform console demo |
| Mercury.Demo.WinForms | Windows graphical demo |
| Mercury.Tests | xUnit tests |

---

## High-level flow

```text
Application
   ↓
Mercury Client
   ↓
Crypto Provider → SecureEnvelope
   ↓
Codec
   ↓
Transport (untrusted)
   ↓
Receiving Mercury Client
   ↓
Application (only after validation)
```

Security is applied above the transport. The transport only moves frames.

---

## Build and test

Requires the .NET SDK.

```powershell
dotnet restore
dotnet build
dotnet test
```

**Console demo**
```powershell
dotnet run --project Mercury.Demo.Console
```

**WinForms demo (Windows)**
```powershell
dotnet run --project Mercury.Demo.WinForms
```

---

## Known limitations

- No PKI, certificates, or production key management
- No key exchange or rotation
- Process-local in-memory replay protection
- Not production-hardened
- Demo-focused interfaces
- Proprietary ShadowWorx processes intentionally omitted

These constraints reflect the academic timeline and confidentiality requirements.

---

## Copyright

Copyright © 2026 Matthew D. Barker. All rights reserved.

Submitted in partial fulfillment of CSE499 at Brigham Young University–Idaho.  
No license is granted for commercial use, redistribution, or incorporation into other systems without explicit written permission.

The original academic submission remains under the BYU-Idaho account per course agreement. This repository is a personal copy.

---

## Summary

Mercury is a lightweight, working demonstration of secure communications principles. It was built under real constraints of time and confidentiality. The concepts are production-relevant; the implementation is scoped to what could be shown.
