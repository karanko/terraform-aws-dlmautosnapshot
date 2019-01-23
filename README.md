<!-- This file was automatically generated by the `build-harness`. Make all changes to `README.yaml` and run `make readme` to rebuild this file. -->

[![Slalom][logo]](https://slalom.com)

# terraform-aws-dlmautowsnapshot [![Build Status](https://travis-ci.com/JamesWoolfenden/terraform-aws-dlmautowsnapshot.svg?branch=master)](https://travis-ci.com/JamesWoolfenden/terraform-aws-dlmautowsnapshot) [![Latest Release](https://img.shields.io/github/release/JamesWoolfenden/terraform-aws-dlmautowsnapshot.svg)](https://github.com/JamesWoolfenden/terraform-aws-dlmautowsnapshot/releases/latest)

Terraform module - creates ups data lifecycle management to automate ebs backups.

---

This project uses the "build-harness" a modified version of the project ["SweetOps"](https://cpco.io/sweetops) from Cloudposse. Sweet indeed.

It's 100% Open Source and licensed under the [APACHE2](LICENSE).

## Usage

Include this repository as a module in your existing terraform code:

``` HCL
module "dlmautowsnapshot" {
  source          = "JamesWoolfenden/dlmautowsnapshot/aws"
  version         = "0.0.2"
  common_tags     = "${var.common_tags}"
  snapshot_name   = "${local.snapshot_name}"
  cron_expression = "${var.cron_expression}"
  regions         = "${var.regions}"
}
```

The management of EC2 backup has become simpler With the new release of Data Lifecycle Manager (DLM) policies https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/snapshot-lifecycle.html.
There is no more need for a Lambdas to manage EBS snapshots, and additionally with the new release of support for DLM in Terraform https://www.terraform.io/docs/providers/aws/r/dlm_lifecycle_policy.html it can achieved easily.

The example - exampleA shows how to implement a DLM policy on EBS snapshots.
As before you include a reference to the module in your code.

In the example the variable schedule is an extensible list of maps.

```JSON
  schedule = [{
      name = "2 weeks of daily snapshots"
      create_rule=[{
        interval      = 24
        interval_unit = "HOURS"
        times         = ["23:45"]
      }]

      retain_rule=[{
        count = 14
      }]

      tags_to_add {
        SnapshotCreator = "DLM"
      }

      copy_tags = false
    }
]
```

That's all for now.

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|:----:|:-----:|:-----:|
| schedule | - | list | - | yes |



## Related Projects

Check out these related projects.

- [terraform-aws-s3](https://github.com/jameswoolfenden/terraform-aws-s3) - S3 buckets

## Help

**Got a question?**

File a GitHub [issue](https://github.com/JamesWoolfenden/terraform-aws-dlmautowsnapshot/issues).

## Contributing

### Bug Reports & Feature Requests

Please use the [issue tracker](https://github.com/JamesWoolfenden/terraform-aws-dlmautowsnapshot/issues) to report any bugs or file feature requests.

## Copyrights

Copyright © 2019-2019 [Slalom, LLC](https://slalom.com)

## License

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

See [LICENSE](LICENSE) for full details.

    Licensed to the Apache Software Foundation (ASF) under one
    or more contributor license agreements.  See the NOTICE file
    distributed with this work for additional information
    regarding copyright ownership.  The ASF licenses this file
    to you under the Apache License, Version 2.0 (the
    "License"); you may not use this file except in compliance
    with the License.  You may obtain a copy of the License at

      https://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing,
    software distributed under the License is distributed on an
    "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
    KIND, either express or implied.  See the License for the
    specific language governing permissions and limitations
    under the License.

### Contributors

  [![James Woolfenden][jameswoolfenden_avatar]][jameswoolfenden_homepage]<br/>[James Woolfenden][jameswoolfenden_homepage] |


  [jameswoolfenden_homepage]: https://github.com/jameswoolfenden
  [jameswoolfenden_avatar]: https://github.com/jameswoolfenden.png?size=150

[logo]: https://gist.githubusercontent.com/JamesWoolfenden/5c457434351e9fe732ca22b78fdd7d5e/raw/15933294ae2b00f5dba6557d2be88f4b4da21201/slalom-logo.png
[website]: https://slalom.com
[github]: https://github.com/jameswoolfenden
[linkedin]: https://www.linkedin.com/company/slalom-consulting/
[twitter]: https://twitter.com/Slalom

[share_twitter]: https://twitter.com/intent/tweet/?text=terraform-aws-dlmautowsnapshot&url=https://github.com/JamesWoolfenden/terraform-aws-dlmautowsnapshot
[share_linkedin]: https://www.linkedin.com/shareArticle?mini=true&title=terraform-aws-dlmautowsnapshot&url=https://github.com/JamesWoolfenden/terraform-aws-dlmautowsnapshot
[share_reddit]: https://reddit.com/submit/?url=https://github.com/JamesWoolfenden/terraform-aws-dlmautowsnapshot
[share_facebook]: https://facebook.com/sharer/sharer.php?u=https://github.com/JamesWoolfenden/terraform-aws-dlmautowsnapshot
[share_googleplus]: https://plus.google.com/share?url=https://github.com/JamesWoolfenden/terraform-aws-dlmautowsnapshot
[share_email]: mailto:?subject=terraform-aws-dlmautowsnapshot&body=https://github.com/JamesWoolfenden/terraform-aws-dlmautowsnapshot
