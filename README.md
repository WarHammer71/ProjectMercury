<div align="center">

# Mercury

**CSE499 Senior Capstone Project**  
Brigham Young University–Idaho  
Matthew D. Barker

**Version 1.2.0-rc.1** · Academic Release Candidate

</div>

---

## What this is

Mercury is a lightweight, multi-project .NET prototype of a secure envelope-based communications layer. It was designed and implemented as the CSE499 senior capstone project.

It demonstrates:

- Separation of crypto, envelope, transport, and client coordination
- Pluggable authenticated-encryption providers (AES-GCM, ChaCha20-Poly1305)
- Secure envelope construction and validation
- Transport abstraction (in-memory, framed TCP)
- Replay protection
- Controlled failure behavior
- Working console and WinForms demonstrations
- Automated tests

It is an academic proof-of-concept. It is not a production system.

## What this is not

This repository is **not** UmbraUplink, UmbraCipher, or any other ShadowWorx Systems product.

ShadowWorx Systems LLC develops separate, proprietary, production-oriented communications and security components. Those products are not open-sourced here and are not derived from this academic submission. Mercury represents earlier student exploration of related concepts only.

## Copyright and use

Copyright © 2026 Matthew D. Barker. All rights reserved.

This code was submitted in partial fulfillment of CSE499 at Brigham Young University–Idaho.  
No license is granted for commercial use, redistribution, modification and redistribution as a product, or incorporation into other systems without explicit written permission from the copyright holder.

The original academic submission remains under the BYU-Idaho account per course agreement. This repository is a personal copy maintained by the author.

---

## Final Project Presentation

[Watch the Mercury CSE499 Final Project Presentation](https://www.youtube.com/watch?v=WH4le9u4RpQ)

---

## Academic Scope

Mercury is submitted as a CSE499 senior project. It is intended to demonstrate architecture, implementation, modularity, testing, and defensive design.

It is not:

- A commercial product
- A military or classified system
- A DoD-certified or production-certified system
- A complete identity, PKI, or key-management solution
- A chat application

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

~~~text
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
~~~

Security is applied above the transport. The transport only moves frames.

---

## Build and test

Requires the .NET SDK.

~~~powershell
dotnet restore
dotnet build
dotnet test
~~~

Console demo:

~~~powershell
dotnet run --project Mercury.Demo.Console
~~~

WinForms demo (Windows):

~~~powershell
dotnet run --project Mercury.Demo.WinForms
~~~

---

## Known limitations (academic scope)

- No PKI, certificates, or production key management
- No key exchange or rotation
- Process-local in-memory replay protection
- Not production-hardened
- Demo-focused interfaces

These limits are intentional. The project does not claim production readiness.

---

## Summary

Mercury shows a modular approach to protecting payloads over untrusted transports, with clear boundaries between crypto, encoding, transport, and client logic. It is academic work.

Protect the payload.  
Treat the transport as untrusted.  
Fail safely.  
Keep the commercial product separate.