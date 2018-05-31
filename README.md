# Peering

Create and accept VPC Peering

[![Build Status](https://travis-ci.org/Flaconi/ansible-role-aws-vpc-peering.svg?branch=master)](https://travis-ci.org/Flaconi/ansible-role-aws-vpc-peering)
[![Version](https://img.shields.io/github/tag/Flaconi/ansible-role-aws-vpc-peering.svg)](https://github.com/Flaconi/ansible-role-aws-vpc-peering/tags)
[![Ansible Galaxy](https://img.shields.io/ansible/role/d/25995.svg)](https://galaxy.ansible.com/Flaconi/aws-vpc-peering/)

## Requirements

* Ansible 2.5

## Additional variables

Additional variables that can be used (either as `host_vars`/`group_vars` or via command line args):

| Variable                     | Description                  |
|------------------------------|------------------------------|
| `aws_vpc_peering_profile`        | Boto profile name to be used |
| `aws_vpc_peering_default_region` | Default region to use        |

## Example definition

#### With sane defaults
When using the sane defaults, the only thing to configure for each peering is:

* the name of the peering requester
* the name of the peering accepter

```yml
aws_vpc_peering:
  - reqfilter:
      "tag:Name": filter
    accfilter:
      "tag:Name": filter2
  - reqfilter:
      "tag:Name": filter
    accfilter:
      "tag:Name": filter3
  - reqfilter:
      "tag:Name": filter2
    accfilter:
      "tag:Name": filter3
```

#### Customized array
Instead of using somebody's sane defaults, you can also fully customize your peering.

```yml
aws_vpc_peering:
  - name: mypeering
    reqfilter:
      "tag:Name": filter
    region: eu-central-1
    accfilter:
      "tag:Name": filter2
    accregion: eu-west-1
  - reqfilter:
      "tag:Name": filter
    accfilter:
      "tag:Name": filter3
    accregion: eu-west-1
  - reqfilter:
      "tag:Name": filter2
    accfilter:
      "tag:Name": filter3
  - reqfilter:
      "tag:Name": filter
    region: eu-central-1
    accfilter:
      "tag:Name": filter4
```
