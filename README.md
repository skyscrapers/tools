# Skyscrapers public tools

This repo contains tools some tools that Skyscrapers and/or its customers use. These tools are then published in our [Homebrew tap](https://github.com/skyscrapers/homebrew-tap).

## Tools

### Terraform helper

All our infrastructure is deployed via Terraform. We heavily rely on Terraform for our day-to-day work. So this is a small helper script to make our lives, and those of our customers, a bit easier when running Terraform on our stacks.

These are the main two features of the helper script:

- full support for [Terraform standard stacks](https://github.com/skyscrapers/documentation/blob/master/coding_guidelines/terraform.md#standard-stack), including the ability to run `output`, `state` and `import` commands.
- automatically load variables and backend config from the customer repository root folder. Usefull to set a common backend config for all customer stacks or when there are some variables common for multiple stacks.

See the description in the script for more information.

You can install it with:

```bash
brew tap skyscrapers/tap
brew install tf
```

Examples:

```shell
export TF_STACK_PATH=~/projects/skyscrapers/stacks/kubernetes-stack/eks-cluster
tf init
tf workspace select staging
tf apply
tf output cluster_name
tf import 'foo.bar[\"lorem\"].hello' 'ipsum'
tf state list
```

*Note that it is important to correctly escape the input parameters for `import` commands.*

## Releasing

When it's time to release a new version of a tool contained in this repo, you must create a new release in this Github repository, following the [Semantic Versioning schema](https://semver.org/). Then you need to update the Brew manifest of the [Homebrew tap](https://github.com/skyscrapers/homebrew-tap/blob/main/tf.rb). The two values that must be updated in that manifest are `url` and `sha256`, which you can get by running:

```bash
brew create <the-new-release-archive-url.tar.gz>
```
