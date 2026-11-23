# Issuer and terminal-state policy

## Issuer validation

The configured USDC issuer is validated as a Stellar public key before a USDC
asset is constructed. Client input cannot provide an issuer, and an invalid
server configuration fails with a generic network configuration error rather
than producing a malformed asset or trustline operation.

This check is covered without contacting Horizon or submitting a trustline.
The configured issuer must still be independently verified against the
selected network during deployment.

## Terminal transaction states

Horizon's `successful: false` response is a terminal failed transaction state.
Polling returns `STELLAR_TX_FAILED` immediately and does not consume remaining
poll attempts. Only a not-found record is retried, with the configured bounded
attempt count, because the transaction may not have been ingested yet.
