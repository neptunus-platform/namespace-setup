# Namespace Setup

This project provides a [Carvel package](https://carvel.dev/kapp-controller/docs/latest/packaging) for setting up namespaces with the necessary RBAC and Secrets to work with the platform.

## Components

* namespace-setup

## Configuration

The Namespace Setup package has the following configurable properties.

| Value | Required/Optional | Description |
|-------|-------------------|-------------|
| `registry.server` | Required | The FQDN for the container registry where to publish workload artifacts. |
| `registry.username` | Required | The username for the container registry where to publish workload artifacts. |
| `registry.password` | Required | The password for the container registry where to publish workload artifacts. |
| `namespaces` | Required | A list of namespaces to set up. |

```yaml
registry: 
  server: ghcr.io
  username: <username>
  password: <password>

namespaces:
  - name: default
    exists: True # If True, the namespace must exist.
  - name: dev
    exists: False # If False, the namespace will be created.
  - name: test
    exists: False
```

## Prerequisites

Before installing the Tekton Pipelines package, you need to add [the Neptunus Platform package repository](https://github.com/neptunus-platform/package-repository) to your cluster.

## Installation

You can install the Tekton package using `kctrl`:

   ```shell
   kctrl package install --package-install namespace-setup \
     --package namespace-setup.neptunus.thomasvitale.com \
     --version ${NAMESPACE_SETUP_PACKAGE_VERSION}
   ```

   > You can get the `${NAMESPACE_SETUP_PACKAGE_VERSION}` from running `kctrl
   > package available list -p namespace-setup.neptunus.thomasvitale.com`.
   > Specifying a namespace may be required depending on where your package
   > repository was installed.
