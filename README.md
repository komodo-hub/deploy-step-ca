# Deploy Step CA

Part of the [_Komodo Hub_ collection.](https://github.com/komodo-hub/komodo-hub)

Deploys Smallstep's `step-ca`, a private online certificate authority.

https://hub.docker.com/r/smallstep/step-ca

*Note.* After deploying, check the `fingerprint` service's log to get the certificate fingerprint.

## Komodo Resource TOML

```toml
[[stack]]
name = "step-ca"
[stack.config]
repo = "komodo-hub/deploy-step-ca"
file_paths = ["compose.yaml"]
ignore_services = ["fingerprint"]
environment = """
  ## Pass environment directory to container
  ## See https://hub.docker.com/r/smallstep/step-ca
  DOCKER_STEPCA_INIT_NAME = Smallstep
  DOCKER_STEPCA_INIT_DNS_NAMES = localhost,local
  DOCKER_STEPCA_INIT_REMOTE_MANAGEMENT = true

  ## Compose variables.
  STEPCA_PORT = 9000
  STEPCA_TAG = latest
  RESTART = unless-stopped
  LOGGING_DRIVER = local
"""
```
