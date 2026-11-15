# Optional log panel: security warning

The imported Sanajinx bundle referenced an optional Node.js panel for viewing
captured logs. That panel is not included in this repository and is not needed
to run the proxy.

If you deploy an equivalent panel:

- Do not expose it directly on a public IP over plain HTTP.
- Bind it to `127.0.0.1` or a private interface.
- Put it behind an authenticated TLS reverse proxy (mTLS, SSO, or VPN).
- Restrict source addresses with firewall rules.
- Treat captured credentials and session tokens as highly sensitive material.
- Encrypt data at rest and delete it when the engagement ends.
- Prefer retrieving logs over an SSH tunnel instead of running a panel.

The old setup note suggested browsing the panel on `<server-ip>:3000`. Do not do
that. An unauthenticated panel on port 3000 exposes captured authentication data
to anyone who can reach it.
