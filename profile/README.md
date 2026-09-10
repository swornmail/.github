# SwornMail

**Cryptographic IPv6 prefix attestation for email.**

A single IPv6 /64 holds 18.4 quintillion addresses, so per-address reputation
carries no information and receivers fall back on blunt heuristics for IPv6
mail. SwornMail lets a sending operator attest, verifiably and at connection
time, that an address belongs to a declared prefix under one accountable
domain — giving receivers a stable reputation key instead of a guess.

- **Fail-open by design**: no attestation, or a broken one, means today's
  status quo — SwornMail must never make treatment worse, for reputation or
  for delivery
- **One TXT record to start** (DNS-only mode); optional signed connection
  tokens (174 bytes, Ed25519) for stronger binding
- **Key theft alone is bounded**: a token must be authorized by the
  operator's separately published policy and presented from inside the prefix
  it names
- **Reputation lands where the evidence is**: receivers key on the operator
  domain and the connecting /64, not on whatever range the operator claimed,
  unless they hold independent evidence of control over the wider prefix
- **Algorithm-agile**: a registry of key algorithms, with ML-DSA (FIPS 204)
  as the basis for a future post-quantum transition

## Status

The `-01` wire format is frozen. The Internet-Draft is written and not yet
submitted to the IETF; it is not a standard. Two independent verifiers (Go,
Rust) agree on 85 shared conformance vectors, and the rspamd module is checked
against the Go reference by a 259-case record differential. There are no
public deployments.

| Repo | Contents |
|---|---|
| `spec` | Internet-Draft source, test vectors, threat model |
| `swornmail-go` | Go reference library, CLI, Postfix milter, differential harnesses |
| `swornmail` | Independent Rust verifier, 0.2 or later ([crates.io](https://crates.io/crates/swornmail)) |
| `rspamd-swornmail` | rspamd module for DNS-only verification |
| `swornmail.com` · `swornmail.dev` | [Project site](https://swornmail.com) · [reference documentation](https://swornmail.dev) |

## Get involved

Read the draft, run the vectors, file issues. Security reports:
security@swornmail.dev (see SECURITY.md). Contributions under Apache-2.0
with DCO sign-off.

Maintained by Val Kafedzhy. Protocol
governance is intended to move to an open standards process as adoption
warrants.
