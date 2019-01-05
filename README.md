# Terraform-aws-dlmautosnapshot

The management of EC2 backup has become simpler With the new release of Data Lifecycle Manager (DLM) policies https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/snapshot-lifecycle.html. 
There is no more need for a Lambdas to manage EBS snapshots, and additionally with the new release of support for DLM in Terraform https://www.terraform.io/docs/providers/aws/r/dlm_lifecycle_policy.html it can achieved easily.

The Example - exampleA shows how to implement a DLM policy on EBS snapshots.
As before you include a reference to the module in your code:

~~~ HCL
module "ebsnapshot" {
  source   = "../../"
  schedule = "${var.schedule}"
}
~~~

Where the variable schedule is an extensible list of maps, as seen in the terraform tfvars of the example.

~~~ JSON
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
~~~

That's all for now.

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|:----:|:-----:|:-----:|
| schedule |  | list | - | yes |
�