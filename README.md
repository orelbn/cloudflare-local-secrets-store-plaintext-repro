# Cloudflare Local Secrets Store Plaintext Repro

This is a minimal reproduction for local-only Wrangler Secrets Store persistence storing secrets in plaintext on disk.

## Requirements

- `wrangler` available on your `PATH`

## Reproduction

From this directory, run:

```bash
mkdir -p .tmp/cf-secrets-persist
```

```bash
wrangler secrets-store secret create test-store \
  --name TEST_SECRET \
  --value 'UNIQUE_CF_SECRET_9d3f4b6e' \
  --scopes workers \
  --persist-to .tmp/cf-secrets-persist
```

```bash
rg -n 'UNIQUE_CF_SECRET_9d3f4b6e' .tmp/cf-secrets-persist
```

## Expected

No plaintext match on disk.

## Actual

The plaintext secret is found in the local persisted state under `.tmp/cf-secrets-persist`.
