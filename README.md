# aws-iam-policy-tools

This repository contains demos of different tools that can be integrated in CI/CD processes for finding IAM policy misconfigurations:
- [trivy by aquasecurity](https://github.com/aquasecurity/trivy) - Trivy is a comprehensive and versatile security scanner. Trivy has scanners that look for security issues, and targets where it can find those issues. Targets (what Trivy can scan): Container Image, Filesystem, Git Repository (remote), Virtual Machine Image, Kubernetes, AWS. Scanners (what Trivy can find there): OS packages and software dependencies in use (SBOM), Known vulnerabilities (CVEs), IaC issues and misconfigurations, Sensitive information and secrets, Software licenses.


## Sample vulnerable templates

For this repository I used the following IaC templates:
- [CloudFormation](https://github.com/IgorSasovets/aws-iam-policy-tools/tree/main/clf-templates)
    - [cfngoat.yml](https://github.com/IgorSasovets/aws-iam-policy-tools/blob/main/clf-templates/cfngoat.yml) - [Cfngoat](https://github.com/bridgecrewio/cfngoat) was built to enable DevSecOps design and implement a sustainable misconfiguration prevention strategy. It can be used to test a policy-as-code framework like [Bridgecrew](https://bridgecrew.io/?utm_source=github&utm_medium=organic_oss&utm_campaign=cfngoat) & [Checkov](https://github.com/bridgecrewio/checkov/), inline-linters, pre-commit hooks or other code scanning methods.
    - [sample_insecure_iam_policies.yml](https://github.com/IgorSasovets/aws-iam-policy-tools/blob/main/clf-templates/sample_insecure_iam_policies.yml) - CF template that contains two overly permissive roles: Full S3 Access for Lambda, Full DynamoDB Access for API Gateway.
    - [sample_web_application.yml](https://github.com/IgorSasovets/aws-iam-policy-tools/blob/main/clf-templates/sample_web_application.yml) - CF template for sample web application that is using EC2, S3, Lambda, DynamoDB, CodeBuild, and SecretsManager services.
- [Terraform](https://github.com/IgorSasovets/aws-iam-policy-tools/tree/main/tf-templates)
    - [rhino_cloudgoat_lambda_privesc](https://github.com/IgorSasovets/aws-iam-policy-tools/tree/main/tf-templates/rhino_cloudgoat_lambda_privesc) - one of the scenarios [lambda_privesc](https://github.com/RhinoSecurityLabs/cloudgoat/tree/master/scenarios/lambda_privesc) from the [CloudGoat](https://github.com/RhinoSecurityLabs/cloudgoat) application. CloudGoat is Rhino Security Labs' "Vulnerable by Design" AWS deployment tool. It allows you to hone your cloud cybersecurity skills by creating and completing several "capture-the-flag" style scenarios. Each scenario is composed of AWS resources arranged together to create a structured learning experience. Some scenarios are easy, some are hard, and many offer multiple paths to victory. As the attacker, it is your mission to explore the environment, identify vulnerabilities, and exploit your way to the scenario's goal(s).
