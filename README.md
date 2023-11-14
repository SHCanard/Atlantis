# Atlantis

## Vault secrets

Some secrets come from Hashicorp Vault. If it is normally possible to inject them in a sidecar, here we use Vals-operator because it is simpler particularly since Atlantis and Vault do not reside inside the same K8s cluster.
`vals-secret.yaml` tells the Vals-operator which secrets to retrieve from Vault. After that just define secrets (like a native secret) as environment vars inside `statefulset.yaml`.

## SSL Certificates

Certificates are handled as secrets encoded in base64.
Modify `ca-root.yaml` to put root ca certs you need, i.e. CuSL root cert (to verify gitlab cert) and Terraform root cert (to verify registry.terraform.io).
For information, the fact that we need to add Terraform root cert is a known issue not specific to Atlantis: https://support.hashicorp.com/hc/en-us/articles/4415187888019--x509-certificate-signed-by-unknown-authority-from-Terraform-CLI-with-a-Terraform-Enterprise-remote
