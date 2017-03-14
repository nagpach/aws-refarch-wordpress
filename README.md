# Hosting WordPress on AWS

This reference architecture provides a set of YAML templates for deploying WordPress on AWS using [Amazon Virtual Private Cloud (Amazon VPC)](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Introduction.html), [Amazon Elastic Compute Cloud (Amazon EC2)](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html), [Auto Scaling](http://docs.aws.amazon.com/autoscaling/latest/userguide/WhatIsAutoScaling.html), [Elastic Load Balancing](http://docs.aws.amazon.com/elasticloadbalancing/latest/classic/introduction.html), [Amazon Relational Database Service (Amazon RDS)](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html), [Amazon ElastiCache](http://docs.aws.amazon.com/AmazonElastiCache/latest/UserGuide/WhatIs.html), [Amazon Elastic File System (Amazon EFS)](http://docs.aws.amazon.com/efs/latest/ug/whatisefs.html), [Amazon CloudFront](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Introduction.html), [Amazon Route 53](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/Welcome.html), [Amazon Certificate Manager (Amazon ACM)](http://docs.aws.amazon.com/acm/latest/userguide/acm-overview.html)  with [AWS CloudFormation](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html).

You can launch this CloudFormation stack, using your account, in the following AWS Regions:

| AWS Region Code | Name | Launch |
| --- | --- | --- 
| us-east-1 |US East (N. Virginia)| [![cloudformation-launch-stack](images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=WordPress&templateURL=https://s3.amazonaws.com/aws-us-east-1/reference-architecture/wordpress/latest/templates/aws-refarch-wordpress-master.yaml) |
| us-east-2 |US East (Ohio)| [![cloudformation-launch-stack](images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=us-east-2#/stacks/new?stackName=WordPress&templateURL=https://s3.amazonaws.com/aws-us-east-1/reference-architecture/wordpress/latest/templates/aws-refarch-wordpress-master.yaml) |
| us-west-2 |US West (Oregon)| [![cloudformation-launch-stack](images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/new?stackName=WordPress&templateURL=https://s3.amazonaws.com/aws-us-east-1/reference-architecture/wordpress/latest/templates/aws-refarch-wordpress-master.yaml) |
| eu-west-1 |EU (Ireland)| [![cloudformation-launch-stack](images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=eu-west-1#/stacks/new?stackName=WordPress&templateURL=https://s3.amazonaws.com/aws-us-east-1/reference-architecture/wordpress/latest/templates/aws-refarch-wordpress-master.yaml) |

## Overview

![architecture-overview](images/aws-refarch-wordpress.jpg)

The repository consists of a set of nested templates that deploy the following:






### Change the VPC or subnet IP ranges

This set of templates deploys the following network design:

| Item | CIDR Range | Usable IPs | Description |
| --- | --- | --- | --- |
| VPC | 10.0.0.0/16 | 65,536 | The whole range used for the VPC and all subnets |
| Application Subnet | 10.0.0.0/22 | 1022 | Private subnet in first Availability Zone |
| Application Subnet | 10.0.4.0/22 | 1022 | Private subnet in second Availability Zone |
| Application Subnet | 10.0.8.0/22 | 1022 | Private subnet in third Availability Zone (if available) |
| Database Subnet | 10.0.12.0/22 | 1022 | Private subnet in first Availability Zone |
| Database Subnet | 10.0.16.0/22 | 1022 | Private subnet in second Availability Zone |
| Database Subnet | 10.0.20.0/22 | 1022 | Private subnet in third Availability Zone (if available) |
| Web Subnet | 10.0.250.0/23 | 510 | Public subnet in first Availability Zone |
| Web Subnet | 10.0.252.0/23 | 510 | Public subnet in second Availability Zone |
| Web Subnet | 10.0.254.0/23 | 510 | Public subnet in third Availability Zone (if available) |

You can adjust the CIDR ranges used in this section of the [aws-refarch-wordpress-newvpc.yaml](/templates/aws-refarch-wordpress-newvpc.yaml) template:

```
Mappings:
  SubnetConfig:
    VPC:
      "CIDR": "10.0.0.0/16"
    ApplicationSubnet0:
      "CIDR": "10.0.0.0/22"
    ApplicationSubnet1:
      "CIDR": "10.0.4.0/22"
    ApplicationSubnet2:
      "CIDR": "10.0.8.0/22"
    DatabaseSubnet0:
      "CIDR": "10.0.12.0/22"
    DatabaseSubnet1:
      "CIDR": "10.0.16.0/22"
    DatabaseSubnet2:
      "CIDR": "10.0.20.0/22"
    WebSubnet0:
      "CIDR": "10.0.250.0/23"
    WebSubnet1:
      "CIDR": "10.0.252.0/23"
    WebSubnet2:
      "CIDR": "10.0.254.0/23"
```

### Add a new item to this list

If you found yourself wishing this set of frequently asked questions had an answer for a particular problem, please [submit a pull request](https://help.github.com/articles/creating-a-pull-request-from-a-fork/). The chances are that others will also benefit from having the answer listed here.

## Contributing

Please [create a new GitHub issue](https://github.com/darrylsosborne/aws-refarch-wordpress/issues/new) for any feature requests, bugs, or documentation improvements. 

Where possible, please also [submit a pull request](https://help.github.com/articles/creating-a-pull-request-from-a-fork/) for the change. 

## License

Copyright 2010-2017 Amazon.com, Inc. or its affiliates. All Rights Reserved.

Licensed under the Apache License, Version 2.0 (the "License"). You may not use this file except in compliance with the License. A copy of the License is located at

[http://aws.amazon.com/apache2.0/](http://aws.amazon.com/apache2.0/)

or in the "license" file accompanying this file. This file is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.
