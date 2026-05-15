# Security Policy

This document describes the security expectations for the Vector Network documentation and any protocol, SDK, or reference implementation that claims compliance with it.

## Scope

This policy applies to:

- protocol behavior described in the canonical specification
- wallet and identity handling
- signature verification and authorization logic
- record generation, replay, and validation
- delegation, recovery, and incident handling
- any implementation that stores, processes, or materializes Vector Network state

## Reporting security issues

Report security vulnerabilities through the project’s designated private security channel.

Do not disclose sensitive exploit details publicly until the issue has been reviewed and, where appropriate, mitigated.

If no private reporting channel is available, contact the maintainers through the repository’s prescribed security contact path.

## 1. Ownership model

Ownership is established by a cryptographic signature or a protocol-defined equivalent proof.

A vWallet owner MUST be able to demonstrate control over the associated public identity.

## 2. Private key handling

Private keys MUST NOT be exposed on any shared ledger or public record.

Implementations SHOULD:

- store private keys locally or in secure hardware
- avoid plaintext key export
- rotate or migrate keys only through explicit protocol support
- treat key compromise as a security incident

## 3. Authorization

Ownership proof and authorization are distinct.

- Ownership proof establishes control of the wallet identity.
- Authorization determines whether a specific operation is permitted.

A valid signature alone does not override certification, type, drain, space, or other protocol constraints.

## 4. Signature verification

Signature verification MUST:

- bind the initiator to the requested operation
- bind the request to the target vector or wallet
- prevent replay when the protocol uses nonces or nonce-equivalent fields
- fail closed on malformed input

## 5. Threat model

Implementations SHOULD account for at least the following threats:

- replay attacks
- signature forgery
- double settlement
- double-spend-like reuse
- malformed vector type injection
- unauthorized projection
- record rewriting
- cross-space confusion
- drain manipulation
- zero-vector normalization failure
- metadata spoofing

## 6. Defensive requirements

A compliant implementation SHOULD:

- use canonical serialization
- validate all numeric bounds
- reject negative or NaN values unless explicitly allowed
- enforce atomic transition logic
- log security-relevant events
- separate custody from ledger visibility
- use versioned rule sets

## 7. Delegation

Delegated authority MAY be supported only if the protocol defines:

- delegation scope
- expiry
- revocation
- replay protection
- audit trail

## 8. Recovery

If key compromise is detected, the protocol MAY support:

- revocation
- wallet freezing
- owner reauthentication
- migration to a new identity
- emergency governance actions

Every recovery action MUST be recorded.

## 9. Confidentiality

The protocol is not required to make all state private.

Sensitive material that is not necessary for validation SHOULD be minimized, encrypted, or represented by commitment rather than disclosed directly.

## 10. Security baseline

A system is not compliant if it:

- exposes private keys
- accepts unsigned owner-bound actions
- fails to detect replay where replay protection is declared
- allows hidden value creation
- silently bypasses certification

## 11. Versioning and maintenance

Security requirements MAY evolve as the protocol evolves. Implementations SHOULD track the version of the rules they enforce and MUST NOT claim compliance with requirements they do not implement.

Maintainers SHOULD review this policy whenever protocol rules, serialization formats, key-handling rules, or certification logic change.
