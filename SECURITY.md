# Security

## What this software touches

Colony signs one EIP-191 message per paid ask and reads a private key from
`~/.telegraph/wallet.json` or `TELEGRAPH_PRIVATE_KEY`. It spends testnet USDC through a
Telegraph escrow balance, bounded by `--max-ask`, `--max-run` and `--max-day`.

It has no server, no database, no accounts, and no telemetry. The HTTP surface in
`colony/api.py` is unauthenticated by design and should be bound to localhost.

## Reporting

Email `169134776+atharhive@users.noreply.github.com` with the details. If the issue is a
fund loss or key exposure, say so in the subject line and include the commit hash.

Please do not open a public issue for a live vulnerability. There is no bounty program;
there is a fast reply.

## Hard rules for anyone running this

- Never commit a real key. `.env.example` shows the shape, not a value.
- The spend caps exist because a bug in a swarm is a spending bug. Keep them low.
- `verify_bundle.py` is the trust boundary. If a bundle fails it, do not use the memo.
