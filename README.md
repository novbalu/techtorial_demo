# Cisco Techtorial 2023 Demo: 'ACI as Code a la Cisco CX'

## Setup

Install [Terraform](https://www.terraform.io/downloads), and the following two Python tools:

- [iac-validate](https://github.com/netascode/iac-validate)
- [iac-test](https://github.com/netascode/iac-test)

```shell
pip install -r requirements.txt
```

Set environment variables pointing to APIC:

```shell
export ACI_USERNAME=admin
export ACI_PASSWORD=!v3G@!4@Y
export ACI_URL=https://sandboxapicdc.cisco.com
```

Update the `cloud` block within the `terraform` configuration in `main.tf` to point to your Terraform Cloud Organization and Workspace:

```terraform
terraform {
  cloud {
    organization = "balnovak"

    workspaces {
      name = "techtorial-demo"
    }
  }
}
```

Or remove the `cloud` block completely to revert to local state storage.

## Initialization

```shell
terraform init
```

## Pre-Change Validation

```shell
iac-validate ./data/
```

## Terraform Plan/Apply

```shell
terraform apply
```

## Testing

```shell
iac-test --data ./data --data ./defaults.yaml --templates ./tests/templates --output ./tests/results/aci
```
