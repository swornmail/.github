# SwornMail

**Cryptographic IPv6 prefix attestation for email.**

A single IPv6 /64 holds 18.4 quintillion addresses — per-address reputation
is mathematically dead, so receivers punish all IPv6 mail with blunt
heuristics, and email remains the last major workload where IPv6 is
operationally penalized. SwornMail fixes the root cause: it lets a sending
operator attest, verifiably and at connection time, that an address belongs
to a declared prefix under one accountable domain — giving receivers a
stable reputation unit instead of a guess.

- **Fail-open by design**: no attestation, or a broken one, means today's
  status quo — SwornMail cannot make deliverability worse
- **One TXT record to start** (DNS-only mode); optional signed connection
  tokens (135 bytes, Ed25519) for stronger binding
- **Key theft alone is useless**: verification also requires sourcing from
  inside the attested prefix
- **Post-quantum planned at birth**: algorithm-agile records, Falcon-512
  migration path

## Status

Early development. Internet-Draft in preparation; wire format not yet
frozen. Test vectors and two implementations (Go, Rust) verify against
shared vectors.

| Repo | Contents |
|---|---|
| `spec` | Internet-Draft source, test vectors, threat model |
| `swornmail-go` | Go library, Postfix milter, CLI |
| `swornmail` | Rust verifier crate ([crates.io](https://crates.io/crates/swornmail)) |

## Get involved

Read the draft, run the vectors, file issues. Security reports:
security@swornmail.dev (see SECURITY.md). Contributions under Apache-2.0
with DCO sign-off.

Maintained by [PlatOps Security, LLC](https://platops.com). Protocol
governance is intended to move to an open standards process as adoption
warrants.
