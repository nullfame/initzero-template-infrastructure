# Init Zero ⚛️ - Infrastructure Template 🏭👥

TODO: update the project header (e.g., `SPONSOR - AWS Infrastructure 🌨️`) 

AWS meta infrastructure management via CDK

## 📋 Stack Overview

* AWS CDK
    * CloudFormation to bootstrap GitHub OIDC
    * CDK for infrastructure deployment
* GitHub
    * Actions for CI/CD
    * Variables and secrets for configuration management

### Caveats

This template assumes a single-account setup. Multi-account setups can be managed by bootstrapping each account and triggering different CDK stacks for each account. This is outside the scope of this template.

## 💿 Infrastructure Deployment

### Pre-requisites

* An AWS account with sufficient permissions, the cleaner the better
    * Organizations allow existing account to create new sub-accounts with consolidated billing
* GitHub account or organization for CI/CD and configuration management

### Initial Setup

* Create a new GitHub using this repository as a template (or fork/copy this)
    * Suggested naming convention `SPONSOR-aws`, `SPONSOR-infrastructure`, or `SPONSOR-aws-infrastructure` for the truly undecided
    * `SPONSOR` is the GitHub username, GitHub organization, something else, or nothing at all
    * This will be referred to as the "infrastructure repository"
* Update the project header in this README and remove the TODO item
* Optionally edit/replace any/all README content (e.g., the Changelog)

### AWS Bootstrapping: OIDC and CDK

* Switch to "N. Virginia" (us-east-1) region
    * Other regions will work with additional configuration outside the scope of this template
* Visit CloudFormation in the AWS Console
* Create a new stack with the `github-actions-oidc-provider.yml` template
* In Step 2,
    * Name the stack `iam-github-actions-oidc-provider` or anything else
    * Set GithubRepoParam to the organization, slash, the infrastructure repository name (e.g., `SPONSOR/SPONSOR-aws-infrastructure`)
    * Optionally change the NonceParam to a random string
* Once deployed, make note of the `GitHubDeployIamRoleArn` output value (e.g., `arn:aws:iam::123456789012:role/iam-github-actions-oidc-provide-GitHubDeployIamRole-g4rb4g3t3xt`) in the Outputs tab
* Open the CloudShell from the lower left or services menu
* Run:
    * `
cdk bootstrap aws://$( aws sts get-caller-identity | jq -r '.Account' )/us-east-1`

## 📝 Changelog

| Date       | Version | Summary        |
| ---------- | ------- | -------------- |
|  12/9/2024 |   0.0.1 | Initial commit |

## 📜 License

[MIT License](./LICENSE.txt). Published by Finlayson Studio
