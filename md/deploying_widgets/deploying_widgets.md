## Deployment

### Usage (CLI)

**Command:** `deploy`

Deploys an app in the workspace via a convenient wrapper to [bos-cli-rs](https://github.com/bos-cli-rs/bos-cli-rs).

```cmd
bw deploy [app name] --deploy-account-id [deployAccountId] --signer-account-id [signerAccountId] --signer-public-key [signerPublicKey] --signer-private-key [signerPrivateKey]
```

- `[app name]`: Name of the app to be deployed. Assumed to be the current app in App structure (bos.config.json), but is required when using the Workspace structure (bos.workspace.json); this should match the name of the App's directory.
- `--deploy-account-id <deployAccountId>` (Optional): Account under which component code should be deployed. Defaults to `config.account`, or will use `config.accounts.deploy` if specified.

- `--signer-account-id <signerAccountId>` (Optional): Account which will be used for signing deploy transactions, frequently the same as deploy-account-id. Defaults to `config.account`, or will use `config.accounts.deploy` if specified.

- `--signer-public-key <signerPublicKey>` (Required): Public key for signing transactions in the format: `ed25519:<public_key>`.

- `--signer-private-key <signerPrivateKey>` (Required): Private key in `ed25519:<private_key>` format for signing transactions.

- `-n, --network <network>` (Optional): Network to deploy for (default: "mainnet").

### Usage (Git Workflow)

#### Prerequisites

1. Must be upgraded to bos-workspace v1, see the [migration guide](./MIGRATION_GUIDE.md)
2. Specify testnet [overrides + aliases](#aliases) in bos.config.json.

#### Mainnet

1. Create `.github/workflow/release-mainnet.yml`

```yml
name: Deploy Components to Mainnet
on:
  push:
    branches: [main]
jobs:
  deploy-mainnet:
    uses: NEARBuilders/bos-workspace/.github/workflows/deploy.yml@main
    with:
      bw-legacy: false
      deploy-env: "mainnet"
      app-name: "[APP_NAME]"
      deploy-account-address: "[DEPLOY_ACCOUNT]"
      signer-account-address: "[SIGNER_ACCOUNT]"
      signer-public-key: [PUBLIC_KEY]
    secrets:
      SIGNER_PRIVATE_KEY: ${{ secrets.SIGNER_PRIVATE_KEY }} // then configure this in your Github/Settings/Actions
```

#### Testnet

1. Create `.github/workflow/release-testnet.yml`

```yml
name: Deploy Components to Testnet
on:
  push:
    branches: [develop]
jobs:
  deploy-mainnet:
    uses: NEARBuilders/bos-workspace/.github/workflows/deploy.yml@main
    with:
      bw-legacy: false
      build-env: "testnet"
      deploy-env: "testnet"
      app-name: "[APP_NAME]"
      deploy-account-address: "[DEPLOY_ACCOUNT]" // testnet account
      signer-account-address: "[SIGNER_ACCOUNT]"
      signer-public-key: [PUBLIC_KEY]
    secrets:
      SIGNER_PRIVATE_KEY: ${{ secrets.SIGNER_PRIVATE_KEY }} // then configure this in your Github/Settings/Actions
```

Reference: [quickstart](https://github.com/nearbuilders/quickstart)
