<div align="center">

# The Mercury Project

### CSE499 Senior Capstone  
**Version 1.2.0-rc.1** · Academic Release Candidate

Matthew D. Barker  
Brigham Young University–Idaho

</div>

---

## What this is

Mercury is a lightweight, multi-project .NET prototype of a secure envelope-based communications layer, created as the CSE499 senior capstone project.

It demonstrates modular architecture, pluggable authenticated-encryption providers, secure envelope handling, transport abstraction, replay protection, controlled failure, working demos, and automated tests.

It is an academic proof-of-concept. It is not a production system.

## What this is not

This repository is **not** UmbraUplink, UmbraCipher, or any other ShadowWorx Systems product.

ShadowWorx Systems LLC develops separate, proprietary communications and security components. Those products are not open-sourced here. Mercury is earlier student work exploring related concepts only.

## Copyright and use

Copyright © 2026 Matthew D. Barker. All rights reserved.

Submitted in partial fulfillment of CSE499 at Brigham Young University–Idaho.  
No license is granted for commercial use, redistribution, or incorporation into other systems without explicit written permission.

The original academic submission remains under the BYU-Idaho account per course agreement. This is a personal copy.

---

## Final Project Presentation

[Watch the Mercury CSE499 Final Project Presentation](https://www.youtube.com/watch?v=WH4le9u4RpQ)

---

## Academic Scope

Mercury is a CSE499 senior project intended to demonstrate architecture, implementation, modularity, testing, and defensive design.

| It is | It is not |
| --- | --- |
| An academic prototype | A commercial product |
| A demonstration of secure-envelope design | A military or classified system |
| Modular and testable | DoD- or production-certified |
| Limited in scope by design | A full PKI or key-management system |

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

These limits are intentional.

---

## Summary

Mercury demonstrates a modular approach to protecting payloads over untrusted transports. It is academic work.

Protect the payload.  
Treat the transport as untrusted.  
Fail safely.  
Keep the commercial product separate.
