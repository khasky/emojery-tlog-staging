# emojery-tlog-staging

A partial mirror of the Emojery transparency log of the staging deployment, `log-staging.emojery.app`. The log itself — entry bundles, hash tiles, ENROLL proofs and the current checkpoint — is at [`https://log-staging.emojery.app/g0/`](https://log-staging.emojery.app/g0/); this repository keeps the parts that need a shared, append-only history:

- `g<k>/anchors/` — every anchor: the log's checkpoint with its Sigstore Rekor entry, inclusion proof and shard checkpoint. Committed append-only, so every reader sees the same anchors.
- `index.json` — rewind records, if there ever are any.
- `jwks/<provider>/` — the sign-in providers' public keys, each committed the first time a verification run saw it in the provider's live key set; `jwksAdded` in that run's verdict line names the file.
- `verdicts/<YYYY-MM>.ndjson` — one line per verification run: verdict, origin, size, notes.
- `segments.json` — where each month's entries are archived (Zenodo, Internet Archive), once that archive exists.

A workflow in this repository runs [`emojery-verifier`](https://github.com/khasky/emojery-verifier) every 30 minutes and commits the result; only that workflow writes here. The operator runs it, so this is a record, not an independent audit — run the verifier yourself (`npx @emojery/verifier --log log-staging.emojery.app`) for that.

The log is pseudonymous. Do not attempt to re-identify pseudonyms in this log or link them with other data about a person.

The data is licensed under [CC BY 4.0](LICENSE).
