# Alephys lakehouse

Ansible site for the six-node Ozone, Iceberg, Trino, and Kyuubi platform. Kerberos, Ranger, Atlas, and Knox stay on. `versions.yml` is the version catalog.

## Commands

```
make bootstrap
make deploy
make test
make report
```

`make bootstrap` opens password SSH once (`--ask-pass` and `--ask-become-pass`) and installs an ed25519 key. The password is typed at the prompt. It is not in this repo. Set `BOOTSTRAP_SSH_PUBKEY` or `-e bootstrap_ssh_pubkey`.

`make deploy` runs `playbooks/site.yml`. `make test` runs `playbooks/validate.yml`. `make report` points at `reports/PROGRESS.md`.

## Live deploy is not finished

The encrypted vault and the OpenLakeHouse bind are in place. These are still open:

- AD CA trust. `trust_ad_ca` is false. The SHA256 is in `docs/DECISIONS.md`.
- PTR mismatches for test3 (`10.1.0.170`) and test6 (`10.1.0.118`). `allow_hosts_file_fallback` is true and Kerberos `rdns` is false. Preflight still treats this as red.

Tests have not passed. Do not treat a syntax check as a deployment.
