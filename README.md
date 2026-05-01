# harveybl.github.io

User-pages site. Hosts a Tesla Fleet API partner public key at
`/.well-known/appspecific/com.tesla.3p.public-key.pem` so Tesla can
verify domain control during partner-account registration.

The file at that path is intentionally public — it's a public key,
and Tesla requires it to be reachable over plain HTTPS for verification.

See https://developer.tesla.com/docs/fleet-api for the protocol.
