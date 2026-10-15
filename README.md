# MTA-STS policy for eduworks.com

Served by GitHub Pages at https://mta-sts.eduworks.com/.well-known/mta-sts.txt. MTA-STS (RFC 8461) tells sending mail servers to deliver to eduworks.com only over TLS with a valid certificate. Required by NIST SP 800-171 3.13.1 and 3.13.8 (Eduworks POA&M C-22; Google Workspace Baseline Configuration item 5.4).

DNS (eduworks.com):

- `mta-sts` CNAME `eduworks.github.io`
- `_mta-sts` TXT `v=STSv1; id=<YYYYMMDDNN>` (change the id whenever the policy file changes)
- `_smtp._tls` TXT `v=TLSRPTv1; rua=mailto:it@eduworks.com`

Rollout: `mode: testing` for at least 2 weeks while TLS reports are reviewed, then `mode: enforce` with `max_age: 604800` or more, and a new `id`.

The `mx` lines must match the domain's MX records (Google Workspace). Keep this site up: in enforce mode, senders that cannot fetch a cached policy fall back to their previous policy until it expires.
