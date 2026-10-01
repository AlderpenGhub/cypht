# Caddy Routing

`Caddyfile.mail` enforces the mailbox boundary before traffic reaches Cypht:

- WINSANDBOX-VM (`192.168.40.75`) is proxied to DOCKER-VM port `8093`.
- Every other source receives the static page under `mail-restricted`.
- The fallback handler does not proxy any request to Cypht.

Before deployment, back up `/etc/caddy/Caddyfile`, install the static page at
`/var/www/mail-restricted/index.html`, append the reviewed site block, run
`caddy validate --config /etc/caddy/Caddyfile`, and reload only after validation
passes.

`mail-assist.alderpen.lan` is intentionally absent. Add its route only after
the authenticated management interface exists and its permitted client-device
policy has been chosen.
