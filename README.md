# Peering

Create and accept VPC Peering

## Requirements

* Ansible 2.5

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
  - reqfilter:
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
