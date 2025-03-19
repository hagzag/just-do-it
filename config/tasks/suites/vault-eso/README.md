# Working with hashicorp-vault and external secrets operator

## Goals

- Get into the habit of working with a secrets manager for local development
- Learn the basics of `external secrets operator` and its integration with `vault`

## Prerequisites

- k3d
- helm
- basic vault understanding
- task (taskfile)

### Worth mentioning

This setup will initialize vault with a simple password - the password is `root` and you can use it both in the UI & vault API

### Installation

You can install all components using a single task command:

```sh
task vault:deploy:all
```

This will install:
1. Vault (in the `vault` namespace)
2. External Secrets Operator (in the `external-secrets` namespace)
3. Example configuration (in the `default` namespace)

If you prefer to install components individually:

```sh
# Install Vault
task vault:install

# Install External Secrets Operator
task vault:install:eso

# Install example configuration
task vault:demo:vault-eso:install
```

### Testing the external secret

To verify the external secret is functioning correctly:

```sh
task vault:test-result
```

## Architecture Details

1. Vault is installed in the `vault` namespace hence it's url is: `http://vault.vault:8200`
2. The token is `root` which is something you would probably do more securely in a public environment.
3. Cluster secret store is configured to retrieve secrets from vault via `clusterSecretStore`:

    ```yaml
    apiVersion: external-secrets.io/v1beta1
    kind: ClusterSecretStore
    metadata:
    name: vault-backend
    spec:
    provider:
        vault:
        auth:
            tokenSecretRef:
            key: token
            name: vault-token
            namespace: default
        path: secret
        server: http://vault.vault:8200
        version: v2
    ```

4. An external secret object is used to retrieve a secret via `clusterSecretStore`

    ```yaml
    apiVersion: external-secrets.io/v1beta1
    kind: ExternalSecret
    metadata:
    name: test
    namespace: default
    spec:
    data:
    - remoteRef:
        conversionStrategy: Default
        decodingStrategy: None
        key: secret/foo
        metadataPolicy: None
        property: hello
        secretKey: foobar
    refreshInterval: 15s
    secretStoreRef:
        kind: ClusterSecretStore
        name: vault-backend
    target:
        creationPolicy: Owner
        deletionPolicy: Retain
        name: test
    ```

## Cleanup

To remove all components:

```sh
task vault:cleanup:all
```

For individual component cleanup:

```sh
# Remove Vault
task vault:uninstall

# Remove External Secrets Operator
task vault:uninstall:eso

# Remove example configuration
task vault:demo:vault-eso:uninstall
```
