
# AWS Environment Setup & IAM Documentation

## 1. Overview

This document describes the IAM permissions, resource tagging strategy, and AWS CodeBuild environment used by the AWS CI/CD pipeline.

## 2. IAM Permissions Strategy

The pipeline uses IAM roles to authorize communication between AWS services.

### CodePipeline Service Role

Required permissions include:

- CodeCommit: Retrieve source revisions.
- CodeBuild: Start builds and retrieve build status.
- Amazon S3: Access pipeline input and output artifacts.

### CodeBuild Service Role

Required permissions include:

- Amazon CloudWatch Logs: Create log streams and publish build logs.
- Amazon S3: Read and write required artifacts.
- CodeCommit: Retrieve source code when required by the configured source integration.

Permissions should be restricted to the resources required by each service. Avoid granting unnecessary administrative access.

## 3. AWS CLI Identity Verification

Verify the active AWS identity:

```bash
aws sts get-caller-identity
```

This command confirms the AWS account and identity associated with the current credentials.

## 4. Resource Tagging Strategy

The following tags provide a consistent approach to identifying project resources.

| Tag Key | Example Value | Purpose |
|---|---|---|
| `Project` | `aws-devops-ci` | Identifies project resources |
| `Environment` | `Development` | Identifies the deployment environment |
| `ManagedBy` | `AWS Console` | Identifies the management method |
| `Owner` | `Feezcodev` | Identifies the project owner |

Apply these tags to the relevant AWS resources and update the values to reflect the actual configuration.

## 5. AWS CodeBuild Environment

Example configuration:

- **Compute type:** `BUILD_GENERAL1_SMALL`
- **Environment image:** `aws/codebuild/standard:7.0`
- **Container type:** Linux
- **Service role:** The IAM role assigned to the CodeBuild project

Verify the actual environment settings in the AWS CodeBuild console before treating these values as confirmed.

## 6. Security Practices

- Follow the principle of least privilege.
- Never commit AWS access keys or secret credentials.
- Restrict access to artifact buckets.
- Review IAM policies regularly.
- Enable appropriate logging and monitoring.
- Keep build environments and dependencies maintained.

## 7. Verification Checklist

- [ ] IAM roles are configured.
- [ ] Service permissions are scoped appropriately.
- [ ] AWS CLI identity has been verified.
- [ ] Resource tags have been applied.
- [ ] CodeBuild environment settings have been confirmed.
- [ ] Build logs are available in CloudWatch.

---

**Project:** AWS CI/CD Automation Pipeline  
**GitHub:** [Feezcodev](https://github.com/Feezcodev)
