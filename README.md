# aws-iam-policy-tools

This repository contains demos of different tools that can be integrated in CI/CD processes for finding IAM policy misconfigurations:
- [trivy by aquasecurity](https://github.com/aquasecurity/trivy) - Trivy is a comprehensive and versatile security scanner. Trivy has scanners that look for security issues, and targets where it can find those issues. Targets (what Trivy can scan): Container Image, Filesystem, Git Repository (remote), Virtual Machine Image, Kubernetes, AWS. Scanners (what Trivy can find there): OS packages and software dependencies in use (SBOM), Known vulnerabilities (CVEs), IaC issues and misconfigurations, Sensitive information and secrets, Software licenses.
- [Checkov by Prisma Cloud](https://www.checkov.io/) - Checkov is a static code analysis tool for infrastructure as code (IaC) and also a software composition analysis (SCA) tool for images and open source packages. It scans cloud infrastructure provisioned using Terraform, Terraform plan, Cloudformation, AWS SAM, Kubernetes, Helm charts, Kustomize, Dockerfile, Serverless, Bicep, OpenAPI or ARM Templates and detects security and compliance misconfigurations using graph-based scanning.
- [cfn_nag by Stelligent](https://github.com/stelligent/cfn_nag) - The cfn-nag tool looks for patterns in CloudFormation templates that may indicate insecure infrastructure. Roughly speaking, it will look for: IAM rules that are too permissive (wildcards), Security group rules that are too permissive (wildcards), Access logs that aren't enabled, Encryption that isn't enabled, Password literals.
- [parliamemt by duo-labs](https://github.com/duo-labs/parliament/) - parliament is an AWS IAM linting library. It reviews policies looking for problems such as: malformed json, missing required elements, incorrect prefix and action names, incorrect resources or conditions for the actions provided, type mismatches, bad policy patterns.


## Sample vulnerable templates

For this repository I used the following IaC templates:
- [CloudFormation](https://github.com/IgorSasovets/aws-iam-policy-tools/tree/main/clf-templates)
    - [cfngoat.yml](https://github.com/IgorSasovets/aws-iam-policy-tools/blob/main/clf-templates/cfngoat.yml) - [Cfngoat](https://github.com/bridgecrewio/cfngoat) was built to enable DevSecOps design and implement a sustainable misconfiguration prevention strategy. It can be used to test a policy-as-code framework like [Bridgecrew](https://bridgecrew.io/?utm_source=github&utm_medium=organic_oss&utm_campaign=cfngoat) & [Checkov](https://github.com/bridgecrewio/checkov/), inline-linters, pre-commit hooks or other code scanning methods.
    - [sample_insecure_iam_policies.yml](https://github.com/IgorSasovets/aws-iam-policy-tools/blob/main/clf-templates/sample_insecure_iam_policies.yml) - CF template that contains two overly permissive roles: Full S3 Access for Lambda, Full DynamoDB Access for API Gateway.
    - [sample_web_application.yml](https://github.com/IgorSasovets/aws-iam-policy-tools/blob/main/clf-templates/sample_web_application.yml) - CF template for sample web application that is using EC2, S3, Lambda, DynamoDB, CodeBuild, and SecretsManager services.
- [Terraform](https://github.com/IgorSasovets/aws-iam-policy-tools/tree/main/tf-templates)
    - [rhino_cloudgoat_lambda_privesc](https://github.com/IgorSasovets/aws-iam-policy-tools/tree/main/tf-templates/rhino_cloudgoat_lambda_privesc) - one of the scenarios [lambda_privesc](https://github.com/RhinoSecurityLabs/cloudgoat/tree/master/scenarios/lambda_privesc) from the [CloudGoat](https://github.com/RhinoSecurityLabs/cloudgoat) application. CloudGoat is Rhino Security Labs' "Vulnerable by Design" AWS deployment tool. It allows you to hone your cloud cybersecurity skills by creating and completing several "capture-the-flag" style scenarios. Each scenario is composed of AWS resources arranged together to create a structured learning experience. Some scenarios are easy, some are hard, and many offer multiple paths to victory. As the attacker, it is your mission to explore the environment, identify vulnerabilities, and exploit your way to the scenario's goal(s).

There is also one JSON file with sample insecure IAM policy:
- [iam-policies-json/sample_insecure_policy.json](https://github.com/IgorSasovets/aws-iam-policy-tools/blob/main/iam-policies-json/sample_insecure_policy.json) - sample insecure IAM policy with overly permissive statements for CodeBuild, IAM, EC2 services
