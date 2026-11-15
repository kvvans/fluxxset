# Active phishlet

One phishlet is active, scoped to Microsoft 365:

| File | `name:` | Notes |
| --- | --- | --- |
| `o365.yaml` | `o365` | Primary O365 phishlet, `min_ver: 3.0.0` |

## Alternate variant (not active)

`docs/variants/office.yaml` is the imported Office variant (identity `office`).
Its hostnames overlap with `o365.yaml`. Do not copy it into
`evilginx2/phishlets/` while `o365.yaml` is active; loading both produces
hostname-collision warnings. It is retained for reference only.

The original Sanajinx bundle contained 16 phishlets. The non-M365 phishlets and
the legacy duplicate O365 variants were removed to:

- keep the repository scoped to the authorized Microsoft 365 engagement,
- avoid hostname collisions at startup, and
- avoid shipping unrelated brand-specific phishing configurations.

## Adding a phishlet

1. Put a single YAML file in `evilginx2/phishlets/`.
2. Make sure its `name:` is unique.
3. Check that its `hostnames` do not overlap with the active phishlet.
4. Review `min_ver`, proxy requirements, and any comments in the file.
5. Validate in an isolated lab before using it on an engagement.

## Do not commit runtime data

Never commit generated or captured data:

- `config.json`, `data.db`, `blacklist.txt`
- private keys or certificates (`*.pem`, `*.key`, `*.crt`)
- logs, captured credentials, tokens, or session cookies
- `.evilginx_cache`

These patterns are covered by `evilginx2/.gitignore`.

## Provenance

`o365.yaml` was imported from the Sanajinx-o365 bundle in `kvvans/evilginx`.
`office.yaml` was imported as an alternate variant and moved to
`docs/variants/office.yaml`; only its `name:` field was changed (from `o365` to
`office`). The duplicate legacy variant was not retained.
