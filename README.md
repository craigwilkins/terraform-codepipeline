# terraform-codepipeline
Terraform module that stands up a new AWS CodeCommit repository integrated with AWS CodePipeline. The CodePipeline consists of three stages:

1. A Source stage that is fed by the repository.
2. A Test stage that uses the artifacts of the Source and executes commands in `buildspec_test.yml`.
3. A Package stage that uses the artrifacts of the Test stage and excutes commands in `buildspec.yml`.

## Usage
```hcl
module "codecommit-cicd" {
    source                 = "git::https://terraform-codepipeline.git?ref=master"
    repo_name                 = "new-test-repo"              # Required
    organization_name         = "acme"                     # Required
    repo_default_branch       = "master"                     # Default value
    aws_region                = "ap-southeast-2"                  # Default value
    char_delimiter            = "-"                          # Default value
    environment               = "dev"                        # Default value
    build_timeout             = "5"                          # Default value
    build_compute_type        = "BUILD_GENERAL1_SMALL"       # Default value
    build_image               = "aws/codebuild/nodejs:6.3.1" # Default value
    build_privileged_override = "false"                      # Default value
    test_buildspec            = "buildspec_test.yml"         # Default value
    package_buildspec         = "buildspec.yml"              # Default value
    force_artifact_destroy    = "false"                      # Default value
}
```

<!-- BEGIN_TF_DOCS -->
# Name of your service

| Current Version |
|-----------------|
| 0.0.0           |

#### Module description

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_aws_region"></a> [aws_region](#input_aws_region) | The AWS region to deploy into (default: us-west-2). | `string` | `"us-west-2"` | no |
| <a name="input_build_compute_type"></a> [build_compute_type](#input_build_compute_type) | The build instance type for CodeBuild (default: BUILD_GENERAL1_SMALL) | `string` | `"BUILD_GENERAL1_SMALL"` | no |
| <a name="input_build_image"></a> [build_image](#input_build_image) | The build image for CodeBuild to use (default: aws/codebuild/nodejs:6.3.1) | `string` | `"aws/codebuild/nodejs:6.3.1"` | no |
| <a name="input_build_privileged_override"></a> [build_privileged_override](#input_build_privileged_override) | Set the build privileged override to 'true' if you are not using a CodeBuild supported Docker base image. This is only relevant to building Docker images | `string` | `"false"` | no |
| <a name="input_build_timeout"></a> [build_timeout](#input_build_timeout) | The time to wait for a CodeBuild to complete before timing out in minutes (default: 5) | `string` | `"5"` | no |
| <a name="input_char_delimiter"></a> [char_delimiter](#input_char_delimiter) | The delimiter to use for unique names (default: -) | `string` | `"-"` | no |
| <a name="input_environment"></a> [environment](#input_environment) | The environment being deployed (default: dev) | `string` | `"dev"` | no |
| <a name="input_force_artifact_destroy"></a> [force_artifact_destroy](#input_force_artifact_destroy) | Force the removal of the artifact S3 bucket on destroy (default: false). | `string` | `"false"` | no |
| <a name="input_organization_name"></a> [organization_name](#input_organization_name) | The organization name provisioning the template (e.g. acme) | `string` | `"acme"` | no |
| <a name="input_package_buildspec"></a> [package_buildspec](#input_package_buildspec) | The buildspec to be used for the Package stage (default: buildspec.yml) | `string` | `"buildspec.yml"` | no |
| <a name="input_repo_default_branch"></a> [repo_default_branch](#input_repo_default_branch) | The name of the default repository branch (default: master) | `string` | `"master"` | no |
| <a name="input_repo_name"></a> [repo_name](#input_repo_name) | The name of the CodeCommit repository (e.g. new-repo). | `string` | `""` | no |
| <a name="input_test_buildspec"></a> [test_buildspec](#input_test_buildspec) | The buildspec to be used for the Test stage (default: buildspec_test.yml) | `string` | `"buildspec_test.yml"` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_artifact_bucket"></a> [artifact_bucket](#output_artifact_bucket) | n/a |
| <a name="output_clone_repo_https"></a> [clone_repo_https](#output_clone_repo_https) | n/a |
| <a name="output_clone_repo_ssh"></a> [clone_repo_ssh](#output_clone_repo_ssh) | n/a |
| <a name="output_codebuild_role"></a> [codebuild_role](#output_codebuild_role) | n/a |
| <a name="output_codebuild_role_name"></a> [codebuild_role_name](#output_codebuild_role_name) | n/a |
| <a name="output_codepipeline_role"></a> [codepipeline_role](#output_codepipeline_role) | n/a |
| <a name="output_codepipeline_role_name"></a> [codepipeline_role_name](#output_codepipeline_role_name) | n/a |

## Modules

| Name | Source | Version |
|------|--------|---------|
| <a name="module_unique_label"></a> [unique_label](#module_unique_label) | git::https://github.com/cloudposse/terraform-null-label.git | tags/0.24.0 |

## Resources

| Name | Type |
|------|------|
| [aws_codebuild_project.build_project](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/codebuild_project) | resource |
| [aws_codebuild_project.test_project](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/codebuild_project) | resource |
| [aws_codecommit_repository.repo](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/codecommit_repository) | resource |
| [aws_codepipeline.codepipeline](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/codepipeline) | resource |
| [aws_iam_role.codebuild_assume_role](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role) | resource |
| [aws_iam_role.codepipeline_role](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role) | resource |
| [aws_iam_role_policy.attach_codepipeline_policy](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy) | resource |
| [aws_iam_role_policy.codebuild_policy](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy) | resource |
| [aws_kms_key.artifact_encryption_key](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/kms_key) | resource |
| [aws_s3_bucket.build_artifact_bucket](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket) | resource |
| [aws_s3_bucket_acl.build_artifact_bucket_acl](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket_acl) | resource |

## Usage

```
Directions on how to use
```
<!-- END_TF_DOCS -->
