# Peering

Create and accept VPC Peering

[![Build Status](https://travis-ci.org/Flaconi/ansible-role-aws-vpc-peering.svg?branch=master)](https://travis-ci.org/Flaconi/ansible-role-aws-vpc-peering)
[![Version](https://img.shields.io/github/tag/Flaconi/ansible-role-aws-vpc-peering.svg)](https://github.com/Flaconi/ansible-role-aws-vpc-peering/tags)
[![Ansible Galaxy](https://img.shields.io/ansible/role/d/25995.svg)](https://galaxy.ansible.com/Flaconi/aws-vpc-peering/)

## Requirements

* Ansible 2.5

## Additional variables

Additional variables that can be used (either as `host_vars`/`group_vars` or via command line args):

| Variable                                | Description                  |
|-----------------------------------------|------------------------------|
| `aws_vpc_peering_profile`               | Boto profile name to be used |
| `aws_vpc_peering_default_region`        | Default region to use        |
| `aws_vpc_peering_vpc_filter_additional` | Additional `key` `val` filter to add to `vpc_acc_filter`, `vpc_acc_name`, `vpc_req_filter` and `vpc_req_name` by default. |

## Example definition

#### With sane defaults
When using the sane defaults, the only thing to configure for each peering is:
* the peering name
* the name or filter of the peering requester
* the name or filter of the peering accepter

```yml
aws_vpc_peering:
  - name: my-peering-1
    req_filter:
      - key: "tag:Name"
        val: vpc-1
      - key: "tag:Env"
        val: production
    acc_filter:
      - key: "tag:Name"
        val: vpc-2
      - key: "tag:Env"
        val: production
  - name:
    req_name: vpc-1
    acc_name: vpc-2
```

#### Customized array
Instead of using somebody's sane defaults, you can also fully customize your peering.

```yml
# Ensure VPC filter (name or filter) includes that the VPC is created already
# (not pending nor deleted)
aws_vpc_peering_vpc_filter_additional:
  - key: state
    val: available

aws_vpc_peering:
  - name: my-peering-1
    req_filter:
      - key: "tag:Name"
        val: vpc-1
      - key: "tag:Env"
        val: production
    acc_filter:
      - key: "tag:Name"
        val: vpc-2
      - key: "tag:Env"
        val: production
    region: eu-central-1
    tags:
      - key: env
        val: production
      - key: department
        val: devops

  - name:
    req_name: vpc-1
    acc_name: vpc-2
    region: eu-central-1
    tags:
      - key: env
        val: production
      - key: department
        val: devops
```


## Testing

#### Requirements

* Docker
* [yamllint](https://github.com/adrienverge/yamllint)

#### Run tests

```bash
# Lint the source files
make lint

# Run integration tests with default Ansible version
make test

# Run integration tests with custom Ansible version
make test ANSIBLE_VERSION=2.4
```
