# Cronicle Docker Images: Hard-coded secret_key to Unauthenticated RCE

CVE pending (reserved).

Several Cronicle Docker images bake a fixed `secret_key` into the image. The key is the same
for everyone who pulls the image, so any remote attacker can forge the worker's
server-to-server authentication and run arbitrary commands with no login. The tested image
runs as root, so the attacker gets code execution as root.

- Affected images: `soulteary/cronicle`, `intelliops/cronicle`, `cronicle/cronicle`, `nicholasamorim/cronicle`
- CWE-798 (Use of Hard-coded Credentials)
- CVSS 3.1: 9.8 Critical (AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H)

Cronicle installed from source generates a random `secret_key` per host and is not affected;
the issue is in these image builds.

Full write-up and proof of concept: **[HR-cronicle-docker-hardcoded-key-rce.pdf](HR-cronicle-docker-hardcoded-key-rce.pdf)**

## Disclaimer

This proof of concept is for authorized security testing and education only.
Test only systems that you own or have explicit permission to test. The author
takes no responsibility for misuse.
