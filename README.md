[![Banner][banner-image]](https://masterpoint.io/)

# github-action-tf-test

[![Release][release-badge]][latest-release]

💡 Learn more about Masterpoint [below](#who-we-are-𐦂𖨆𐀪𖠋).

## Purpose and Functionality

A reusable GitHub Action for testing Terraform and OpenTofu modules.

This action:

- Automates the process of running tests on your infrastructure code
- Supports optional AWS credentials configuration via OIDC
- Aqua-based dependency management
- Caching for faster execution
- Configurable AWS region and role session name

## Usage

### Basic Usage

```yaml
name: TF Test

on:
  push:
    branches:
      - main
  pull_request:

jobs:
  tf-test:
    name: 🧪 ${{ matrix.tf }} test
    runs-on: ubuntu-latest
    strategy:
      matrix:
        tf: [tofu, terraform]
    steps:
      - uses: masterpointio/github-action-tf-test/action.yaml@v1.0.0
        with:
          tf_type: ${{ matrix.tf }}
          github_token: ${{ secrets.GITHUB_TOKEN }}
```

### AWS Configuration

The action supports AWS authentication in two ways:

1. **Organization-level Environment Variable (Recommended)**

   - Set `TF_TEST_AWS_ROLE_ARN` in your GitHub organization's environment variables
   - This value will be automatically available to all workflows

2. **Input Parameter**
   - Pass the AWS role ARN directly in the workflow:
   ```yaml
   with:
     aws_role_arn: "arn:aws:iam::123456789012:role/your-role"
   ```

### Input Parameters

| Parameter           | Required | Default                 | Description                                                                               |
| ------------------- | -------- | ----------------------- | ----------------------------------------------------------------------------------------- |
| `tf_type`           | Yes      | -                       | Type of terraform to use (`tofu` or `terraform`)                                          |
| `aws_role_arn`      | No       | -                       | AWS role ARN to assume for testing (takes precedence over `TF_TEST_AWS_ROLE_ARN` env var) |
| `aws_region`        | No       | `us-east-1`             | AWS region to use                                                                         |
| `github_token`      | Yes      | -                       | GitHub token for checkout                                                                 |
| `role_session_name` | No       | `GitHubActions-TF-Test` | AWS role session name for OIDC authentication                                             |

### Required Permissions

Add these permissions to your workflow:

```yaml
permissions:
  actions: read
  checks: write
  contents: read
  id-token: write
  pull-requests: read
```

## How It Works

1. **Checkout**: Clones your repository
2. **Aqua Setup**: Installs and configures Aqua for dependency management
3. **AWS Configuration**: Sets up AWS credentials using OIDC
4. **Test Execution**: Runs `terraform init` and `terraform test` (or equivalent for OpenTofu)

## Dependencies

The action uses:

- [Aqua](https://aquaproj.github.io/) for dependency management
- [AWS OIDC](https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/configuring-openid-connect-in-amazon-web-services) for AWS authentication
- [actions/checkout](https://github.com/actions/checkout) for repository access
- [actions/cache](https://github.com/actions/cache) for dependency caching

## Built By

Powered by the [Masterpoint team](https://masterpoint.io/who-we-are/) and driven forward by contributions from the community ❤️

[![Contributors][contributors-image]][contributors-url]

## Contribution Guidelines

Contributions are welcome and appreciated!

Found an issue or want to request a feature? [Open an issue][issues-url]

Want to fix a bug you found or add some functionality? Fork, clone, commit, push, and PR — we'll check it out.

## Who We Are 𐦂𖨆𐀪𖠋

Established in 2016, Masterpoint is a team of experienced software and platform engineers specializing in Infrastructure as Code (IaC). We provide expert guidance to organizations of all sizes, helping them leverage the latest IaC practices to accelerate their engineering teams.

### Our Mission

Our mission is to simplify cloud infrastructure so developers can innovate faster, safer, and with greater confidence. By open-sourcing tools and modules that we use internally, we aim to contribute back to the community, promoting consistency, quality, and security.

### Our Commitments

- 🌟 **Open Source**: We live and breathe open source, contributing to and maintaining hundreds of projects across multiple organizations.
- 🌎 **1% for the Planet**: Demonstrating our commitment to environmental sustainability, we are proud members of [1% for the Planet](https://www.onepercentfortheplanet.org), pledging to donate 1% of our annual sales to environmental nonprofits.
- 🇺🇦 **1% Towards Ukraine**: With team members and friends affected by the ongoing [Russo-Ukrainian war](https://en.wikipedia.org/wiki/Russo-Ukrainian_War), we donate 1% of our annual revenue to invasion relief efforts, supporting organizations providing aid to those in need. [Here's how you can help Ukraine with just a few clicks](https://masterpoint.io/updates/supporting-ukraine/).

## Connect With Us

We're active members of the community and are always publishing content, giving talks, and sharing our hard earned expertise. Here are a few ways you can see what we're up to:

[![LinkedIn][linkedin-badge]][linkedin-url] [![Newsletter][newsletter-badge]][newsletter-url] [![Blog][blog-badge]][blog-url] [![YouTube][youtube-badge]][youtube-url]

... and be sure to connect with our founder, [Matt Gowie](https://www.linkedin.com/in/gowiem/).

## License

[Apache License, Version 2.0][license-url].

[![Open Source Initiative][osi-image]][license-url]

Copyright © 2016-2025 [Masterpoint Consulting LLC](https://masterpoint.io/)

<!-- MARKDOWN LINKS & IMAGES -->

[banner-image]: https://masterpoint-public.s3.us-west-2.amazonaws.com/v2/standard-long-fullcolor.png
[license-url]: https://opensource.org/license/apache-2-0
[osi-image]: https://i0.wp.com/opensource.org/wp-content/uploads/2023/03/cropped-OSI-horizontal-large.png?fit=250%2C229&ssl=1
[linkedin-badge]: https://img.shields.io/badge/LinkedIn-Follow-0A66C2?style=for-the-badge&logoColor=white
[linkedin-url]: https://www.linkedin.com/company/masterpoint-consulting
[blog-badge]: https://img.shields.io/badge/Blog-IaC_Insights-55C1B4?style=for-the-badge&logoColor=white
[blog-url]: https://masterpoint.io/updates/
[newsletter-badge]: https://img.shields.io/badge/Newsletter-Subscribe-ECE295?style=for-the-badge&logoColor=222222
[newsletter-url]: https://newsletter.masterpoint.io/
[youtube-badge]: https://img.shields.io/badge/YouTube-Subscribe-D191BF?style=for-the-badge&logo=youtube&logoColor=white
[youtube-url]: https://www.youtube.com/channel/UCeeDaO2NREVlPy9Plqx-9JQ
[release-badge]: https://img.shields.io/github/v/release/masterpointio/github-action-tf-test?color=0E383A&label=Release&style=for-the-badge&logo=github&logoColor=white
[latest-release]: https://github.com/masterpointio/github-action-tf-test/releases/latest
[contributors-image]: https://contrib.rocks/image?repo=masterpointio/github-action-tf-test
[contributors-url]: https://github.com/masterpointio/github-action-tf-test/graphs/contributors
[issues-url]: https://github.com/masterpointio/github-action-tf-test/issues
