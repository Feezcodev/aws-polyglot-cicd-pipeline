
# 🚀 Polyglot CI/CD Automation Pipeline with AWS DevOps Services

## 📌 Project Overview

Implemented a CI/CD pipeline using AWS native DevOps services to automate application build workflows, validate runtime environments, and manage build artifacts.

## 🏗️ Architecture

```text
AWS CodeCommit
      |
      v
AWS CodePipeline
      |
      v
AWS CodeBuild
      |
      v
Amazon S3

CloudWatch Logs → Build Monitoring
AWS IAM         → Access Control
```

## 🛠️ Technologies Used

- AWS CodeCommit
- AWS CodePipeline
- AWS CodeBuild
- Amazon S3
- Amazon CloudWatch
- AWS IAM
- AWS CLI
- Go, Node.js, Python, YAML

## ⚙️ Implementation

- Configured an automated CI/CD workflow using AWS CodePipeline.
- Defined build commands and runtime configuration in `buildspec.yml`.
- Compiled and executed a Go application in CodeBuild.
- Configured IAM service roles and permissions for AWS service integration.
- Managed build artifacts through Amazon S3.
- Used CloudWatch Logs to inspect build execution.
- Verified AWS CLI authentication using `aws sts get-caller-identity`.

## 📸 Project Evidence

The `Screenshots/` directory contains evidence of pipeline execution, build logs, repository configuration, artifact storage, and AWS CLI identity verification.

## 👨‍💻 Author

**Feezco Touch**

GitHub: [@Feezcodev](https://github.com/Feezcodev)

*One project. One skill. One opportunity at a time.* 🚀
